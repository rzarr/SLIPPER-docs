---
title: WaveDaqDisplay
summary: Class that handles the creation and display of the plots for SC, TW and CALO in the EventDisplay executable. 

---

# WaveDaqDisplay



Class that handles the creation and display of the plots for SC, TW and CALO in the EventDisplay executable. 

Inherits from [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[WaveDaqDisplay](/Classes/classWaveDaqDisplay.md#function-wavedaqdisplay)**()<br>Default constructor.  |
| virtual | **[~WaveDaqDisplay](/Classes/classWaveDaqDisplay.md#function-~wavedaqdisplay)**()<br>Default destructor.  |
| virtual void | **[CheckLoadedBoards](/Classes/classWaveDaqDisplay.md#function-checkloadedboards)**()<br>Check and print all the loaded WaveDREAM boars.  |
| void | **[EnableHistograms](/Classes/classWaveDaqDisplay.md#function-enablehistograms)**()<br>Enable histogram writing in the output.  |
| void | **[LoadChannelMap](/Classes/classWaveDaqDisplay.md#function-loadchannelmap)**(std::string FileName)<br>Load xml containing the channel map, i.e. the mapping between channels,boards and bar.  |
| void | **[LoadTriggerCalibration](/Classes/classWaveDaqDisplay.md#function-loadtriggercalibration)**(std::string FileName)<br>Load the trigger calibration map.  |
| virtual void | **[RunReconstruction](/Classes/classWaveDaqDisplay.md#function-runreconstruction)**(std::string FileName, std::string TimeCalFileName, int nEv)<br>Perform the reconstruction.  |
| void | **[SetDebugMode](/Classes/classWaveDaqDisplay.md#function-setdebugmode)**(Int_t first_ev, Int_t last_ev)<br>Activate debug mode if requested and set event range.  |
| void | **[SetGain](/Classes/classWaveDaqDisplay.md#function-setgain)**(Float_t Gain)<br>Set the frontend gain.  |
| void | **[SetIncludeCLKs](/Classes/classWaveDaqDisplay.md#function-setincludeclks)**()<br>Set the flag for CLK signal display.  |
| void | **[SetOutputFileName](/Classes/classWaveDaqDisplay.md#function-setoutputfilename)**(const std::string & FileName)<br>Set the output file name.  |
| void | **[SetSaveBeamRate](/Classes/classWaveDaqDisplay.md#function-setsavebeamrate)**()<br>Enable the saving of beam rate in an output txt file for online monitoring.  |
| void | **[SetSaveNeutrons](/Classes/classWaveDaqDisplay.md#function-setsaveneutrons)**()<br>Set the SaveNeutrons flag to true.  |
| void | **[SetTDAQfile](/Classes/classWaveDaqDisplay.md#function-settdaqfile)**()<br>Signal that the file is produced through the TDAQ.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddCALOPlots](/Classes/classWaveDaqDisplay.md#function-addcaloplots)**(UShort_t board)<br>Add the waveform plots of the CALO.  |
| void | **[AddPlots](/Classes/classWaveDaqDisplay.md#function-addplots)**()<br>Add the waveform plots to each detector.  |
| void | **[AddSCPlots](/Classes/classWaveDaqDisplay.md#function-addscplots)**(UShort_t board)<br>Add the waveform plots of the SC.  |
| void | **[AddTWPlots](/Classes/classWaveDaqDisplay.md#function-addtwplots)**(UShort_t board)<br>Add the waveform plots of the TW.  |
| void | **[AnalyzeSingleBarEvent](/Classes/classWaveDaqDisplay.md#function-analyzesinglebarevent)**(Int_t BarId)<br>Compute the information at the bar level.  |
| void | **[AnalyzeWaveformsCALO](/Classes/classWaveDaqDisplay.md#function-analyzewaveformscalo)**(UShort_t board)<br>Analysis of CALO Waveforms (WFs)  |
| void | **[AnalyzeWaveformsNeutrons](/Classes/classWaveDaqDisplay.md#function-analyzewaveformsneutrons)**(UShort_t board)<br>Analysis of Neutron detector WFs.  |
| void | **[AnalyzeWaveformsRC](/Classes/classWaveDaqDisplay.md#function-analyzewaveformsrc)**(UShort_t board)<br>Analysis of RC Waveforms (WFs)  |
| void | **[AnalyzeWaveformsSC](/Classes/classWaveDaqDisplay.md#function-analyzewaveformssc)**(UShort_t board)<br>Analysis of SC Waveforms (WFs)  |
| void | **[AnalyzeWaveformsTW](/Classes/classWaveDaqDisplay.md#function-analyzewaveformstw)**(UShort_t board)<br>Analyze the WFs of TW.  |
| void | **[CheckFragTriggerConditions](/Classes/classWaveDaqDisplay.md#function-checkfragtriggerconditions)**()<br>Check if the fragmentation trigger conditions are satisfied.  |
| void | **[ClearPlots](/Classes/classWaveDaqDisplay.md#function-clearplots)**()<br>Clear all the plots for the next event.  |
| void | **[ClearWFdata](/Classes/classWaveDaqDisplay.md#function-clearwfdata)**()<br>Clear all the Waveforms.  |
| Float_t | **[CLKAnalysis](/Classes/classWaveDaqDisplay.md#function-clkanalysis)**(int boardindex, int channel) |
| void | **[CreateHistograms](/Classes/classWaveDaqDisplay.md#function-createhistograms)**()<br>Booking of the histograms.  |
| void | **[DisplayWaveForms](/Classes/classWaveDaqDisplay.md#function-displaywaveforms)**()<br>Display all the waveforms in their dedicated canvas.  |
| void | **[EvalCLKJitter](/Classes/classWaveDaqDisplay.md#function-evalclkjitter)**(int boardindex, Int_t globalch, int channel)<br>Calculate the clock phase jitter between TW and SC.  |
| void | **[FillHistograms](/Classes/classWaveDaqDisplay.md#function-fillhistograms)**()<br>Fill the histograms.  |
| void | **[FillNeutronWaveforms](/Classes/classWaveDaqDisplay.md#function-fillneutronwaveforms)**(UShort_t board)<br>Fill the output objects with neutron waveforms.  |
| Float_t | **[GetCRatio](/Classes/classWaveDaqDisplay.md#function-getcratio)**(Int_t BarId)<br>Charge logarithmic ratio.  |
| Float_t | **[GetDeltaT](/Classes/classWaveDaqDisplay.md#function-getdeltat)**(Int_t BarId)<br>Time difference between the two channels.  |
| Float_t | **[GetEventRawEnergy](/Classes/classWaveDaqDisplay.md#function-geteventrawenergy)**(Int_t BarId)<br>Raw energy of the event: geometric mean of the A-B charges.  |
| Float_t | **[GetEventRawTimestamp](/Classes/classWaveDaqDisplay.md#function-geteventrawtimestamp)**(Int_t BarId)<br>Bar timestamp of the event: mean of the channels' timestamps.  |
| void | **[GetFileTags](/Classes/classWaveDaqDisplay.md#function-getfiletags)**(std::string FileName)<br>Get the file tags.  |
| void | **[LoopEvent](/Classes/classWaveDaqDisplay.md#function-loopevent)**(TTree * RecTree)<br>Main event loop.  |
| void | **[PlotAll](/Classes/classWaveDaqDisplay.md#function-plotall)**()<br>Plot all the waveforms in their canvas.  |
| void | **[PrintTriggerEfficiency](/Classes/classWaveDaqDisplay.md#function-printtriggerefficiency)**()<br>Print the fragmentation trigger efficiency.  |
| void | **[SavePlots](/Classes/classWaveDaqDisplay.md#function-saveplots)**()<br>Save the plots to a file for the current event.  |
| void | **[SetOutputDataToZero](/Classes/classWaveDaqDisplay.md#function-setoutputdatatozero)**()<br>Function called at the beginning of each event to reset the output data.  |
| void | **[SetOutputNeutronWF](/Classes/classWaveDaqDisplay.md#function-setoutputneutronwf)**(TTree * RecTree)<br>Set the output for neutron waveforms.  |
| void | **[SetOutputTreeBranches](/Classes/classWaveDaqDisplay.md#function-setoutputtreebranches)**(TTree * RecTree)<br>Booking of the output tree branches.  |
| Float_t | **[TimeOfFlight](/Classes/classWaveDaqDisplay.md#function-timeofflight)**(Int_t BarId)<br>Uncorrected TOF of the event in ns.  |
| void | **[WaitForNextEventSignal](/Classes/classWaveDaqDisplay.md#function-waitfornexteventsignal)**()<br>Create the input dialog window and wait for a command.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< UShort_t, Int_t > | **[_ActiveBoards](/Classes/classWaveDaqDisplay.md#variable--activeboards)** <br>Subset of the _BoardIdtoIdMap containing only the boards w/ at least one active channel; This variable is updated at each event.  |
| Float_t | **[_BCharge](/Classes/classWaveDaqDisplay.md#variable--bcharge)** <br>TW bar charge (raw energy loss) [V*ns].  |
| Float_t | **[_BCratio](/Classes/classWaveDaqDisplay.md#variable--bcratio)** <br>TW bar logarithmic ratio of charge "A" over charge "B" [ns].  |
| Float_t | **[_BDeltaT](/Classes/classWaveDaqDisplay.md#variable--bdeltat)** <br>TW bar raw time difference between channels "A" and "B" [ns].  |
| Float_t | **[_BeamRate](/Classes/classWaveDaqDisplay.md#variable--beamrate)** <br>Beam Rate calculated as rate of minimum bia triggers [Hz].  |
| [ReadBinary](/Classes/classReadBinary.md) * | **[_BinaryReader](/Classes/classWaveDaqDisplay.md#variable--binaryreader)** <br>Pointer to binary reader object.  |
| std::map< UShort_t,Int_t > | **[_BoardIdToIdMap](/Classes/classWaveDaqDisplay.md#variable--boardidtoidmap)** <br>Map that links the WaveDREAM board serial number to its index in the [WaveFormContainer](/Classes/classWaveFormContainer.md) vector.  |
| Float_t | **[_BTimestamps](/Classes/classWaveDaqDisplay.md#variable--btimestamps)** <br>TW bar raw time [ns].  |
| Float_t | **[_CALOAmplitude](/Classes/classWaveDaqDisplay.md#variable--caloamplitude)** <br>CALO crystal amplitude (<0) [V].  |
| Float_t | **[_CALOCharge](/Classes/classWaveDaqDisplay.md#variable--calocharge)** <br>CALO crystal integral charge [V*ns].  |
| Float_t | **[_CALOPedestal](/Classes/classWaveDaqDisplay.md#variable--calopedestal)** <br>CALO crystal pedestal [V].  |
| Float_t | **[_CALOPedestalRMS](/Classes/classWaveDaqDisplay.md#variable--calopedestalrms)** <br>CALO crystal pedestal RMS [V].  |
| Float_t | **[_CALORiseTime](/Classes/classWaveDaqDisplay.md#variable--calorisetime)** <br>CALO crystal rise time [ns].  |
| Float_t | **[_CALOTimestamps](/Classes/classWaveDaqDisplay.md#variable--calotimestamps)** <br>CALO crystal raw time [ns].  |
| Float_t | **[_CALOTimestampsCorrJit](/Classes/classWaveDaqDisplay.md#variable--calotimestampscorrjit)** <br>CALO crystal time with CLK jitter correction [ns].  |
| Float_t | **[_CAmpA](/Classes/classWaveDaqDisplay.md#variable--campa)** <br>TW channel "A" amplitude (<0) [V].  |
| Float_t | **[_CAmpB](/Classes/classWaveDaqDisplay.md#variable--campb)** <br>TW channel "B" amplitude (<0) [V].  |
| Float_t | **[_CAmplitude](/Classes/classWaveDaqDisplay.md#variable--camplitude)** <br>TW global channel amplitude [V] **DEBUG ONLY** |
| std::map< TString, TCanvas * > | **[_CanvasMap](/Classes/classWaveDaqDisplay.md#variable--canvasmap)** <br>Map containing all the canvas for the WaveDAQ detectors.  |
| Float_t | **[_CCharge](/Classes/classWaveDaqDisplay.md#variable--ccharge)** <br>TW global channel total charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_CChargeA](/Classes/classWaveDaqDisplay.md#variable--cchargea)** <br>TW channel "A" integral charge [V*ns].  |
| Float_t | **[_CChargeB](/Classes/classWaveDaqDisplay.md#variable--cchargeb)** <br>TW channel "B" integral charge [V*ns].  |
| Float_t | **[_CLK_Jitter](/Classes/classWaveDaqDisplay.md#variable--clk-jitter)** <br>TW global channel CLK jitter correction [ns] **DEBUG ONLY** |
| Float_t | **[_CLK_phase](/Classes/classWaveDaqDisplay.md#variable--clk-phase)** <br>CLK phase of all boards [ns] **DEBUG ONLY** |
| Float_t | **[_CPedA](/Classes/classWaveDaqDisplay.md#variable--cpeda)** <br>TW channel "A" pedestal [V].  |
| Float_t | **[_CPedB](/Classes/classWaveDaqDisplay.md#variable--cpedb)** <br>TW channel "B" pedestal [V].  |
| Float_t | **[_CPedestal](/Classes/classWaveDaqDisplay.md#variable--cpedestal)** <br>TW global channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_CPedestalRMS](/Classes/classWaveDaqDisplay.md#variable--cpedestalrms)** <br>TW global channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_CPedRMSA](/Classes/classWaveDaqDisplay.md#variable--cpedrmsa)** <br>TW channel "A" pedestal RMS [V].  |
| Float_t | **[_CPedRMSB](/Classes/classWaveDaqDisplay.md#variable--cpedrmsb)** <br>TW channel "B" pedestal RMS [V].  |
| Float_t | **[_CRiseTime](/Classes/classWaveDaqDisplay.md#variable--crisetime)** <br>TW global channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_CRiseTimeA](/Classes/classWaveDaqDisplay.md#variable--crisetimea)** <br>TW channel "A" rise time [ns].  |
| Float_t | **[_CRiseTimeB](/Classes/classWaveDaqDisplay.md#variable--crisetimeb)** <br>TW channel "B" rise time [ns].  |
| Float_t | **[_CTimeA](/Classes/classWaveDaqDisplay.md#variable--ctimea)** <br>TW channel "A" time with CLK jitter correction [ns].  |
| Float_t | **[_CTimeB](/Classes/classWaveDaqDisplay.md#variable--ctimeb)** <br>TW channel "B" time with CLK jitter correction [ns].  |
| Float_t | **[_CTimestamps](/Classes/classWaveDaqDisplay.md#variable--ctimestamps)** <br>TW global channel raw time [ns] **DEBUG ONLY** |
| Float_t | **[_CTimestampsCorrJit](/Classes/classWaveDaqDisplay.md#variable--ctimestampscorrjit)** <br>TW global channel time with CLK jitter correction [ns] **DEBUG ONLY** |
| bool | **[_Debug](/Classes/classWaveDaqDisplay.md#variable--debug)** <br>Global debug flag.  |
| bool | **[_EnableHisto](/Classes/classWaveDaqDisplay.md#variable--enablehisto)** <br>Flag for enabling histogram saving.  |
| int | **[_Event](/Classes/classWaveDaqDisplay.md#variable--event)** <br>Current event number.  |
| int | **[_FirstEventToSave](/Classes/classWaveDaqDisplay.md#variable--firsteventtosave)** <br>First event saved in Debug Mode.  |
| TFile * | **[_fOut](/Classes/classWaveDaqDisplay.md#variable--fout)** <br>Pointer to output file.  |
| std::vector< Int_t > | **[_FragTrigBars](/Classes/classWaveDaqDisplay.md#variable--fragtrigbars)** <br>List o TW bars connected to the fragmentation trigger.  |
| Float_t | **[_Gain](/Classes/classWaveDaqDisplay.md#variable--gain)** <br>Frontend Gain of the WaveDAQ system.  |
| TGlobalToBarChIDpairMap | **[_GlobalToBarChIDpairMap](/Classes/classWaveDaqDisplay.md#variable--globaltobarchidpairmap)** <br>Map linking the TW global channel to the bar and side ("A"/"B")  |
| TH1I * | **[_hCALOMultiplicity](/Classes/classWaveDaqDisplay.md#variable--hcalomultiplicity)** <br>Multiplicity of CALO crystals **HISTOGRAM** |
| std::map< Int_t, TH1F * > | **[_hFragCharge](/Classes/classWaveDaqDisplay.md#variable--hfragcharge)** <br>Charge histogram of fragmentation trigger bars with SW chosen threshold! **HISTOGRAM** |
| TH2F * | **[_hitmap_all](/Classes/classWaveDaqDisplay.md#variable--hitmap-all)** <br>2D Hitmap of TW for all events **HISTOGRAM** |
| TH1F * | **[_hitmap_Bars](/Classes/classWaveDaqDisplay.md#variable--hitmap-bars)** <br>1D Hitmap of TW bars **HISTOGRAM** |
| TH2F * | **[_hitmap_CALO](/Classes/classWaveDaqDisplay.md#variable--hitmap-calo)** <br>2D Hitmap of TW for Minimum Bias events **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Front](/Classes/classWaveDaqDisplay.md#variable--hitmap-channels-front)** <br>1D Hitmap of TW channels in front layer **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Rear](/Classes/classWaveDaqDisplay.md#variable--hitmap-channels-rear)** <br>1D Hitmap of TW channels in rear layer **HISTOGRAM** |
| TH2F * | **[_hitmap_frag](/Classes/classWaveDaqDisplay.md#variable--hitmap-frag)** <br>2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM** |
| TH2F * | **[_hitmap_fragSW](/Classes/classWaveDaqDisplay.md#variable--hitmap-fragsw)** <br>2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM** |
| TH2F * | **[_hitmap_MB](/Classes/classWaveDaqDisplay.md#variable--hitmap-mb)** <br>2D Hitmap of TW for Minimum Bias events **HISTOGRAM** |
| TH2F * | **[_hTGEN_frag](/Classes/classWaveDaqDisplay.md#variable--htgen-frag)** <br>Trigger generation (TGEN) for Fragmentation Trigger Events **HISTOGRAM** |
| TH2F * | **[_hTGEN_MB](/Classes/classWaveDaqDisplay.md#variable--htgen-mb)** <br>Trigger generation (TGEN) for Minimum Bias Events **HISTOGRAM** |
| TH1F ** | **[_hTrigAmp](/Classes/classWaveDaqDisplay.md#variable--htrigamp)** <br>Trigger amplitude of Fragmentation trigger channels **HISTOGRAM** |
| TH1I * | **[_hTriggerPattern](/Classes/classWaveDaqDisplay.md#variable--htriggerpattern)** <br>Trigger pattern (TRGI) **HISTOGRAM** |
| TH1I * | **[_hTriggerRates](/Classes/classWaveDaqDisplay.md#variable--htriggerrates)** <br>Trigger rates (TRGC) **HISTOGRAM** |
| Bool_t | **[_IncludeCLKs](/Classes/classWaveDaqDisplay.md#variable--includeclks)** <br>Flag to check wether to display CLK signals or not.  |
| std::string | **[_InputFileName](/Classes/classWaveDaqDisplay.md#variable--inputfilename)** <br>Input file name.  |
| Bool_t | **[_IsFragTriggerOn](/Classes/classWaveDaqDisplay.md#variable--isfragtriggeron)** <br>Flag that tells if the fragmentation trigger fired in the event.  |
| Bool_t | **[_IsFragTriggerSWOn](/Classes/classWaveDaqDisplay.md#variable--isfragtriggerswon)** <br>Flag that tells if the fragmentation trigger fired in the event.  |
| Bool_t | **[_IsPossiblePileUp](/Classes/classWaveDaqDisplay.md#variable--ispossiblepileup)** <br>Flag for signaling possible Pile-Up events.  |
| Bool_t | **[_IsPossiblePileUpRC](/Classes/classWaveDaqDisplay.md#variable--ispossiblepileuprc)** <br>Flag for signaling possible Pile-Up events in RC.  |
| bool | **[_IsTDAQ](/Classes/classWaveDaqDisplay.md#variable--istdaq)** <br>Flag that signals if the file comes from the TDAQ.  |
| int | **[_LastEventToSave](/Classes/classWaveDaqDisplay.md#variable--lasteventtosave)** <br>Last event saved in Debug Mode.  |
| UShort_t | **[_NbFast](/Classes/classWaveDaqDisplay.md#variable--nbfast)** <br>Serial number of Neutron Fast board.  |
| UShort_t | **[_NbSlow](/Classes/classWaveDaqDisplay.md#variable--nbslow)** <br>Serial number of Neutron Slow board.  |
| Bool_t | **[_NeutronOn](/Classes/classWaveDaqDisplay.md#variable--neutronon)** <br>Flag for Neutron detectors status in the event.  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NF_WF](/Classes/classWaveDaqDisplay.md#variable--nf-wf)** <br>Container for signals of Fast channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| Float_t | **[_NFAmp](/Classes/classWaveDaqDisplay.md#variable--nfamp)** <br>Neutron Fast channel amplitude (<0) [V].  |
| Float_t | **[_NFCharge](/Classes/classWaveDaqDisplay.md#variable--nfcharge)** <br>Neutron Fast channel integral charge [V*ns].  |
| Float_t | **[_NFPed](/Classes/classWaveDaqDisplay.md#variable--nfped)** <br>Neutron Fast channel pedestal [V].  |
| Float_t | **[_NFPedRMS](/Classes/classWaveDaqDisplay.md#variable--nfpedrms)** <br>Neutron Fast channel pedestal RMS [V].  |
| Float_t | **[_NFRiseTime](/Classes/classWaveDaqDisplay.md#variable--nfrisetime)** <br>Neutron Fast channel rise time [ns].  |
| Float_t | **[_NFTime](/Classes/classWaveDaqDisplay.md#variable--nftime)** <br>Neutron Fast channel raw time [ns].  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NS_WF](/Classes/classWaveDaqDisplay.md#variable--ns-wf)** <br>Container for signals of Slow channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| Float_t | **[_NSAmp](/Classes/classWaveDaqDisplay.md#variable--nsamp)** <br>Neutron Slow channel amplitude (<0) [V].  |
| Float_t | **[_NSCharge](/Classes/classWaveDaqDisplay.md#variable--nscharge)** <br>Neutron Slow channel integral charge [V*ns].  |
| Float_t | **[_NSPed](/Classes/classWaveDaqDisplay.md#variable--nsped)** <br>Neutron Slow channel pedestal [V].  |
| Float_t | **[_NSPedRMS](/Classes/classWaveDaqDisplay.md#variable--nspedrms)** <br>Neutron Slow channel pedestal RMS [V].  |
| Float_t | **[_NSRiseTime](/Classes/classWaveDaqDisplay.md#variable--nsrisetime)** <br>Neutron Slow channel rise time [ns].  |
| Float_t | **[_NSTime](/Classes/classWaveDaqDisplay.md#variable--nstime)** <br>Neutron Slow channel raw time [ns].  |
| std::ofstream | **[_ofsBeamRate](/Classes/classWaveDaqDisplay.md#variable--ofsbeamrate)** <br>Ofstream file for beam rate output (online monitoring)  |
| std::string | **[_OutputFileName](/Classes/classWaveDaqDisplay.md#variable--outputfilename)** <br>Output file name.  |
| Float_t | **[_RC_CLK_phase](/Classes/classWaveDaqDisplay.md#variable--rc-clk-phase)** <br>Phase of Rome Counter CLK [ns].  |
| Float_t | **[_RCAmplitude](/Classes/classWaveDaqDisplay.md#variable--rcamplitude)** <br>RC channel amplitude (<0) [V].  |
| Float_t | **[_RCCharge](/Classes/classWaveDaqDisplay.md#variable--rccharge)** <br>RC channel integral charge [V*ns].  |
| Float_t | **[_RCPedestal](/Classes/classWaveDaqDisplay.md#variable--rcpedestal)** <br>RC channel pedestal [V].  |
| Float_t | **[_RCPedestalRMS](/Classes/classWaveDaqDisplay.md#variable--rcpedestalrms)** <br>RC channel pedestal RMS [V].  |
| Float_t | **[_RCRiseTime](/Classes/classWaveDaqDisplay.md#variable--rcrisetime)** <br>RC channel rise time [ns].  |
| Float_t | **[_RCTime](/Classes/classWaveDaqDisplay.md#variable--rctime)** <br>RC channel time [ns].  |
| Float_t | **[_RCTimeTot](/Classes/classWaveDaqDisplay.md#variable--rctimetot)** <br>RC raw time [ns].  |
| Float_t | **[_RCTotCharge](/Classes/classWaveDaqDisplay.md#variable--rctotcharge)** <br>RC raw total energy loss [V*ns].  |
| bool | **[_SaveBeamRate](/Classes/classWaveDaqDisplay.md#variable--savebeamrate)** <br>Flag that signals if the executable has to save the beam rate (used for online monitoring)  |
| Bool_t | **[_SaveNeutrons](/Classes/classWaveDaqDisplay.md#variable--saveneutrons)** <br>Global flag that checks if the neutron waveforms have to be saved or not in the output.  |
| Float_t | **[_SC_CLK_phase](/Classes/classWaveDaqDisplay.md#variable--sc-clk-phase)** <br>Phase of Start Counter CLK [ns].  |
| Float_t | **[_SCAmplitude](/Classes/classWaveDaqDisplay.md#variable--scamplitude)** <br>SC channel amplitude (<0) [V] **DEBUG ONLY** |
| Float_t | **[_SCCharge](/Classes/classWaveDaqDisplay.md#variable--sccharge)** <br>SC channel integral charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_SCPedestal](/Classes/classWaveDaqDisplay.md#variable--scpedestal)** <br>SC channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_SCPedestalRMS](/Classes/classWaveDaqDisplay.md#variable--scpedestalrms)** <br>SC channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_SCRiseTime](/Classes/classWaveDaqDisplay.md#variable--scrisetime)** <br>SC channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_SCTime](/Classes/classWaveDaqDisplay.md#variable--sctime)** <br>SC raw time [ns].  |
| Float_t | **[_SCTotCharge](/Classes/classWaveDaqDisplay.md#variable--sctotcharge)** <br>SC raw total energy loss [V*ns].  |
| std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > | **[_TCBdata](/Classes/classWaveDaqDisplay.md#variable--tcbdata)** <br>Container for TCB raw data.  |
| [TDAQTag](/Classes/classTDAQTag.md) | **[_TDAQTags](/Classes/classWaveDaqDisplay.md#variable--tdaqtags)** <br>Tags of TDAQ files.  |
| Float_t | **[_TOF](/Classes/classWaveDaqDisplay.md#variable--tof)** <br>TW bar raw Time-Of-Flight [ns].  |
| UInt_t | **[_TotalTimeWD](/Classes/classWaveDaqDisplay.md#variable--totaltimewd)** <br>Total acquisition time for current run [s].  |
| std::map< Int_t, std::pair< Float_t, Float_t > > | **[_TrigCalMap](/Classes/classWaveDaqDisplay.md#variable--trigcalmap)** <br>Fragmentation trigger discriminator amplitude calibration map.  |
| Int_t | **[_TrigFN](/Classes/classWaveDaqDisplay.md#variable--trigfn)** <br>Number of False Negative events in firmware-software quality checks.  |
| Int_t | **[_TrigFP](/Classes/classWaveDaqDisplay.md#variable--trigfp)** <br>Number of False Positive events in firmware-software quality checks.  |
| bool | **[_TriggerEnable](/Classes/classWaveDaqDisplay.md#variable--triggerenable)** <br>Flag for enabling studies on fragmentation trigger.  |
| Float_t | **[_TriggerTh](/Classes/classWaveDaqDisplay.md#variable--triggerth)** <br>Calibrated trigger thresholds [V].  |
| Int_t | **[_TriggerType](/Classes/classWaveDaqDisplay.md#variable--triggertype)** <br>Trigger type of the event.  |
| Int_t | **[_TrigTN](/Classes/classWaveDaqDisplay.md#variable--trigtn)** <br>Number of True Negative events in firmware-software quality checks.  |
| Int_t | **[_TrigTP](/Classes/classWaveDaqDisplay.md#variable--trigtp)** <br>Number of True Positive events in firmware-software quality checks.  |
| std::vector< [WaveFormContainer](/Classes/classWaveFormContainer.md) * > | **[_WaveFormContainer](/Classes/classWaveDaqDisplay.md#variable--waveformcontainer)** <br>Container for WaveDREAM raw waveforms and signal processing methods.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classWaveDaqDisplay.md#variable--wdchannelmap)** <br>WaveDAQ Channel Map.  |
| [WDTag](/Classes/classWDTag.md) | **[_WDTags](/Classes/classWaveDaqDisplay.md#variable--wdtags)** <br>Tags of WaveDREAM stand-alone files.  |
| std::map< TString, std::vector< TGraph * > > | **[_WFmap](/Classes/classWaveDaqDisplay.md#variable--wfmap)** <br>Map containing all the TGraphs for the WaveDAQ detectors.  |

## Additional inherited members

**Public Functions inherited from [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md#function-wavedaqreconstruction)**()<br>Default constructor.  |
| virtual | **[~WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md#function-~wavedaqreconstruction)**()<br>Default destructor.  |


## Public Functions Documentation

### function WaveDaqDisplay

```cpp
WaveDaqDisplay()
```

Default constructor. 

### function ~WaveDaqDisplay

```cpp
virtual ~WaveDaqDisplay()
```

Default destructor. 

### function CheckLoadedBoards

```cpp
virtual void CheckLoadedBoards()
```

Check and print all the loaded WaveDREAM boars. 

**Reimplements**: [WaveDaqReconstruction::CheckLoadedBoards](/Classes/classWaveDaqReconstruction.md#function-checkloadedboards)


This overrides the [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md) function to perform additional operations on the allocation of canvas and waveform maps 


### function EnableHistograms

```cpp
void EnableHistograms()
```

Enable histogram writing in the output. 

### function LoadChannelMap

```cpp
void LoadChannelMap(
    std::string FileName
)
```

Load xml containing the channel map, i.e. the mapping between channels,boards and bar. 

**Parameters**: 

  * **FileName** Name of the input XML file 


Channel map is needed in order to run the Reconstruction executable 


### function LoadTriggerCalibration

```cpp
void LoadTriggerCalibration(
    std::string FileName
)
```

Load the trigger calibration map. 

**Parameters**: 

  * **FileName** Name of the calibration file 


### function RunReconstruction

```cpp
virtual void RunReconstruction(
    std::string FileName,
    std::string TimeCalFileName,
    int nEv
)
```

Perform the reconstruction. 

**Parameters**: 

  * **FileName** Name of the input binary file 
  * **TimeCalFileName** Name of the time calibration file. Equal to the previous parameter for WaveDAQ files 
  * **nEv** Number of events to be processed (optional, default=-1) -> NOT USED BY THIS FUNCTION 


**Reimplements**: [WaveDaqReconstruction::RunReconstruction](/Classes/classWaveDaqReconstruction.md#function-runreconstruction)


### function SetDebugMode

```cpp
void SetDebugMode(
    Int_t first_ev,
    Int_t last_ev
)
```

Activate debug mode if requested and set event range. 

**Parameters**: 

  * **first_ev** First event to save in debug 
  * **last_ev** Last event to save in debug 


### function SetGain

```cpp
void SetGain(
    Float_t Gain
)
```

Set the frontend gain. 

**Parameters**: 

  * **Gain** Frontend gain of the acquisition 


### function SetIncludeCLKs

```cpp
void SetIncludeCLKs()
```

Set the flag for CLK signal display. 

### function SetOutputFileName

```cpp
void SetOutputFileName(
    const std::string & FileName
)
```

Set the output file name. 

**Parameters**: 

  * **FileName** Name of the output file 


### function SetSaveBeamRate

```cpp
void SetSaveBeamRate()
```

Enable the saving of beam rate in an output txt file for online monitoring. 

### function SetSaveNeutrons

```cpp
void SetSaveNeutrons()
```

Set the SaveNeutrons flag to true. 

### function SetTDAQfile

```cpp
void SetTDAQfile()
```

Signal that the file is produced through the TDAQ. 

## Protected Functions Documentation

### function AddCALOPlots

```cpp
void AddCALOPlots(
    UShort_t board
)
```

Add the waveform plots of the CALO. 

**Parameters**: 

  * **board** Serial number of the CALO WaveDREAM board to be added 


The CALO waveforms plotted include all the single channels that cross the (software) zero suppression threshold and their associated CLKs 


### function AddPlots

```cpp
void AddPlots()
```

Add the waveform plots to each detector. 

### function AddSCPlots

```cpp
void AddSCPlots(
    UShort_t board
)
```

Add the waveform plots of the SC. 

**Parameters**: 

  * **board** Serial number of the SC WaveDREAM board 


The SC waveforms plotted include all the single channels, the CLK signal and the summed SC waveform 


### function AddTWPlots

```cpp
void AddTWPlots(
    UShort_t board
)
```

Add the waveform plots of the TW. 

**Parameters**: 

  * **board** Serial number of the TW WaveDREAM board to be added 


The TW waveforms plotted include all the single channels that cross the (software) zero suppression threshold and their associated CLKs 


### function AnalyzeSingleBarEvent

```cpp
void AnalyzeSingleBarEvent(
    Int_t BarId
)
```

Compute the information at the bar level. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function AnalyzeWaveformsCALO

```cpp
void AnalyzeWaveformsCALO(
    UShort_t board
)
```

Analysis of CALO Waveforms (WFs) 

**Parameters**: 

  * **board** Serial number of the CALO board to analyze 


The channels of the CALO with a "good" signal are selected and analyzed 


### function AnalyzeWaveformsNeutrons

```cpp
void AnalyzeWaveformsNeutrons(
    UShort_t board
)
```

Analysis of Neutron detector WFs. 

**Parameters**: 

  * **board** Serial number of the board 


### function AnalyzeWaveformsRC

```cpp
void AnalyzeWaveformsRC(
    UShort_t board
)
```

Analysis of RC Waveforms (WFs) 

**Parameters**: 

  * **board** Serial number of the RC board 


This function performs the whole anlysis of RC waveforms


### function AnalyzeWaveformsSC

```cpp
void AnalyzeWaveformsSC(
    UShort_t board
)
```

Analysis of SC Waveforms (WFs) 

**Parameters**: 

  * **board** Serial number of the SC board 


This function performs the whole anlysis of SC waveforms, which consists of two steps:

* The channels of the SC are added together in a single WF.
* The energy loss in the total SC signal is calculated and saved in a global variable.
* The timestamp of the event is then evaluated applying the CFD method to this WF.
* In debug mode, the routine processes also single SC waveforms one by one.


### function AnalyzeWaveformsTW

```cpp
void AnalyzeWaveformsTW(
    UShort_t board
)
```

Analyze the WFs of TW. 

**Parameters**: 

  * **board** Serial number of the board to be analyzed 


This function extracts data from the A-B channels. The calculated quantities are pedestal, amplitude, integral charge and timestamp of each WF 


### function CheckFragTriggerConditions

```cpp
void CheckFragTriggerConditions()
```

Check if the fragmentation trigger conditions are satisfied. 

### function ClearPlots

```cpp
void ClearPlots()
```

Clear all the plots for the next event. 

### function ClearWFdata

```cpp
void ClearWFdata()
```

Clear all the Waveforms. 

### function CLKAnalysis

```cpp
Float_t CLKAnalysis(
    int boardindex,
    int channel
)
```


### function CreateHistograms

```cpp
void CreateHistograms()
```

Booking of the histograms. 

### function DisplayWaveForms

```cpp
void DisplayWaveForms()
```

Display all the waveforms in their dedicated canvas. 

### function EvalCLKJitter

```cpp
void EvalCLKJitter(
    int boardindex,
    Int_t globalch,
    int channel
)
```

Calculate the clock phase jitter between TW and SC. 

**Parameters**: 

  * **boardindex** Index of the TW board 
  * **globalch** Global Id of the TW channel 
  * **channel** Id of the TW channel 


### function FillHistograms

```cpp
void FillHistograms()
```

Fill the histograms. 

### function FillNeutronWaveforms

```cpp
void FillNeutronWaveforms(
    UShort_t board
)
```

Fill the output objects with neutron waveforms. 

**Parameters**: 

  * **board** Board serial number 


### function GetCRatio

```cpp
Float_t GetCRatio(
    Int_t BarId
)
```

Charge logarithmic ratio. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function GetDeltaT

```cpp
Float_t GetDeltaT(
    Int_t BarId
)
```

Time difference between the two channels. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function GetEventRawEnergy

```cpp
Float_t GetEventRawEnergy(
    Int_t BarId
)
```

Raw energy of the event: geometric mean of the A-B charges. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function GetEventRawTimestamp

```cpp
Float_t GetEventRawTimestamp(
    Int_t BarId
)
```

Bar timestamp of the event: mean of the channels' timestamps. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function GetFileTags

```cpp
void GetFileTags(
    std::string FileName
)
```

Get the file tags. 

**Parameters**: 

  * **FileName** Name of the input file containing the tags 


This function works for WDAQ files only if the filenames are set with the convention chosen by Niccolò (ref. README.md). For TDAQ files, the run and file number are extracted 


### function LoopEvent

```cpp
void LoopEvent(
    TTree * RecTree
)
```

Main event loop. 

**Parameters**: 

  * **RecTree** Pointer to the output tree 


### function PlotAll

```cpp
void PlotAll()
```

Plot all the waveforms in their canvas. 

### function PrintTriggerEfficiency

```cpp
void PrintTriggerEfficiency()
```

Print the fragmentation trigger efficiency. 

### function SavePlots

```cpp
void SavePlots()
```

Save the plots to a file for the current event. 

### function SetOutputDataToZero

```cpp
void SetOutputDataToZero()
```

Function called at the beginning of each event to reset the output data. 

### function SetOutputNeutronWF

```cpp
void SetOutputNeutronWF(
    TTree * RecTree
)
```

Set the output for neutron waveforms. 

**Parameters**: 

  * **RecTree** Pointer to output tree 


### function SetOutputTreeBranches

```cpp
void SetOutputTreeBranches(
    TTree * RecTree
)
```

Booking of the output tree branches. 

**Parameters**: 

  * **RecTree** Pointer to the output tree 


### function TimeOfFlight

```cpp
Float_t TimeOfFlight(
    Int_t BarId
)
```

Uncorrected TOF of the event in ns. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function WaitForNextEventSignal

```cpp
void WaitForNextEventSignal()
```

Create the input dialog window and wait for a command. 

## Protected Attributes Documentation

### variable _ActiveBoards

```cpp
std::map< UShort_t, Int_t > _ActiveBoards;
```

Subset of the _BoardIdtoIdMap containing only the boards w/ at least one active channel; This variable is updated at each event. 

### variable _BCharge

```cpp
Float_t _BCharge;
```

TW bar charge (raw energy loss) [V*ns]. 

### variable _BCratio

```cpp
Float_t _BCratio;
```

TW bar logarithmic ratio of charge "A" over charge "B" [ns]. 

### variable _BDeltaT

```cpp
Float_t _BDeltaT;
```

TW bar raw time difference between channels "A" and "B" [ns]. 

### variable _BeamRate

```cpp
Float_t _BeamRate;
```

Beam Rate calculated as rate of minimum bia triggers [Hz]. 

### variable _BinaryReader

```cpp
ReadBinary * _BinaryReader;
```

Pointer to binary reader object. 

### variable _BoardIdToIdMap

```cpp
std::map< UShort_t,Int_t > _BoardIdToIdMap;
```

Map that links the WaveDREAM board serial number to its index in the [WaveFormContainer](/Classes/classWaveFormContainer.md) vector. 

### variable _BTimestamps

```cpp
Float_t _BTimestamps;
```

TW bar raw time [ns]. 

### variable _CALOAmplitude

```cpp
Float_t _CALOAmplitude;
```

CALO crystal amplitude (<0) [V]. 

### variable _CALOCharge

```cpp
Float_t _CALOCharge;
```

CALO crystal integral charge [V*ns]. 

### variable _CALOPedestal

```cpp
Float_t _CALOPedestal;
```

CALO crystal pedestal [V]. 

### variable _CALOPedestalRMS

```cpp
Float_t _CALOPedestalRMS;
```

CALO crystal pedestal RMS [V]. 

### variable _CALORiseTime

```cpp
Float_t _CALORiseTime;
```

CALO crystal rise time [ns]. 

### variable _CALOTimestamps

```cpp
Float_t _CALOTimestamps;
```

CALO crystal raw time [ns]. 

### variable _CALOTimestampsCorrJit

```cpp
Float_t _CALOTimestampsCorrJit;
```

CALO crystal time with CLK jitter correction [ns]. 

### variable _CAmpA

```cpp
Float_t _CAmpA;
```

TW channel "A" amplitude (<0) [V]. 

### variable _CAmpB

```cpp
Float_t _CAmpB;
```

TW channel "B" amplitude (<0) [V]. 

### variable _CAmplitude

```cpp
Float_t _CAmplitude;
```

TW global channel amplitude [V] **DEBUG ONLY**

### variable _CanvasMap

```cpp
std::map< TString, TCanvas * > _CanvasMap;
```

Map containing all the canvas for the WaveDAQ detectors. 

### variable _CCharge

```cpp
Float_t _CCharge;
```

TW global channel total charge [V*ns] **DEBUG ONLY**

### variable _CChargeA

```cpp
Float_t _CChargeA;
```

TW channel "A" integral charge [V*ns]. 

### variable _CChargeB

```cpp
Float_t _CChargeB;
```

TW channel "B" integral charge [V*ns]. 

### variable _CLK_Jitter

```cpp
Float_t _CLK_Jitter;
```

TW global channel CLK jitter correction [ns] **DEBUG ONLY**

### variable _CLK_phase

```cpp
Float_t _CLK_phase;
```

CLK phase of all boards [ns] **DEBUG ONLY**

### variable _CPedA

```cpp
Float_t _CPedA;
```

TW channel "A" pedestal [V]. 

### variable _CPedB

```cpp
Float_t _CPedB;
```

TW channel "B" pedestal [V]. 

### variable _CPedestal

```cpp
Float_t _CPedestal;
```

TW global channel pedestal [V] **DEBUG ONLY**

### variable _CPedestalRMS

```cpp
Float_t _CPedestalRMS;
```

TW global channel pedestal RMS [V] **DEBUG ONLY**

### variable _CPedRMSA

```cpp
Float_t _CPedRMSA;
```

TW channel "A" pedestal RMS [V]. 

### variable _CPedRMSB

```cpp
Float_t _CPedRMSB;
```

TW channel "B" pedestal RMS [V]. 

### variable _CRiseTime

```cpp
Float_t _CRiseTime;
```

TW global channel rise time [ns] **DEBUG ONLY**

### variable _CRiseTimeA

```cpp
Float_t _CRiseTimeA;
```

TW channel "A" rise time [ns]. 

### variable _CRiseTimeB

```cpp
Float_t _CRiseTimeB;
```

TW channel "B" rise time [ns]. 

### variable _CTimeA

```cpp
Float_t _CTimeA;
```

TW channel "A" time with CLK jitter correction [ns]. 

### variable _CTimeB

```cpp
Float_t _CTimeB;
```

TW channel "B" time with CLK jitter correction [ns]. 

### variable _CTimestamps

```cpp
Float_t _CTimestamps;
```

TW global channel raw time [ns] **DEBUG ONLY**

### variable _CTimestampsCorrJit

```cpp
Float_t _CTimestampsCorrJit;
```

TW global channel time with CLK jitter correction [ns] **DEBUG ONLY**

### variable _Debug

```cpp
bool _Debug;
```

Global debug flag. 

### variable _EnableHisto

```cpp
bool _EnableHisto;
```

Flag for enabling histogram saving. 

### variable _Event

```cpp
int _Event;
```

Current event number. 

### variable _FirstEventToSave

```cpp
int _FirstEventToSave;
```

First event saved in Debug Mode. 

### variable _fOut

```cpp
TFile * _fOut;
```

Pointer to output file. 

### variable _FragTrigBars

```cpp
std::vector< Int_t > _FragTrigBars;
```

List o TW bars connected to the fragmentation trigger. 

### variable _Gain

```cpp
Float_t _Gain;
```

Frontend Gain of the WaveDAQ system. 

### variable _GlobalToBarChIDpairMap

```cpp
TGlobalToBarChIDpairMap _GlobalToBarChIDpairMap;
```

Map linking the TW global channel to the bar and side ("A"/"B") 

### variable _hCALOMultiplicity

```cpp
TH1I * _hCALOMultiplicity;
```

Multiplicity of CALO crystals **HISTOGRAM**

### variable _hFragCharge

```cpp
std::map< Int_t, TH1F * > _hFragCharge;
```

Charge histogram of fragmentation trigger bars with SW chosen threshold! **HISTOGRAM**

### variable _hitmap_all

```cpp
TH2F * _hitmap_all;
```

2D Hitmap of TW for all events **HISTOGRAM**

### variable _hitmap_Bars

```cpp
TH1F * _hitmap_Bars;
```

1D Hitmap of TW bars **HISTOGRAM**

### variable _hitmap_CALO

```cpp
TH2F * _hitmap_CALO;
```

2D Hitmap of TW for Minimum Bias events **HISTOGRAM**

### variable _hitmap_Channels_Front

```cpp
TH1F * _hitmap_Channels_Front;
```

1D Hitmap of TW channels in front layer **HISTOGRAM**

### variable _hitmap_Channels_Rear

```cpp
TH1F * _hitmap_Channels_Rear;
```

1D Hitmap of TW channels in rear layer **HISTOGRAM**

### variable _hitmap_frag

```cpp
TH2F * _hitmap_frag;
```

2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM**

### variable _hitmap_fragSW

```cpp
TH2F * _hitmap_fragSW;
```

2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM**

### variable _hitmap_MB

```cpp
TH2F * _hitmap_MB;
```

2D Hitmap of TW for Minimum Bias events **HISTOGRAM**

### variable _hTGEN_frag

```cpp
TH2F * _hTGEN_frag;
```

Trigger generation (TGEN) for Fragmentation Trigger Events **HISTOGRAM**

### variable _hTGEN_MB

```cpp
TH2F * _hTGEN_MB;
```

Trigger generation (TGEN) for Minimum Bias Events **HISTOGRAM**

### variable _hTrigAmp

```cpp
TH1F ** _hTrigAmp;
```

Trigger amplitude of Fragmentation trigger channels **HISTOGRAM**

### variable _hTriggerPattern

```cpp
TH1I * _hTriggerPattern;
```

Trigger pattern (TRGI) **HISTOGRAM**

### variable _hTriggerRates

```cpp
TH1I * _hTriggerRates;
```

Trigger rates (TRGC) **HISTOGRAM**

### variable _IncludeCLKs

```cpp
Bool_t _IncludeCLKs;
```

Flag to check wether to display CLK signals or not. 

### variable _InputFileName

```cpp
std::string _InputFileName;
```

Input file name. 

### variable _IsFragTriggerOn

```cpp
Bool_t _IsFragTriggerOn;
```

Flag that tells if the fragmentation trigger fired in the event. 

### variable _IsFragTriggerSWOn

```cpp
Bool_t _IsFragTriggerSWOn;
```

Flag that tells if the fragmentation trigger fired in the event. 

### variable _IsPossiblePileUp

```cpp
Bool_t _IsPossiblePileUp;
```

Flag for signaling possible Pile-Up events. 

### variable _IsPossiblePileUpRC

```cpp
Bool_t _IsPossiblePileUpRC;
```

Flag for signaling possible Pile-Up events in RC. 

### variable _IsTDAQ

```cpp
bool _IsTDAQ;
```

Flag that signals if the file comes from the TDAQ. 

### variable _LastEventToSave

```cpp
int _LastEventToSave;
```

Last event saved in Debug Mode. 

### variable _NbFast

```cpp
UShort_t _NbFast;
```

Serial number of Neutron Fast board. 

### variable _NbSlow

```cpp
UShort_t _NbSlow;
```

Serial number of Neutron Slow board. 

### variable _NeutronOn

```cpp
Bool_t _NeutronOn;
```

Flag for Neutron detectors status in the event. 

### variable _NF_WF

```cpp
NeutronWF * _NF_WF = nullptr;
```

Container for signals of Fast channels of Neutron detectors (only used when _SaveNeutrons is True) 

### variable _NFAmp

```cpp
Float_t _NFAmp;
```

Neutron Fast channel amplitude (<0) [V]. 

### variable _NFCharge

```cpp
Float_t _NFCharge;
```

Neutron Fast channel integral charge [V*ns]. 

### variable _NFPed

```cpp
Float_t _NFPed;
```

Neutron Fast channel pedestal [V]. 

### variable _NFPedRMS

```cpp
Float_t _NFPedRMS;
```

Neutron Fast channel pedestal RMS [V]. 

### variable _NFRiseTime

```cpp
Float_t _NFRiseTime;
```

Neutron Fast channel rise time [ns]. 

### variable _NFTime

```cpp
Float_t _NFTime;
```

Neutron Fast channel raw time [ns]. 

### variable _NS_WF

```cpp
NeutronWF * _NS_WF = nullptr;
```

Container for signals of Slow channels of Neutron detectors (only used when _SaveNeutrons is True) 

### variable _NSAmp

```cpp
Float_t _NSAmp;
```

Neutron Slow channel amplitude (<0) [V]. 

### variable _NSCharge

```cpp
Float_t _NSCharge;
```

Neutron Slow channel integral charge [V*ns]. 

### variable _NSPed

```cpp
Float_t _NSPed;
```

Neutron Slow channel pedestal [V]. 

### variable _NSPedRMS

```cpp
Float_t _NSPedRMS;
```

Neutron Slow channel pedestal RMS [V]. 

### variable _NSRiseTime

```cpp
Float_t _NSRiseTime;
```

Neutron Slow channel rise time [ns]. 

### variable _NSTime

```cpp
Float_t _NSTime;
```

Neutron Slow channel raw time [ns]. 

### variable _ofsBeamRate

```cpp
std::ofstream _ofsBeamRate;
```

Ofstream file for beam rate output (online monitoring) 

### variable _OutputFileName

```cpp
std::string _OutputFileName;
```

Output file name. 

### variable _RC_CLK_phase

```cpp
Float_t _RC_CLK_phase;
```

Phase of Rome Counter CLK [ns]. 

### variable _RCAmplitude

```cpp
Float_t _RCAmplitude;
```

RC channel amplitude (<0) [V]. 

### variable _RCCharge

```cpp
Float_t _RCCharge;
```

RC channel integral charge [V*ns]. 

### variable _RCPedestal

```cpp
Float_t _RCPedestal;
```

RC channel pedestal [V]. 

### variable _RCPedestalRMS

```cpp
Float_t _RCPedestalRMS;
```

RC channel pedestal RMS [V]. 

### variable _RCRiseTime

```cpp
Float_t _RCRiseTime;
```

RC channel rise time [ns]. 

### variable _RCTime

```cpp
Float_t _RCTime;
```

RC channel time [ns]. 

### variable _RCTimeTot

```cpp
Float_t _RCTimeTot;
```

RC raw time [ns]. 

### variable _RCTotCharge

```cpp
Float_t _RCTotCharge;
```

RC raw total energy loss [V*ns]. 

### variable _SaveBeamRate

```cpp
bool _SaveBeamRate;
```

Flag that signals if the executable has to save the beam rate (used for online monitoring) 

### variable _SaveNeutrons

```cpp
Bool_t _SaveNeutrons;
```

Global flag that checks if the neutron waveforms have to be saved or not in the output. 

### variable _SC_CLK_phase

```cpp
Float_t _SC_CLK_phase;
```

Phase of Start Counter CLK [ns]. 

### variable _SCAmplitude

```cpp
Float_t _SCAmplitude;
```

SC channel amplitude (<0) [V] **DEBUG ONLY**

### variable _SCCharge

```cpp
Float_t _SCCharge;
```

SC channel integral charge [V*ns] **DEBUG ONLY**

### variable _SCPedestal

```cpp
Float_t _SCPedestal;
```

SC channel pedestal [V] **DEBUG ONLY**

### variable _SCPedestalRMS

```cpp
Float_t _SCPedestalRMS;
```

SC channel pedestal RMS [V] **DEBUG ONLY**

### variable _SCRiseTime

```cpp
Float_t _SCRiseTime;
```

SC channel rise time [ns] **DEBUG ONLY**

### variable _SCTime

```cpp
Float_t _SCTime;
```

SC raw time [ns]. 

### variable _SCTotCharge

```cpp
Float_t _SCTotCharge;
```

SC raw total energy loss [V*ns]. 

### variable _TCBdata

```cpp
std::vector< TCBDATA * > _TCBdata;
```

Container for TCB raw data. 

### variable _TDAQTags

```cpp
TDAQTag _TDAQTags;
```

Tags of TDAQ files. 

### variable _TOF

```cpp
Float_t _TOF;
```

TW bar raw Time-Of-Flight [ns]. 

### variable _TotalTimeWD

```cpp
UInt_t _TotalTimeWD;
```

Total acquisition time for current run [s]. 

### variable _TrigCalMap

```cpp
std::map< Int_t, std::pair< Float_t, Float_t > > _TrigCalMap;
```

Fragmentation trigger discriminator amplitude calibration map. 

### variable _TrigFN

```cpp
Int_t _TrigFN;
```

Number of False Negative events in firmware-software quality checks. 

### variable _TrigFP

```cpp
Int_t _TrigFP;
```

Number of False Positive events in firmware-software quality checks. 

### variable _TriggerEnable

```cpp
bool _TriggerEnable;
```

Flag for enabling studies on fragmentation trigger. 

### variable _TriggerTh

```cpp
Float_t _TriggerTh;
```

Calibrated trigger thresholds [V]. 

### variable _TriggerType

```cpp
Int_t _TriggerType;
```

Trigger type of the event. 

### variable _TrigTN

```cpp
Int_t _TrigTN;
```

Number of True Negative events in firmware-software quality checks. 

### variable _TrigTP

```cpp
Int_t _TrigTP;
```

Number of True Positive events in firmware-software quality checks. 

### variable _WaveFormContainer

```cpp
std::vector< WaveFormContainer * > _WaveFormContainer;
```

Container for WaveDREAM raw waveforms and signal processing methods. 

### variable _WDChannelMap

```cpp
WDChannelMap _WDChannelMap;
```

WaveDAQ Channel Map. 

### variable _WDTags

```cpp
WDTag _WDTags;
```

Tags of WaveDREAM stand-alone files. 

### variable _WFmap

```cpp
std::map< TString, std::vector< TGraph * > > _WFmap;
```

Map containing all the TGraphs for the WaveDAQ detectors. 

-------------------------------

Updated on 2023-05-20 at 18:19:18 +0000