---
title: src/WaveDaqReconstruction.cxx
summary: File containing all methods of WaveDaqReconstruction class. 

---

# src/WaveDaqReconstruction.cxx

File containing all methods of [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md) class.  [More...](#detailed-description)

## Detailed Description

File containing all methods of [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md) class. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "WaveDaqReconstruction.h"

WaveDaqReconstruction::WaveDaqReconstruction()
{
    _Gain=1;
    _IsTDAQ = false;

    _WDTags.PrimaryParticle = None;
    _WDTags.BeamEnergy = 0;
    // _WDTags.Gain = 0;
    // _WDTags.BeamPositionX = 0;
    // _WDTags.BeamPositionY = 0;
    _WDTags.FileNumber = 0;

    _TDAQTags.RunNumber = 0;
    _TDAQTags.FileNumber = 0;

    _TrigTP = 0;
    _TrigFP = 0;
    _TrigTN = 0;
    _TrigFN = 0;

    /* Modify these variables to save Waveforms:
    * If _Debug is set to true, it saves additional branches and waveforms of CLK,
    * SC, TW and CALO in the output tree
    * _FirstEventToSave and _LastEventToSave define the range of events in which
    * Waveforms are saved -> if _Debug is set to false, these are not used
    */
    _Debug = false;
    _EnableHisto = false;
    _TriggerEnable = false;
    _FirstEventToSave = 1;
    _LastEventToSave = 50;
    _SaveNeutrons = false;

    _Event = 0;
};


/*************************************** RECONSTRUCTION MAIN **************************************/


void WaveDaqReconstruction::RunReconstruction(std::string FileName, std::string TimeCalFileName, int nEv = -1)
{
    //Set input file
    FILE* BinaryInputFilePtr = fopen(FileName.c_str(), "r");
    if(BinaryInputFilePtr == nullptr)
    {
        Error("RunReconstruction()", "Can not open input file %s", FileName.c_str());
        throw -1;
    }

    //Set time calibration file
    FILE* TimeCalFilePtr;
    if(_IsTDAQ)
    {
        TimeCalFilePtr = fopen(TimeCalFileName.c_str(), "r");
        if(TimeCalFilePtr == nullptr)
        {
            Error("RunReconstruction()", "Can not open time calibration file %s", TimeCalFileName.c_str());
            throw -1;
        }
    }
    else
        TimeCalFilePtr = BinaryInputFilePtr;

    //Set output file
    fout = new TFile(OutputFileName.c_str(),"recreate");
    TTree *RecTree = new TTree("rec_tree","rec_tree");

    if(!_SaveNeutrons)
        SetOutputTreeBranches(RecTree);
    else
        SetOutputNeutronWF(RecTree);

    //Set binary reader and load time calibration
    _BinaryReader = new CReadBinary(&_WaveFormContainer, &_TCBdata, &_BoardIdToIdMap, &_ActiveBoards, _TDCTime, &_TDCchMap, _hTGEN_MB, _hTGEN_frag, _hTriggerPattern, _hTriggerRates);
    _BinaryReader->CheckBinaryFileHeader(TimeCalFilePtr);
    _BinaryReader->LoadWaveDreamTimeCalibration(TimeCalFilePtr);
    
    if(!_IsTDAQ)
        BinaryInputFilePtr = TimeCalFilePtr;

    CheckLoadedBoards();

    //Get acquisition tags + display some messages
    GetFileTags(FileName);
    Message::DisplayMessageWithEmphasys("Running reconstruction");

    //Set max number of events to process to default value if not set before
    if(nEv == -1)   nEv = int(1E6);
    if( _SaveNeutrons )
    {
        _NbSlow = _WDChannelMap.GetNeutronChannelMap()->GetBoardSlow();
        _NbFast = _WDChannelMap.GetNeutronChannelMap()->GetBoardFast();
        _NeutronOn = false;
    }

    //Main event loop
    while(!feof(BinaryInputFilePtr) && _BinaryReader->ReadEvtStartWords(BinaryInputFilePtr))
    {
        if(_Event >= nEv)   break;

        _TriggerType = _BinaryReader->DecodeEvent(BinaryInputFilePtr);
        _IsFragTriggerOn = _BinaryReader->IsFragTriggerOn();
        LoopEvent(RecTree);
    }

    if( _EnableHisto || _Debug )    _BinaryReader->FillHistoTrigRates();

    //Finalize
    Message::DisplayMessage("Done");
    std::cout << "Writing file" << std::endl;
    fout->Write();
    fout->Close();

    if( _TriggerEnable )    PrintTriggerEfficiency();
}


void WaveDaqReconstruction::LoopEvent(TTree* RecTree)
{
    if( !_TriggerType )
    {
        Error("LoopEvent()", "Trigger Type not found in event %d!", _Event);
        throw -1;
    }

    std::map<UShort_t, Int_t>::iterator it;

    SetOutputDataToZero();

    //Waveform level analysis: first analyze SC WFs and then TW for CLK jitter calculations
    for(it = _ActiveBoards.begin(); _WDChannelMap.IsSCMapLoaded() && it != _ActiveBoards.end(); ++it)
    {
        if( _WDChannelMap.IsSCMapLoaded() && it->first == _WDChannelMap.GetSCChannelMap()->GetSCBoard() )
            AnalyzeWaveformsSC( it->first );
        else
            continue;
    }

    if( _SaveNeutrons )
    {
        for(it = _ActiveBoards.begin(); it != _ActiveBoards.end(); ++it)
        {
            if( it->first == _WDChannelMap.GetNeutronChannelMap()->GetBoardSlow() || 
                it->first == _WDChannelMap.GetNeutronChannelMap()->GetBoardFast() )
                FillNeutronWaveforms( it->first );
        }
    }
    else
    {
        for(auto it = _ActiveBoards.begin(); it != _ActiveBoards.end(); ++it)
        {
            if( _WDChannelMap.GetTWChannelMap()->IsBoardLoaded(it->first) )
                AnalyzeWaveformsTW(it->first);
            else if( _WDChannelMap.GetCALOChannelMap()->IsBoardLoaded(it->first) )
                AnalyzeWaveformsCALO(it->first);
            else if( _WDChannelMap.GetNeutronChannelMap()->IsBoardLoaded(it->first) )
                AnalyzeWaveformsNeutrons(it->first);
            else
            {
                // if(it->first == _WDChannelMap.GetSCChannelMap()->GetSCBoard())
                    continue;
                // else
                // {
                //  continue;
                //  // Error("LoopEvent()", "Board %d found in data but not in ChannelMap", it->first);
                //  // throw -1;
                // }
            }
        }

        //Bar level analysis
        if( _WDChannelMap.IsTWMapLoaded() )
            for(Int_t BarId = 0; BarId < NUMBEROFTWBARS; ++BarId)   AnalyzeSingleBarEvent(BarId);
    }

    //Histogram filling
    if(_Debug || _EnableHisto) FillHistograms();

    if( _SaveNeutrons )
    {
        if( _NeutronOn )    RecTree->Fill();
    }
    else
        RecTree->Fill();

    if( _TriggerEnable )
    {
        CheckFragTriggerConditions();
    }
    _BinaryReader->ResetFragTrigger();

    //Clear data and increase event number
    _TriggerType = 0;
    _IsFragTriggerOn = false;
    for(it = _ActiveBoards.begin(); it != _ActiveBoards.end(); ++it)
        _WaveFormContainer[it->second]->ClearData();
    _Event ++;
    _NeutronOn = false;
}


/******************* SET DATASETS AND TREES *******************/

void WaveDaqReconstruction::SetDebugMode(Int_t first_ev, Int_t last_ev)
{
    _Debug = true;
    _FirstEventToSave = first_ev;
    _LastEventToSave = last_ev;
    if( !_EnableHisto ) EnableHistograms();
}


void WaveDaqReconstruction::SetOutputDataToZero()
{
    memset(_TDCTime, 0, sizeof(Float_t)*4);

    if( _WDChannelMap.IsSCMapLoaded() )
    {
        _SCTime = 0;
        _SC_CLK_phase = 0;
        if(_Debug)
        {
            memset(_SCPedestal,0,sizeof(Float_t)*NUMBEROFSCCHANNELS);
            memset(_SCPedestalRMS,0,sizeof(Float_t)*NUMBEROFSCCHANNELS);
            memset(_SCAmplitude,0,sizeof(Float_t)*NUMBEROFSCCHANNELS);
            memset(_SCCharge,0,sizeof(Float_t)*NUMBEROFSCCHANNELS);
            memset(_SCRiseTime,0,sizeof(Float_t)*NUMBEROFSCCHANNELS);
        }
    }

    if( _SaveNeutrons )
    {
        for(int i=0; i<NEUTRONSLOWCHANNELS; ++i) _NS_WF[i].clear();
        for(int i=0; i<NEUTRONFASTCHANNELS; ++i) _NF_WF[i].clear();
        return;
    }

    if( _WDChannelMap.IsTWMapLoaded() )
    {
        memset(_CPedestal,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CPedestalRMS,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CAmplitude,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CTimestamps,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CTimestampsCorrJit,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CCharge,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CRiseTime,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);
        memset(_CLK_Jitter,0,sizeof(Float_t)*NUMBEROFGLOBALCHANNELSTW);

        memset(_CLK_phase,0,sizeof(Float_t)*MAXNUMBEROFBOARDS*2);

        memset(_CPedA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CPedB,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CPedRMSA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CPedRMSB,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CAmpA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CAmpB,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CChargeA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CChargeB,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CTimeA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CTimeB,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CRiseTimeA,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_CRiseTimeB,0,sizeof(Float_t)*NUMBEROFTWBARS);

        memset(_BTimestamps,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_BCharge,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_BDeltaT,0,sizeof(Float_t)*NUMBEROFTWBARS);
        memset(_BCratio,0,sizeof(Float_t)*NUMBEROFTWBARS);

        if( _WDChannelMap.IsSCMapLoaded() )
            memset(_TOF,0,sizeof(Float_t)*NUMBEROFTWBARS);
    }

    if( _WDChannelMap.IsCALOMapLoaded() )
    {
        memset(_CALOPedestal,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALOPedestalRMS,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALOAmplitude,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALOTimestamps,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALOTimestampsCorrJit,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALOCharge,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
        memset(_CALORiseTime,0,sizeof(Float_t)*NUMBEROFCRYSTALS);
    }

    if( _WDChannelMap.IsNeutronMapLoaded() )
    {
        memset(_NSPed,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);
        memset(_NSPedRMS,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);
        memset(_NSAmp,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);
        memset(_NSCharge,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);
        memset(_NSRiseTime,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);
        memset(_NSTime,0,sizeof(Float_t)*NEUTRONSLOWCHANNELS);

        memset(_NFPed,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
        memset(_NFPedRMS,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
        memset(_NFAmp,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
        memset(_NFCharge,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
        memset(_NFRiseTime,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
        memset(_NFTime,0,sizeof(Float_t)*NEUTRONFASTCHANNELS);
    }
}


void WaveDaqReconstruction::SetOutputTreeBranches(TTree* RecTree)
{
    //Set debug folders to save some waveforms
    if(_Debug)
    {
        //SC Waveforms
        if( _WDChannelMap.IsSCMapLoaded() ) gDirectory->mkdir("WavesSC");

        //TW Waveforms
        if( _WDChannelMap.IsTWMapLoaded() ) gDirectory->mkdir("WavesTW");

        //CALO Waveforms
        if( _WDChannelMap.IsCALOMapLoaded() )   gDirectory->mkdir("WavesCALO");

        //Neutron Waveforms
        if( _WDChannelMap.IsNeutronMapLoaded() )    gDirectory->mkdir("WavesNeutrons");

        //CLK Waveforms
        gDirectory->mkdir("WavesCLK");
    }

    if(_Debug || _EnableHisto)
    {
        //Histograms directory
        gDirectory->mkdir("Histos");
        CreateHistograms();
    }

    // SC timestamps
    if( _WDChannelMap.IsSCMapLoaded() ) RecTree->Branch("SC_Timestamp",&_SCTime,"SC_Timestamp/F");

    // Waveform level data
    if(_Debug)
    {
        if( _WDChannelMap.IsSCMapLoaded() )
        {
            TString SCChannels = "";
            for(Int_t i=0; i<NUMBEROFSCCHANNELS; ++i)   SCChannels += Form("SC_Channel%d/F:", i);
            SCChannels.Remove(TString::kTrailing, ':');

            RecTree->Branch("Deb_SC_Ped", _SCPedestal, SCChannels, 1);
            RecTree->Branch("Deb_SC_PedRMS", _SCPedestalRMS, SCChannels, 1);
            RecTree->Branch("Deb_SC_Amp", _SCAmplitude, SCChannels, 1);
            RecTree->Branch("Deb_SC_Charge", _SCCharge, SCChannels, 1);
            RecTree->Branch("Deb_SC_RiseTime", _SCRiseTime, SCChannels, 1);
        }

        /*Strings used for leaves definition: in debug mode data is stored
        * separately for each channel and for each bar
        */
        if( _WDChannelMap.IsTWMapLoaded() )
        {
            TString Channels = "", Bars = "";
            std::string Layer, Side;
            Int_t BarId;

            for(Int_t i=0; i<NUMBEROFGLOBALCHANNELSTW; ++i)
            {
                BarId = _GlobalToBarChIDpairMap[i].first;
                Side = _GlobalToBarChIDpairMap[i].second;
                Layer = BarId < LAYERXBARMIN ? "LayerY" : "LayerX";

                Channels += Form("TW_GlobCh%d_%s_Bar%d_%s/F:", i, Layer.c_str(), BarId, Side.c_str());
            }
            Channels.Remove(TString::kTrailing, ':'); //remove trailing ':' to avoid errors

            for(Int_t i=0; i<NUMBEROFTWBARS; ++i)
            {
                Layer = i < LAYERXBARMIN ? "LayerY" : "LayerX";
                Bars += (Layer+Form("_Bar_%d/F:", i));
            }
            Bars.Remove(TString::kTrailing, ':');

            //set up branches for data of each channel
            RecTree->Branch("Deb_TW_CH_Pedestal",_CPedestal,Channels,1);
            RecTree->Branch("Deb_TW_CH_PedestalRMS",_CPedestalRMS,Channels,1);
            RecTree->Branch("Deb_TW_CH_Amplitude",_CAmplitude,Channels,1);
            RecTree->Branch("Deb_TW_CH_Charge",_CCharge,Channels,1);
            RecTree->Branch("Deb_TW_CH_Timestamps",_CTimestamps,Channels,1);
            RecTree->Branch("Deb_TW_CH_TimestampsCorrJit",_CTimestampsCorrJit,Channels,1);
            RecTree->Branch("Deb_TW_CH_RiseTime",_CRiseTime,Channels,1);
            RecTree->Branch("Deb_TW_CH_CLKJitter",_CLK_Jitter,Channels,1);

            //set up branches for data of each bar
            RecTree->Branch("Deb_BAR_Charge", _BCharge, Bars,1);
            RecTree->Branch("Deb_BAR_Timestamp", _BTimestamps, Bars,1);
            RecTree->Branch("Deb_BAR_DeltaT_AB", _BDeltaT, Bars,1);
            RecTree->Branch("Deb_BAR_LogCratio_AB", _BCratio, Bars,1);

            if( _WDChannelMap.IsSCMapLoaded() ) RecTree->Branch("Deb_BAR_TOF",_TOF,Bars,1);
        }

        //Setup debug branches for CALO
        if( _WDChannelMap.IsCALOMapLoaded() )
        {
            TString Crystals = "";
            Int_t ModuleId;
            std::pair<UShort_t, Int_t> BoardChPair;
            for(int iCrys = 0; iCrys < NUMBEROFCRYSTALS; ++iCrys)
            {
                ModuleId = _WDChannelMap.GetCALOChannelMap()->GetModuleFromCrys(iCrys);
                BoardChPair = _WDChannelMap.GetCALOChannelMap()->GetBoardChFromCrys(iCrys);
                Crystals += Form("Crys%d_Mod%d_B%hu_Ch%d/F:", iCrys, ModuleId, BoardChPair.first, BoardChPair.second);
            }
            Crystals.Remove(TString::kTrailing, ':');

            RecTree->Branch("Deb_CRY_Ped", _CALOPedestal, Crystals, 1);
            RecTree->Branch("Deb_CRY_PedRMS", _CALOPedestalRMS, Crystals, 1);
            RecTree->Branch("Deb_CRY_Amp", _CALOAmplitude, Crystals, 1);
            RecTree->Branch("Deb_CRY_Charge", _CALOCharge, Crystals, 1);
            RecTree->Branch("Deb_CRY_RiseTime", _CALORiseTime, Crystals, 1);
            RecTree->Branch("Deb_CRY_Time", _CALOTimestamps, Crystals, 1);
            RecTree->Branch("Deb_CRY_TimeCorr", _CALOTimestampsCorrJit, Crystals, 1);
        }

        if( _WDChannelMap.IsNeutronMapLoaded() )
        {
            bool chFound = false;
            std::string detName;
            TString Detectors = "";
            Int_t globCh;
            UShort_t board = _WDChannelMap.GetNeutronChannelMap()->GetBoardSlow();
            std::vector<Int_t>* channels = _WDChannelMap.GetNeutronChannelMap()->GetChSlow();
            for(int i=0; i<channels->size(); ++i)
            {
                chFound = _WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, channels->at(i)), &globCh);
                detName = _WDChannelMap.GetNeutronChannelMap()->GetDetFromBoardCh(std::make_pair(board, channels->at(i)));
                if(!chFound)
                {
                    Error("SetOutputTreeBranches()","Requested channel for neutrons (board %hu, ch %d) not found in channel map", board, channels->at(i));
                    throw -1;
                }
                Detectors += Form("%s_SLOW_b%hu_ch%d_glob%d/F:", detName.c_str(), board, channels->at(i), globCh);
                chFound = false;
            }
            Detectors.Remove(TString::kTrailing, ':');

            RecTree->Branch("Deb_NS_Ped", _NSPed, Detectors, 1);
            RecTree->Branch("Deb_NS_PedRMS", _NSPedRMS, Detectors, 1);
            RecTree->Branch("Deb_NS_Amp", _NSAmp, Detectors, 1);
            RecTree->Branch("Deb_NS_Charge", _NSCharge, Detectors, 1);
            RecTree->Branch("Deb_NS_RiseTime", _NSRiseTime, Detectors, 1);
            RecTree->Branch("Deb_NS_Time", _NSTime, Detectors, 1);

            Detectors = "";
            board = _WDChannelMap.GetNeutronChannelMap()->GetBoardFast();
            channels = _WDChannelMap.GetNeutronChannelMap()->GetChFast();
            for(int i=0; i<channels->size(); ++i)
            {
                chFound = _WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, channels->at(i)), &globCh);
                detName = _WDChannelMap.GetNeutronChannelMap()->GetDetFromBoardCh(std::make_pair(board, channels->at(i)));
                if(!chFound)
                {
                    Error("SetOutputTreeBranches()","Requested channel for neutrons (board %hu, ch %d) not found in channel map", board, channels->at(i));
                    throw -1;
                }
                Detectors += Form("%s_FAST_b%hu_ch%d_glob%d/F:", detName.c_str(), board, channels->at(i), globCh);
                chFound = false;
            }
            Detectors.Remove(TString::kTrailing, ':');

            RecTree->Branch("Deb_NF_Ped", _NFPed, Detectors, 1);
            RecTree->Branch("Deb_NF_PedRMS", _NFPedRMS, Detectors, 1);
            RecTree->Branch("Deb_NF_Amp", _NFAmp, Detectors, 1);
            RecTree->Branch("Deb_NF_Charge", _NFCharge, Detectors, 1);
            RecTree->Branch("Deb_NF_RiseTime", _NFRiseTime, Detectors, 1);
            RecTree->Branch("Deb_NF_Time", _NFTime, Detectors, 1);
        }
    }

    // Bar level Data
    if( _WDChannelMap.IsTWMapLoaded() )
    {
        RecTree->Branch("BAR_PedA", _CPedA, Form("BAR_PedA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_PedB", _CPedB, Form("BAR_PedB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_PedRMSA", _CPedRMSA, Form("BAR_PedRMSA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_PedRMSB", _CPedRMSB, Form("BAR_PedRMSB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_AmpA", _CAmpA, Form("BAR_AmpA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_AmpB", _CAmpB, Form("BAR_AmpB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_ChargeA", _CChargeA, Form("BAR_ChargeA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_ChargeB", _CChargeB, Form("BAR_ChargeB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_TimeA", _CTimeA, Form("BAR_TimeA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_TimeB", _CTimeB, Form("BAR_TimeB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_RiseTimeA", _CRiseTimeA, Form("BAR_RiseTimeA[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_RiseTimeB", _CRiseTimeB, Form("BAR_RiseTimeB[%d]/F", NUMBEROFTWBARS));

        RecTree->Branch("BAR_Charge", _BCharge, Form("BAR_Charge[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_Timestamp", _BTimestamps, Form("BAR_Timestamp[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_DeltaT_AB", _BDeltaT, Form("BAR_DeltaT_AB[%d]/F", NUMBEROFTWBARS));
        RecTree->Branch("BAR_LogCratio_AB", _BCratio, Form("BAR_LogCratio_AB[%d]/F", NUMBEROFTWBARS));

        //TOF Data
        if( _WDChannelMap.IsSCMapLoaded() )
            RecTree->Branch("BAR_TOF_Uncal", _TOF, Form("BAR_TOF_Uncal[%d]/F", NUMBEROFTWBARS));
    }

    if( _WDChannelMap.IsCALOMapLoaded() )
    {
        RecTree->Branch("CRY_Ped", _CALOPedestal, Form("CRY_Ped[%d]/F", NUMBEROFCRYSTALS));
        RecTree->Branch("CRY_PedRMS", _CALOPedestalRMS, Form("CRY_PedRMS[%d]/F", NUMBEROFCRYSTALS));
        RecTree->Branch("CRY_Amp", _CALOAmplitude, Form("CRY_Amp[%d]/F", NUMBEROFCRYSTALS));
        RecTree->Branch("CRY_Charge", _CALOCharge, Form("CRY_Charge[%d]/F", NUMBEROFCRYSTALS));
        RecTree->Branch("CRY_RiseTime", _CALORiseTime, Form("CRY_RiseTime[%d]/F", NUMBEROFCRYSTALS));
        RecTree->Branch("CRY_Time", _CALOTimestampsCorrJit, Form("CRY_Time[%d]/F", NUMBEROFCRYSTALS));
    }

    if( _WDChannelMap.IsNeutronMapLoaded() )
    {
        RecTree->Branch("NS_Ped", _NSPed, Form("NS_Ped[%d]/F", NEUTRONSLOWCHANNELS));
        RecTree->Branch("NS_PedRMS", _NSPedRMS, Form("NS_PedRMS[%d]/F", NEUTRONSLOWCHANNELS));
        RecTree->Branch("NS_Amp", _NSAmp, Form("NS_Amp[%d]/F", NEUTRONSLOWCHANNELS));
        RecTree->Branch("NS_Charge", _NSCharge, Form("NS_Charge[%d]/F", NEUTRONSLOWCHANNELS));
        RecTree->Branch("NS_RiseTime", _NSRiseTime, Form("NS_RiseTime[%d]/F", NEUTRONSLOWCHANNELS));
        RecTree->Branch("NS_Time", _NSTime, Form("NS_Time[%d]/F", NEUTRONSLOWCHANNELS));

        RecTree->Branch("NF_Ped", _NFPed, Form("NF_Ped[%d]/F", NEUTRONFASTCHANNELS));
        RecTree->Branch("NF_PedRMS", _NFPedRMS, Form("NF_PedRMS[%d]/F", NEUTRONFASTCHANNELS));
        RecTree->Branch("NF_Amp", _NFAmp, Form("NF_Amp[%d]/F", NEUTRONFASTCHANNELS));
        RecTree->Branch("NF_Charge", _NFCharge, Form("NF_Charge[%d]/F", NEUTRONFASTCHANNELS));
        RecTree->Branch("NF_RiseTime", _NFRiseTime, Form("NF_RiseTime[%d]/F", NEUTRONFASTCHANNELS));
        RecTree->Branch("NF_Time", _NFTime, Form("NF_Time[%d]/F", NEUTRONFASTCHANNELS));
    }

    //Trigger and tags
    RecTree->Branch("TriggerType", &_TriggerType, "TriggerType/I");
    RecTree->Branch("IsFragTriggerOn", &_IsFragTriggerOn, "IsFragTriggerOn/O");
    RecTree->Branch("EventNumber", &_Event, "EventNumber/I");
    if(_IsTDAQ)
        RecTree->Branch("Tags", &_TDAQTags, "RunNumber/I:FileNumber/I");
    else
        RecTree->Branch("Tags", &_WDTags, "BeamEnergy/F:PrimaryParticle/I:FileNumber/I");
        // RecTree->Branch("Tags", &_WDTags, "Gain/F:BeamEnergy/F:PosX/F:PosY/F:PrimaryParticle/I:FileNumber/I");
}


void WaveDaqReconstruction::SetOutputNeutronWF(TTree* RecTree)
{
    if( !_WDChannelMap.IsNeutronMapLoaded() )
    {
        Error("SetOutputNeutronWF()", "Requested waveforms but no neutron detector found in channel map!");
        throw -1;
    }
    
    // SC timestamps
    if( _WDChannelMap.IsSCMapLoaded() ) RecTree->Branch("SC_Timestamp",&_SCTime,"SC_Timestamp/F");

    //Neutron waveforms
    _NS_WF = new NeutronWF[NEUTRONSLOWCHANNELS];
    _NF_WF = new NeutronWF[NEUTRONFASTCHANNELS];
    bool chFound = false;
    std::string detName;
    Int_t globCh;
    UShort_t board = _WDChannelMap.GetNeutronChannelMap()->GetBoardSlow();
    std::vector<Int_t>* channels = _WDChannelMap.GetNeutronChannelMap()->GetChSlow();
    for(int i=0; i<channels->size(); ++i)
    {
        chFound = _WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, channels->at(i)), &globCh);
        detName = _WDChannelMap.GetNeutronChannelMap()->GetDetFromBoardCh(std::make_pair(board, channels->at(i)));
        if(!chFound)
        {
            Error("SetOutputNeutronWF()","Requested channel for neutrons (board %hu, ch %d) not found in channel map", board, channels->at(i));
            throw -1;
        }
        RecTree->Branch(Form("%s_SLOW%d", detName.c_str(), globCh), &_NS_WF[globCh], Form("V[%d]/F:T[%d]/F:IsOn/O", WAVEFORMBINS, WAVEFORMBINS));
        chFound = false;
    }

    board = _WDChannelMap.GetNeutronChannelMap()->GetBoardFast();
    channels = _WDChannelMap.GetNeutronChannelMap()->GetChFast();
    for(int i=0; i<channels->size(); ++i)
    {
        chFound = _WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, channels->at(i)), &globCh);
        detName = _WDChannelMap.GetNeutronChannelMap()->GetDetFromBoardCh(std::make_pair(board, channels->at(i)));
        if(!chFound)
        {
            Error("SetOutputNeutronWF()","Requested channel for neutrons (board %hu, ch %d) not found in channel map", board, channels->at(i));
            throw -1;
        }
        RecTree->Branch(Form("%s_FAST%d", detName.c_str(), globCh), &_NF_WF[globCh], Form("V[%d]/F:T[%d]/F:IsOn/O", WAVEFORMBINS, WAVEFORMBINS));
        chFound = false;
    }

    //Trigger and tags
    RecTree->Branch("TriggerType",&_TriggerType,"TriggerType/I");
    RecTree->Branch("IsFragTriggerOn", &_IsFragTriggerOn, "IsFragTriggerOn/O");
    RecTree->Branch("EventNumber",&_Event,"EventNumber/I");
    if(_IsTDAQ)
        RecTree->Branch("Tags", &_TDAQTags, "RunNumber/I:FileNumber/I");
    else
        RecTree->Branch("Tags", &_WDTags, "BeamEnergy/F:PrimaryParticle/I:FileNumber/I");
        // RecTree->Branch("Tags", &_WDTags, "Gain/F:BeamEnergy/F:PosX/F:PosY/F:PrimaryParticle/I");
}


void WaveDaqReconstruction::GetFileTags(std::string FileName)
{
    //Separate the file name from the path
    std::string pathtofile = FileName.c_str();
    Int_t index = pathtofile.find_last_of("/\\");
    std::string filename = pathtofile.substr(index+1);

    std::string tag, temp;
    
    if(_IsTDAQ)
    {
        Int_t i=0;
        while (filename[i] != '.')
            i++;
        i+=1;
        while(filename[i] != '.')
        {
            if( isdigit(filename[i]) )
                temp+=filename[i];
            i++;
        }
        _TDAQTags.RunNumber = std::atoi(temp.c_str());
        temp.clear();

        i = filename.size()-1;
        while(filename[i] != '_')
            i--;
        while(isdigit(filename[i+1]) && filename[i+1] != '.')
        {
            temp += filename[i+1];
            i++;
        }
        _TDAQTags.FileNumber = std::atoi(temp.c_str());
        temp.clear();
    }
    else
    {
        // //Get primary particle type
        // switch(filename[0])
        // {
        //  case 'P': _WDTags.PrimaryParticle = Proton; break;
        //  case 'H': _WDTags.PrimaryParticle = Helium; break;
        //  case 'C': _WDTags.PrimaryParticle = Carbon; break;
        //  case 'O': _WDTags.PrimaryParticle = Oxygen; break;
        //  default: _WDTags.PrimaryParticle = None; break;
        // }

        // Float_t value;
        // //skip first char if it indicates the particle name
        // for(Int_t i = 1; i < filename.size(); ++i)
        // {
        //  //Get tag and value
        //  if(filename[i]=='_')
        //  {
        //      tag.clear();
        //      temp.clear();
        //      i++;
        //      while(isalpha(filename[i])){
        //          tag += filename[i];
        //          i++;
        //      }
        //      while(filename[i] != '_' && !(filename[i] == '.' && isalpha(filename[i+1])))
        //      {
        //          temp += filename[i];
        //          i++;
        //      }
        //      value = std::atof(temp.c_str());
        //  }
        //  //Register values
        //  if(tag == 'E'){_WDTags.BeamEnergy = value;}
        //  else if(tag == 'G'){_WDTags.Gain = value;}
        //  else if(tag == 'X'){_WDTags.BeamPositionX = value;}
        //  else if(tag == 'Y'){_WDTags.BeamPositionY = value;}
        // }
        for(int i=0; i<filename.size(); ++i)
        {
            if( isdigit(filename[i]) )  temp += filename[i];
        }
        _WDTags.FileNumber = std::atoi(temp.c_str());
    }
}


/**************** TOF-WALL WAVEFORM LEVEL ANALYSIS **************************/

void WaveDaqReconstruction::AnalyzeWaveformsTW(UShort_t board)
{
    //set a boolean variable to flag the 2 clocks of the board
    Bool_t CLK_done[2] = {false, false};
    Int_t boardindex = _BoardIdToIdMap[board];

    for (Int_t channel=0;channel<NUMBEROFCHANNELS-2;++channel)
    {
        // if the waveform is empty skip the analysis
        if(_WaveFormContainer[boardindex]->IsEmpty(channel))    continue;

        //get the global channel
        std::pair<UShort_t, Int_t> BC_pair = std::make_pair(board, channel);
        Int_t globalch = _WDChannelMap.GetTWChannelMap()->GetGlobalFromBoardChannelPair(BC_pair);

        //Calculate the quantities of interest
        std::pair<Float_t, Float_t> PedPair = _WaveFormContainer[boardindex]->GetPedestal(channel);
        _CPedestal[globalch] = PedPair.first;
        _CPedestalRMS[globalch] = PedPair.second;
        _CAmplitude[globalch] = _WaveFormContainer[boardindex]->GetAmplitude(channel);
        _CCharge[globalch] = _WaveFormContainer[boardindex]->GetCharge(channel);
        _CRiseTime[globalch] = _WaveFormContainer[boardindex]->GetRiseTime(channel);

        if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
            _CTimestamps[globalch] = _WaveFormContainer[boardindex]->GetTimeLinear(channel, board, _Event, fout, "TW");
        else
            _CTimestamps[globalch] = _WaveFormContainer[boardindex]->GetTimeLinear(channel);


        /*Analyze the clock if not done yet
        * The reason for the indexing is the mapping of clocks:
        * CLK ch 16 ----> ch 0->7
        * CLK ch 17 ----> ch 8->15
        */
        if(!CLK_done[channel/8])
        {
            if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
            {
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8, board, _Event, fout);
            }
            else
            {
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8);
            }
            CLK_done[channel/8] = true;
        }

        EvalCLKJitter(boardindex, globalch, channel);
        _CTimestampsCorrJit[globalch] = _CTimestamps[globalch] - _CLK_Jitter[globalch];

        Int_t BarId = _GlobalToBarChIDpairMap[globalch].first;

        //save data in A-B variables
        if(_GlobalToBarChIDpairMap[globalch].second=='A')
        {
            _CPedA[BarId] = _CPedestal[globalch];
            _CPedRMSA[BarId] = _CPedestalRMS[globalch];
            _CAmpA[BarId] = _CAmplitude[globalch];
            _CChargeA[BarId] = _CCharge[globalch];
            _CTimeA[BarId] = _CTimestampsCorrJit[globalch];
            _CRiseTimeA[BarId] = _CRiseTime[globalch];
        }
        else if(_GlobalToBarChIDpairMap[globalch].second=='B')
        {
            _CPedB[BarId] = _CPedestal[globalch];
            _CPedRMSB[BarId] = _CPedestalRMS[globalch];
            _CAmpB[BarId] = _CAmplitude[globalch];
            _CChargeB[BarId] = _CCharge[globalch];
            _CTimeB[BarId] = _CTimestampsCorrJit[globalch];
            _CRiseTimeB[BarId] = _CRiseTime[globalch];
        }
        else
        {
            Error("AnalyzeWaveformsTW()", "Channel ID error: neither A nor B label found! Board %d, ch %d, globalch %d", board, channel, globalch);
            throw -1;
        }
    }
}


void WaveDaqReconstruction::EvalCLKJitter(Int_t boardindex, Int_t globalch, Int_t channel)
{
    _CLK_Jitter[globalch] = _CLK_phase[boardindex][channel/8] - _SC_CLK_phase;
}


/************************** SC WAVEFORM LEVEL ANALYSIS ****************************/

void WaveDaqReconstruction::AnalyzeWaveformsSC(UShort_t board)
{
    _SCTime = 0;
    _SC_CLK_phase = 0;
    Int_t boardindex = _BoardIdToIdMap[board];
    std::vector<Int_t> SCChannels = _WDChannelMap.GetSCChannelMap()->GetSCChannels();


    if(_Debug &&  _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
    {
        _SCTime = _WaveFormContainer[boardindex]->GetTimeSC(&SCChannels, board, _Event, fout);
        _SC_CLK_phase = _WaveFormContainer[boardindex]->GetCLKPhase(16, board, _Event, fout);
    }
    else
    {
        _SCTime = _WaveFormContainer[boardindex]->GetTimeSC(&SCChannels);
        _SC_CLK_phase = _WaveFormContainer[boardindex]->GetCLKPhase(16);
    }

    if(_Debug)
    {
        for(std::vector<Int_t>::iterator itCh = SCChannels.begin(); itCh != SCChannels.end(); ++itCh)
        {
            std::pair<Float_t, Float_t> PedPair = _WaveFormContainer[boardindex]->GetPedestal(*itCh);
            _SCPedestal[*itCh] = PedPair.first;
            _SCPedestalRMS[*itCh] = PedPair.second;
            _SCAmplitude[*itCh] = _WaveFormContainer[boardindex]->GetAmplitude(*itCh);
            _SCCharge[*itCh] = _WaveFormContainer[boardindex]->GetCharge(*itCh);
            _SCRiseTime[*itCh] = _WaveFormContainer[boardindex]->GetRiseTime(*itCh);

        }
    }
}


/************************** CALO WAVEFORM LEVEL ANALYSIS ****************************/

void WaveDaqReconstruction::AnalyzeWaveformsCALO(UShort_t board)
{
    //set a boolean variable to flag the 2 clocks of the board
    Bool_t CLK_done[2] = {false, false};
    Int_t boardindex = _BoardIdToIdMap[board];

    for (Int_t channel=0; channel<NUMBEROFCHANNELS-2; ++channel)
    {
        // if the waveform is empty or the CALO crystal is not found in the channel map skip the analysis
        Int_t CrystalId;
        if(_WaveFormContainer[boardindex]->IsEmpty(channel) || !_WDChannelMap.GetCALOChannelMap()->GetCrystalId(board, channel, &CrystalId))
            continue;

        //Calculate the quantities of interest
        std::pair<Float_t, Float_t> PedPair;
        PedPair = _WaveFormContainer[boardindex]->GetPedestal(channel);
        _CALOPedestal[CrystalId] = PedPair.first;
        _CALOPedestalRMS[CrystalId] = PedPair.second;
        _CALOAmplitude[CrystalId] = _WaveFormContainer[boardindex]->GetAmplitude(channel);
        _CALOCharge[CrystalId] = _WaveFormContainer[boardindex]->GetChargeCALO(channel);
        _CALORiseTime[CrystalId] = _WaveFormContainer[boardindex]->GetRiseTime(channel);

        if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
            _CALOTimestamps[CrystalId] = _WaveFormContainer[boardindex]->GetTimeCFD(channel, board, _Event, fout, "CALO");
        else
            _CALOTimestamps[CrystalId] = _WaveFormContainer[boardindex]->GetTimeCFD(channel);

        /*Analyze the clock if not done yet
        * The reason for the indexing is the mapping of clocks:
        * CLK ch 16 ----> ch 0->7
        * CLK ch 17 ----> ch 8->15
        */
        if(!CLK_done[channel/8])
        {
            if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8, board, _Event, fout);

            else
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8);

            CLK_done[channel/8] = true;
        }

        _CALOTimestampsCorrJit[CrystalId] = _CALOTimestamps[CrystalId] - (_CLK_phase[boardindex][channel/8] - _SC_CLK_phase);
    }
}

/**************************** NEUTRON CHANNELS ANALYSIS ****************************/

void WaveDaqReconstruction::AnalyzeWaveformsNeutrons(UShort_t board)
{
    //set a boolean variable to flag the 2 clocks of the board
    Bool_t CLK_done[2] = {false, false};
    Int_t boardindex = _BoardIdToIdMap[board];
    std::pair<Float_t, Float_t> PedPair;
    Float_t Amp, Charge, Time, RiseTime;

    for (Int_t channel=0; channel<NUMBEROFCHANNELS-2; ++channel)
    {
        // if the waveform is empty or the CALO crystal is not found in the channel map skip the analysis
        Int_t GlobalCh;
        if(_WaveFormContainer[boardindex]->IsEmpty(channel) || !_WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, channel), &GlobalCh))
            continue;

        //Calculate the quantities of interest
        PedPair = _WaveFormContainer[boardindex]->GetPedestal(channel);
        Amp = _WaveFormContainer[boardindex]->GetAmplitude(channel);
        Charge = _WaveFormContainer[boardindex]->GetChargeCALO(channel);
        RiseTime = _WaveFormContainer[boardindex]->GetRiseTime(channel);

        if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
            Time = _WaveFormContainer[boardindex]->GetTimeCFD(channel, board, _Event, fout, "CALO");
        else
            Time = _WaveFormContainer[boardindex]->GetTimeCFD(channel);

        /*Analyze the clock if not done yet
        * The reason for the indexing is the mapping of clocks:
        * CLK ch 16 ----> ch 0->7
        * CLK ch 17 ----> ch 8->15
        */
        if(!CLK_done[channel/8])
        {
            if(_Debug && _Event <= _LastEventToSave && _Event >= _FirstEventToSave)
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8, board, _Event, fout);

            else
                _CLK_phase[boardindex][channel/8] = _WaveFormContainer[boardindex]->GetCLKPhase(16 + channel/8);

            CLK_done[channel/8] = true;
        }

        Time = Time - (_CLK_phase[boardindex][channel/8] - _SC_CLK_phase);

        if( board == _WDChannelMap.GetNeutronChannelMap()->GetBoardSlow() )
        {
            _NSPed[GlobalCh] = PedPair.first;
            _NSPedRMS[GlobalCh] = PedPair.second;
            _NSAmp[GlobalCh] = Amp;
            _NSCharge[GlobalCh] = Charge;
            _NSRiseTime[GlobalCh] = RiseTime;
            _NSTime[GlobalCh] = Time;
        }
        else if( board == _WDChannelMap.GetNeutronChannelMap()->GetBoardFast() )
        {
            _NFPed[GlobalCh] = PedPair.first;
            _NFPedRMS[GlobalCh] = PedPair.second;
            _NFAmp[GlobalCh] = Amp;
            _NFCharge[GlobalCh] = Charge;
            _NFRiseTime[GlobalCh] = RiseTime;
            _NFTime[GlobalCh] = Time;
        }
        else
        {
            Error("AnalyzeWaveformsNeutrons()", "Unexpected board (%hu) found in Neutron analysis!", board);
            throw -1;
        }
    }
}

void WaveDaqReconstruction::FillNeutronWaveforms(UShort_t board)
{
    NeutronWF* nWF = (board == _NbSlow) ? _NS_WF : _NF_WF;
    Int_t boardindex = _BoardIdToIdMap[board];
    Int_t globCh;
    for(Int_t i = 0; i<NUMBEROFCHANNELS-2; ++i)
    {
        if( !_WDChannelMap.GetNeutronChannelMap()->GetGlobFromBoardCh(std::make_pair(board, i), &globCh) )
            continue;
        else
        {
            _WaveFormContainer[boardindex]->CopyWaveform(&nWF[globCh], i);
            if( nWF[globCh].IsOn )  _NeutronOn = true;
        }
    }
}


/**************************** BAR LEVEL ANALYSIS **********************************/

void WaveDaqReconstruction::AnalyzeSingleBarEvent(Int_t BarId)
{
    /*Calculate the other quantities only if timestamps A/B != 0, i.e. only
    * if both channels of the bar were on. All the quantities remain 0
    * otherwise
    */
    if(_CTimeA[BarId] != 0 && _CTimeB[BarId] != 0)
    {
        _BCharge[BarId] = GetEventRawEnergy(BarId);
        _BTimestamps[BarId] = GetEventRawTimestamp(BarId);
        _BDeltaT[BarId] = GetDeltaT(BarId);
        _BCratio[BarId] = GetCRatio(BarId);

        // TOF data
        if( _WDChannelMap.IsSCMapLoaded() )
            _TOF[BarId] = TimeOfFlight(BarId);
    }
}

Float_t WaveDaqReconstruction::GetEventRawTimestamp(Int_t BarId)
{
    return (_CTimeA[BarId] + _CTimeB[BarId])/2;
}

Float_t WaveDaqReconstruction::GetEventRawEnergy(Int_t BarId)
{
    return TMath::Sqrt(_CChargeA[BarId]*_CChargeB[BarId]);
}

Float_t WaveDaqReconstruction::GetDeltaT(Int_t BarId)
{
    return _CTimeA[BarId] -_CTimeB[BarId];
}

Float_t WaveDaqReconstruction::GetCRatio(Int_t BarId)
{
    return TMath::Log(_CChargeA[BarId]/_CChargeB[BarId]);
}

Float_t WaveDaqReconstruction::TimeOfFlight(Int_t BarId)
{
    return _BTimestamps[BarId] - _SCTime;
}


/****************************** FRAG-TRIGGER EFFICIENCY *************************************/

void WaveDaqReconstruction::LoadTriggerCalibration(std::string FileName)
{
    Int_t channelId;
    Float_t a, b, TrigTh;
    std::pair<Float_t, Float_t> TrigPar;
    Char_t line[100];
    FILE* fCal = fopen(FileName.c_str(), "r");
    while(fgets(line, sizeof(line), fCal))
    {
        if(line[0] == '\n' || line[0] == '#'){continue;}
        sscanf(line, "%d %f %*f %f %*f %f", &channelId, &a, &b, &TrigTh);
        TrigPar = std::make_pair(a, b);
        _TrigCalMap[channelId] = TrigPar;
        _TriggerTh[channelId] = TrigTh;
    }
    fclose(fCal);
    
    _TriggerEnable = true;
    EnableHistograms();
}


void WaveDaqReconstruction::CheckFragTriggerConditions()
{
    Bool_t VetoOff = false, MargMaj = false;
    Int_t boardindex;

    //Check margarita majority
    if( _WDChannelMap.IsSCMapLoaded() && _BoardIdToIdMap.find(_WDChannelMap.GetSCChannelMap()->GetSCBoard()) != _BoardIdToIdMap.end() )
    {
        boardindex = _BoardIdToIdMap[_WDChannelMap.GetSCChannelMap()->GetSCBoard()];
        Int_t count = 0;
        for(Int_t chId=0; chId < NUMBEROFSCCHANNELS; ++chId)
        {
            if( !_WaveFormContainer[boardindex]->IsEmpty(chId) )
            {
                count++;
                if( count > 3 )
                {
                    MargMaj = true;
                    break;
                }
            }
        }
    }

    //Check TW veto
    if( _WDChannelMap.IsTWMapLoaded() )
    {
        Float_t TrigAmp;
        boardindex = _BoardIdToIdMap[FRAGTRIGGERBOARD];
        for(Int_t chId=0; chId<NUMBEROFTRIGGERCHANNELS; ++chId)
        {
            if( _WaveFormContainer[boardindex]->IsEmpty(chId) )
                TrigAmp=0;
            else
                TrigAmp = _TrigCalMap[chId].first*fabs(_WaveFormContainer[boardindex]->GetAmplitude(chId)) + _TrigCalMap[chId].second;

            if( !VetoOff && TrigAmp < _TriggerTh[chId] )
                VetoOff = true;

            _hTrigAmp[chId]->Fill(TrigAmp);
        }
    }
    else
        VetoOff = true;

    if( _IsFragTriggerOn )
    {
        if(MargMaj && VetoOff) _TrigTP++;
        else _TrigFP++;
    }
    else
    {
        if(MargMaj && VetoOff) _TrigFN++;
        else _TrigTN++;
    }
}

void WaveDaqReconstruction::PrintTriggerEfficiency()
{
        Int_t TrigTot = _TrigFP + _TrigFN + _TrigTP + _TrigTN;
        std::cout << "Fragmentation trigger efficiency\n";
        std::cout << "True positive:\t" << _TrigTP << "\t" << (float)_TrigTP*100/TrigTot << "%\n";
        std::cout << "False positive:\t" << _TrigFP << "\t" << (float)_TrigFP*100/TrigTot << "%\n";
        std::cout << "True negative:\t" << _TrigTN << "\t" << (float)_TrigTN*100/TrigTot << "%\n";
        std::cout << "False negative:\t" << _TrigFN << "\t" << (float)_TrigFN*100/TrigTot << "%\n";
        std::cout << "Efficiency:\t" << (float)(_TrigTP+_TrigTN)*100/TrigTot << "%\n";
}


/************************************* HISTOGRAMS SETTING *************************************/

void WaveDaqReconstruction::CreateHistograms()
{
    if( _WDChannelMap.IsTWMapLoaded() )
    {
        _hitmap_Bars = new TH1F("hitmapBars", "Hitmap Bars", 40, -0.5, 39.5);
        _hitmap_Bars->SetFillColor(kBlue);
        _hitmap_Bars->SetStats(0);
        _hitmap_Bars->SetDirectory( fout->GetDirectory("Histos") );

        _hitmap_Channels_Rear = new TH1F("hitmapChRear", "Hitmap Channel Rear Layer", 40, -0.5, 39.5);
        _hitmap_Channels_Rear->SetStats(0);
        _hitmap_Channels_Rear->SetFillColor(kBlue);
        _hitmap_Channels_Rear->SetDirectory( fout->GetDirectory("Histos") );

        _hitmap_Channels_Front = new TH1F("hitmapChFront", "Hitmap Channel Front Layer", 40, 39.5, 79.5);
        _hitmap_Channels_Front->SetStats(0);
        _hitmap_Channels_Front->SetFillColor(kBlue);
        _hitmap_Channels_Front->SetDirectory( fout->GetDirectory("Histos") );

        _hitmap_MB = new TH2F("hitmap_MB", "Hitmap_MB", 20, -0.5, 19.5, 20, 19.5, 39.5);
        _hitmap_MB->SetStats(0);
        _hitmap_MB->SetOption("text colz");
        _hitmap_MB->SetDirectory( fout->GetDirectory("Histos") );

        _hitmap_frag = new TH2F("hitmap_frag", "Hitmap_frag", 20, -0.5, 19.5, 20, 19.5, 39.5);
        _hitmap_frag->SetStats(0);
        _hitmap_frag->SetOption("text colz");
        _hitmap_frag->SetDirectory( fout->GetDirectory("Histos") );

        _hitmap_all = new TH2F("hitmap_all", "Hitmap_all", 20, -0.5, 19.5, 20, 19.5, 39.5);
        _hitmap_all->SetStats(0);
        _hitmap_all->SetOption("text colz");
        _hitmap_all->SetDirectory( fout->GetDirectory("Histos") );
    }

    if( _WDChannelMap.IsCALOMapLoaded() )
    {
        _hCALOMultiplicity = new TH1I("CALO_Multiplicity", "CALO_Multiplicity", 11, -0.5, 10.5);
        _hCALOMultiplicity->SetDirectory( fout->GetDirectory("Histos") );
    }

    //hTGEN is filled by the ReadBinary class so it doesn't need to use FillHistograms()
    _hTGEN_MB = new TH2F("hTGEN_MB", "Trigger Generation MB;CLK Tick;Algorithm Id", 34, -1.5, 32.5, 16, -1.5, 14.5);
    _hTGEN_MB->SetStats(11111111);
    _hTGEN_MB->SetOption("text colz");
    _hTGEN_MB->SetDirectory( fout->GetDirectory("Histos") );

    _hTGEN_frag = new TH2F("hTGEN_frag", "Trigger Generation frag;CLK Tick;Algorithm Id", 34, -1.5, 32.5, 16, -1.5, 14.5);
    _hTGEN_frag->SetStats(11111111);
    _hTGEN_frag->SetOption("text colz");
    _hTGEN_frag->SetDirectory( fout->GetDirectory("Histos") );

    _hTriggerPattern = new TH1I("hTriggerPattern", "Trigger Pattern;Trigger Id;Entries", 66, -1.5, 64.5);
    _hTriggerPattern->SetStats(0);
    _hTriggerPattern->SetDirectory( fout->GetDirectory("Histos") );

    _hTriggerRates = new TH1I("hTriggerRates", "Trigger Rates;Trigger Id;Trigger rate [Hz]", 66, -1.5, 64.5);
    _hTriggerRates->SetStats(0);
    _hTriggerRates->SetDirectory( fout->GetDirectory("Histos") );

    if( _TriggerEnable )
    {
        for(int i = 0; i<NUMBEROFTRIGGERCHANNELS; ++i)
        {
            _hTrigAmp[i] = new TH1F(Form("hTrigAmp_%d",i), Form("hTrigAmp_%d;TrigAmp [V];Entries",i), 200, -0.2, 1.1);
            _hTrigAmp[i]->SetStats(11111111);
            _hTrigAmp[i]->SetDirectory( fout->GetDirectory("Histos") );
        }
    }
}


void WaveDaqReconstruction::FillHistograms()
{
    if( _WDChannelMap.IsTWMapLoaded() )
    {
        for(Int_t BarId = 0; BarId < NUMBEROFTWBARS; ++BarId)
        {
            if (_BCharge[BarId] == 0) continue;
            _hitmap_Bars->Fill(BarId);
        }

        for (Int_t ChannelId = 0; ChannelId < NUMBEROFGLOBALCHANNELSTW; ++ChannelId)
        {
            if (_CCharge[ChannelId] == 0) continue;
            else if (ChannelId < 40) _hitmap_Channels_Rear->Fill(ChannelId);
            else _hitmap_Channels_Front->Fill(ChannelId);
        }

        for (Int_t i = LAYERYBARMIN; i <= LAYERYBARMAX; i++)
        {
            if (_BCharge[i] == 0) continue;
            for (Int_t j = LAYERXBARMIN; j <= LAYERXBARMAX; j++)
            {
                if(_BCharge[j] == 0) continue;
                
                if(_IsFragTriggerOn)    _hitmap_frag->Fill(i, j);
                else    _hitmap_MB->Fill(i, j);

                _hitmap_all->Fill(i, j);
            }
        }
    }

    if( _WDChannelMap.IsCALOMapLoaded() )
    {
        int countCALO = 0;
        for(int i=0; i<=NUMBEROFCRYSTALS; ++i)
        {
            if(_CALOCharge[i] != 0) countCALO++;
        }
        _hCALOMultiplicity->Fill(countCALO);
    }
}


/*********************************** INPUT/OUTPUT SETTING ***********************************/

void WaveDaqReconstruction::LoadChannelMap(std::string FileName)
{
    if( !_WDChannelMap.LoadMap(FileName) )
    {
        Error("LoadChannelMap()", "Error while loading channel map!");
        throw -1;
    }

    _GlobalToBarChIDpairMap = _WDChannelMap.GetTWChannelMap()->GetGlobalToBarChIDpairMap();
}


void WaveDaqReconstruction::CheckLoadedBoards()
{
    for (auto it = _BoardIdToIdMap.begin(); it!=_BoardIdToIdMap.end(); ++it)
    {
        std::string detector;
        if( _WDChannelMap.IsSCMapLoaded() && it->first == _WDChannelMap.GetSCChannelMap()->GetSCBoard())
            detector = "SC";
        else if(_WDChannelMap.GetTWChannelMap()->IsBoardLoaded(it->first))
            detector = "TW";
        else if(_WDChannelMap.GetCALOChannelMap()->IsBoardLoaded(it->first))
            detector = "CALO";
        else if(_WDChannelMap.GetNeutronChannelMap()->IsBoardLoaded(it->first))
            detector = "NEUTRON";
        else
        {
            // Warning("CheckLoadedBoards()", "Found board %hu in data not included in the Channel Map!!", it->first);
            continue;
        }
        Message::DisplayMessageWithEmphasys(TString::Format("%s Board %hu found => Id %d ", detector.c_str(), it->first, it->second));
    }
}


void WaveDaqReconstruction::EnableHistograms() {_EnableHisto = true;}


void WaveDaqReconstruction::SetTDAQfile() {_IsTDAQ = true;}


void WaveDaqReconstruction::SetSaveNeutrons() { _SaveNeutrons = true; }


void WaveDaqReconstruction::SetOutputFileName(std::string FileName)
{
    this->OutputFileName=FileName;
}


void WaveDaqReconstruction::SetGain(Float_t Gain){_Gain=Gain;}
```


-------------------------------

Updated on 2021-12-29 at 15:21:51 +0000
