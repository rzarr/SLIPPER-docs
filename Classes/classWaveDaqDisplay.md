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
| virtual void | **[RunReconstruction](/Classes/classWaveDaqDisplay.md#function-runreconstruction)**(std::string FileName, std::string TimeCalFileName, int nEv)<br>Perform the reconstruction.  |
| void | **[SetIncludeCLKs](/Classes/classWaveDaqDisplay.md#function-setincludeclks)**()<br>Set the flag for CLK signal display.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddCALOPlots](/Classes/classWaveDaqDisplay.md#function-addcaloplots)**(UShort_t board)<br>Add the waveform plots of the CALO.  |
| void | **[AddPlots](/Classes/classWaveDaqDisplay.md#function-addplots)**()<br>Add the waveform plots to each detector.  |
| void | **[AddSCPlots](/Classes/classWaveDaqDisplay.md#function-addscplots)**(UShort_t board)<br>Add the waveform plots of the SC.  |
| void | **[AddTWPlots](/Classes/classWaveDaqDisplay.md#function-addtwplots)**(UShort_t board)<br>Add the waveform plots of the TW.  |
| void | **[ClearPlots](/Classes/classWaveDaqDisplay.md#function-clearplots)**()<br>Clear all the plots for the next event.  |
| void | **[DisplayWaveForms](/Classes/classWaveDaqDisplay.md#function-displaywaveforms)**()<br>Display all the waveforms in their dedicated canvas.  |
| Bool_t | **[GoToPreviousEvent](/Classes/classWaveDaqDisplay.md#function-gotopreviousevent)**()<br>Go to the previous event of the file.  |
| void | **[PlotAll](/Classes/classWaveDaqDisplay.md#function-plotall)**()<br>Plot all the waveforms in their canvas.  |
| void | **[SavePlots](/Classes/classWaveDaqDisplay.md#function-saveplots)**()<br>Save the plots to a file for the current event.  |
| void | **[WaitForNextEventSignal](/Classes/classWaveDaqDisplay.md#function-waitfornexteventsignal)**()<br>Wait until a command is given to the input.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< TString, TCanvas * > | **[_CanvasMap](/Classes/classWaveDaqDisplay.md#variable--canvasmap)** <br>Map containing all the canvas for the WaveDAQ detectors.  |
| std::vector< UInt_t > | **[_EventSize](/Classes/classWaveDaqDisplay.md#variable--eventsize)** <br>Vector of read event sizes in bytes.  |
| Bool_t | **[_IncludeCLKs](/Classes/classWaveDaqDisplay.md#variable--includeclks)** <br>Flag to check wether to display CLK signals or not.  |
| std::map< TString, std::vector< TGraph * > > | **[_WFmap](/Classes/classWaveDaqDisplay.md#variable--wfmap)** <br>Map containing all the TGraphs for the WaveDAQ detectors.  |

## Additional inherited members

**Public Functions inherited from [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md#function-wavedaqreconstruction)**()<br>Default constructor.  |
| virtual | **[~WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md#function-~wavedaqreconstruction)**()<br>Default destructor.  |
| void | **[EnableHistograms](/Classes/classWaveDaqReconstruction.md#function-enablehistograms)**()<br>Enable histogram writing in the output.  |
| void | **[LoadChannelMap](/Classes/classWaveDaqReconstruction.md#function-loadchannelmap)**(std::string FileName)<br>Load xml containing the channel map, i.e. the mapping between channels,boards and bar.  |
| void | **[LoadTriggerCalibration](/Classes/classWaveDaqReconstruction.md#function-loadtriggercalibration)**(std::string FileName)<br>Load the trigger calibration map.  |
| void | **[SetDebugMode](/Classes/classWaveDaqReconstruction.md#function-setdebugmode)**(Int_t first_ev, Int_t last_ev)<br>Activate debug mode if requested and set event range.  |
| void | **[SetGain](/Classes/classWaveDaqReconstruction.md#function-setgain)**(Float_t Gain) |
| void | **[SetOutputFileName](/Classes/classWaveDaqReconstruction.md#function-setoutputfilename)**(const std::string & FileName)<br>Set the output file name.  |
| void | **[SetSaveBeamRate](/Classes/classWaveDaqReconstruction.md#function-setsavebeamrate)**()<br>Enable the saving of beam rate in an output txt file for online monitoring.  |
| void | **[SetSaveNeutrons](/Classes/classWaveDaqReconstruction.md#function-setsaveneutrons)**()<br>Set the SaveNeutrons flag to true.  |
| void | **[SetTDAQfile](/Classes/classWaveDaqReconstruction.md#function-settdaqfile)**()<br>Signal that the file is produced through the TDAQ.  |

**Protected Functions inherited from [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)**

|                | Name           |
| -------------- | -------------- |
| void | **[AnalyzeSingleBarEvent](/Classes/classWaveDaqReconstruction.md#function-analyzesinglebarevent)**(Int_t BarId)<br>Compute the information at the bar level.  |
| void | **[AnalyzeWaveformsCALO](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformscalo)**(UShort_t board)<br>Analysis of CALO Waveforms (WFs)  |
| void | **[AnalyzeWaveformsNeutrons](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformsneutrons)**(UShort_t board)<br>Analysis of Neutron detector WFs.  |
| void | **[AnalyzeWaveformsRC](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformsrc)**(UShort_t board)<br>Analysis of RC Waveforms (WFs)  |
| void | **[AnalyzeWaveformsSC](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformssc)**(UShort_t board)<br>Analysis of SC Waveforms (WFs)  |
| void | **[AnalyzeWaveformsTW](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformstw)**(UShort_t board)<br>Analyze the WFs of TW.  |
| void | **[CheckFragTriggerConditions](/Classes/classWaveDaqReconstruction.md#function-checkfragtriggerconditions)**()<br>Check if the fragmentation trigger conditions are satisfied.  |
| void | **[ClearWFdata](/Classes/classWaveDaqReconstruction.md#function-clearwfdata)**()<br>Clear all the Waveforms.  |
| Float_t | **[CLKAnalysis](/Classes/classWaveDaqReconstruction.md#function-clkanalysis)**(int boardindex, int channel) |
| void | **[CreateHistograms](/Classes/classWaveDaqReconstruction.md#function-createhistograms)**()<br>Booking of the histograms.  |
| void | **[EvalCLKJitter](/Classes/classWaveDaqReconstruction.md#function-evalclkjitter)**(int boardindex, Int_t globalch, int channel)<br>Calculate the clock phase jitter between TW and SC.  |
| void | **[FillHistograms](/Classes/classWaveDaqReconstruction.md#function-fillhistograms)**()<br>Fill the histograms.  |
| void | **[FillNeutronWaveforms](/Classes/classWaveDaqReconstruction.md#function-fillneutronwaveforms)**(UShort_t board)<br>Fill the output objects with neutron waveforms.  |
| Float_t | **[GetCRatio](/Classes/classWaveDaqReconstruction.md#function-getcratio)**(Int_t BarId)<br>Charge logarithmic ratio.  |
| Float_t | **[GetDeltaT](/Classes/classWaveDaqReconstruction.md#function-getdeltat)**(Int_t BarId)<br>Time difference between the two channels.  |
| Float_t | **[GetEventRawEnergy](/Classes/classWaveDaqReconstruction.md#function-geteventrawenergy)**(Int_t BarId)<br>Raw energy of the event: geometric mean of the A-B charges.  |
| Float_t | **[GetEventRawTimestamp](/Classes/classWaveDaqReconstruction.md#function-geteventrawtimestamp)**(Int_t BarId)<br>Bar timestamp of the event: mean of the channels' timestamps.  |
| void | **[GetFileTags](/Classes/classWaveDaqReconstruction.md#function-getfiletags)**(std::string FileName)<br>Get the file tags.  |
| void | **[LoopEvent](/Classes/classWaveDaqReconstruction.md#function-loopevent)**(TTree * RecTree)<br>Main event loop.  |
| void | **[PrintTriggerEfficiency](/Classes/classWaveDaqReconstruction.md#function-printtriggerefficiency)**()<br>Print the fragmentation trigger efficiency.  |
| void | **[SetOutputDataToZero](/Classes/classWaveDaqReconstruction.md#function-setoutputdatatozero)**()<br>Function called at the beginning of each event to reset the output data.  |
| void | **[SetOutputNeutronWF](/Classes/classWaveDaqReconstruction.md#function-setoutputneutronwf)**(TTree * RecTree)<br>Set the output for neutron waveforms.  |
| void | **[SetOutputTreeBranches](/Classes/classWaveDaqReconstruction.md#function-setoutputtreebranches)**(TTree * RecTree)<br>Booking of the output tree branches.  |
| Float_t | **[TimeOfFlight](/Classes/classWaveDaqReconstruction.md#function-timeofflight)**(Int_t BarId)<br>Uncorrected TOF of the event in ns.  |

**Protected Attributes inherited from [WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)**

|                | Name           |
| -------------- | -------------- |
| std::map< UShort_t, Int_t > | **[_ActiveBoards](/Classes/classWaveDaqReconstruction.md#variable--activeboards)** <br>Subset of the _BoardIdtoIdMap containing only the boards w/ at least one active channel; This variable is updated at each event.  |
| Float_t | **[_BCharge](/Classes/classWaveDaqReconstruction.md#variable--bcharge)** <br>TW bar charge (raw energy loss) [V*ns].  |
| Float_t | **[_BCratio](/Classes/classWaveDaqReconstruction.md#variable--bcratio)** <br>TW bar logarithmic ratio of charge "A" over charge "B" [ns].  |
| Float_t | **[_BDeltaT](/Classes/classWaveDaqReconstruction.md#variable--bdeltat)** <br>TW bar raw time difference between channels "A" and "B" [ns].  |
| [ReadBinary](/Classes/classReadBinary.md) * | **[_BinaryReader](/Classes/classWaveDaqReconstruction.md#variable--binaryreader)** <br>Pointer to binary reader object.  |
| std::map< UShort_t,Int_t > | **[_BoardIdToIdMap](/Classes/classWaveDaqReconstruction.md#variable--boardidtoidmap)** <br>Map that links the WaveDREAM board serial number to its index in the [WaveFormContainer](/Classes/classWaveFormContainer.md) vector.  |
| Float_t | **[_BTimestamps](/Classes/classWaveDaqReconstruction.md#variable--btimestamps)** <br>TW bar raw time [ns].  |
| Float_t | **[_CALOAmplitude](/Classes/classWaveDaqReconstruction.md#variable--caloamplitude)** <br>CALO crystal amplitude (<0) [V].  |
| Float_t | **[_CALOCharge](/Classes/classWaveDaqReconstruction.md#variable--calocharge)** <br>CALO crystal integral charge [V*ns].  |
| Float_t | **[_CALOPedestal](/Classes/classWaveDaqReconstruction.md#variable--calopedestal)** <br>CALO crystal pedestal [V].  |
| Float_t | **[_CALOPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--calopedestalrms)** <br>CALO crystal pedestal RMS [V].  |
| Float_t | **[_CALORiseTime](/Classes/classWaveDaqReconstruction.md#variable--calorisetime)** <br>CALO crystal rise time [ns].  |
| Float_t | **[_CALOTimestamps](/Classes/classWaveDaqReconstruction.md#variable--calotimestamps)** <br>CALO crystal raw time [ns].  |
| Float_t | **[_CALOTimestampsCorrJit](/Classes/classWaveDaqReconstruction.md#variable--calotimestampscorrjit)** <br>CALO crystal time with CLK jitter correction [ns].  |
| Float_t | **[_CAmpA](/Classes/classWaveDaqReconstruction.md#variable--campa)** <br>TW channel "A" amplitude (<0) [V].  |
| Float_t | **[_CAmpB](/Classes/classWaveDaqReconstruction.md#variable--campb)** <br>TW channel "B" amplitude (<0) [V].  |
| Float_t | **[_CAmplitude](/Classes/classWaveDaqReconstruction.md#variable--camplitude)** <br>TW global channel amplitude [V] **DEBUG ONLY** |
| Float_t | **[_CCharge](/Classes/classWaveDaqReconstruction.md#variable--ccharge)** <br>TW global channel total charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_CChargeA](/Classes/classWaveDaqReconstruction.md#variable--cchargea)** <br>TW channel "A" integral charge [V*ns].  |
| Float_t | **[_CChargeB](/Classes/classWaveDaqReconstruction.md#variable--cchargeb)** <br>TW channel "B" integral charge [V*ns].  |
| Float_t | **[_CLK_Jitter](/Classes/classWaveDaqReconstruction.md#variable--clk-jitter)** <br>TW global channel CLK jitter correction [ns] **DEBUG ONLY** |
| Float_t | **[_CLK_phase](/Classes/classWaveDaqReconstruction.md#variable--clk-phase)** <br>CLK phase of all boards [ns] **DEBUG ONLY** |
| Float_t | **[_CPedA](/Classes/classWaveDaqReconstruction.md#variable--cpeda)** <br>TW channel "A" pedestal [V].  |
| Float_t | **[_CPedB](/Classes/classWaveDaqReconstruction.md#variable--cpedb)** <br>TW channel "B" pedestal [V].  |
| Float_t | **[_CPedestal](/Classes/classWaveDaqReconstruction.md#variable--cpedestal)** <br>TW global channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_CPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--cpedestalrms)** <br>TW global channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_CPedRMSA](/Classes/classWaveDaqReconstruction.md#variable--cpedrmsa)** <br>TW channel "A" pedestal RMS [V].  |
| Float_t | **[_CPedRMSB](/Classes/classWaveDaqReconstruction.md#variable--cpedrmsb)** <br>TW channel "B" pedestal RMS [V].  |
| Float_t | **[_CRiseTime](/Classes/classWaveDaqReconstruction.md#variable--crisetime)** <br>TW global channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_CRiseTimeA](/Classes/classWaveDaqReconstruction.md#variable--crisetimea)** <br>TW channel "A" rise time [ns].  |
| Float_t | **[_CRiseTimeB](/Classes/classWaveDaqReconstruction.md#variable--crisetimeb)** <br>TW channel "B" rise time [ns].  |
| Float_t | **[_CTimeA](/Classes/classWaveDaqReconstruction.md#variable--ctimea)** <br>TW channel "A" time with CLK jitter correction [ns].  |
| Float_t | **[_CTimeB](/Classes/classWaveDaqReconstruction.md#variable--ctimeb)** <br>TW channel "B" time with CLK jitter correction [ns].  |
| Float_t | **[_CTimestamps](/Classes/classWaveDaqReconstruction.md#variable--ctimestamps)** <br>TW global channel raw time [ns] **DEBUG ONLY** |
| Float_t | **[_CTimestampsCorrJit](/Classes/classWaveDaqReconstruction.md#variable--ctimestampscorrjit)** <br>TW global channel time with CLK jitter correction [ns] **DEBUG ONLY** |
| bool | **[_Debug](/Classes/classWaveDaqReconstruction.md#variable--debug)** <br>Global debug flag.  |
| bool | **[_EnableHisto](/Classes/classWaveDaqReconstruction.md#variable--enablehisto)** <br>Flag for enabling histogram saving.  |
| int | **[_Event](/Classes/classWaveDaqReconstruction.md#variable--event)** <br>Current event number.  |
| int | **[_FirstEventToSave](/Classes/classWaveDaqReconstruction.md#variable--firsteventtosave)** <br>First event saved in Debug Mode.  |
| TFile * | **[_fOut](/Classes/classWaveDaqReconstruction.md#variable--fout)** <br>Pointer to output file.  |
| std::vector< Int_t > | **[_FragTrigBars](/Classes/classWaveDaqReconstruction.md#variable--fragtrigbars)** <br>List o TW bars connected to the fragmentation trigger.  |
| Float_t | **[_Gain](/Classes/classWaveDaqReconstruction.md#variable--gain)** <br>Frontend Gain of the WaveDAQ system.  |
| TGlobalToBarChIDpairMap | **[_GlobalToBarChIDpairMap](/Classes/classWaveDaqReconstruction.md#variable--globaltobarchidpairmap)** <br>Map linking the TW global channel to the bar and side ("A"/"B")  |
| TH1I * | **[_hCALOMultiplicity](/Classes/classWaveDaqReconstruction.md#variable--hcalomultiplicity)** <br>Multiplicity of CALO crystals **HISTOGRAM** |
| std::map< Int_t, TH1F * > | **[_hFragSWCharge](/Classes/classWaveDaqReconstruction.md#variable--hfragswcharge)** <br>Charge histogram of fragmentation trigger bars with SW chosen threshold! **HISTOGRAM** |
| TH2F * | **[_hitmap_all](/Classes/classWaveDaqReconstruction.md#variable--hitmap-all)** <br>2D Hitmap of TW for all events **HISTOGRAM** |
| TH1F * | **[_hitmap_Bars](/Classes/classWaveDaqReconstruction.md#variable--hitmap-bars)** <br>1D Hitmap of TW bars **HISTOGRAM** |
| TH2F * | **[_hitmap_CALO](/Classes/classWaveDaqReconstruction.md#variable--hitmap-calo)** <br>2D Hitmap of TW for Minimum Bias events **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Front](/Classes/classWaveDaqReconstruction.md#variable--hitmap-channels-front)** <br>1D Hitmap of TW channels in front layer **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Rear](/Classes/classWaveDaqReconstruction.md#variable--hitmap-channels-rear)** <br>1D Hitmap of TW channels in rear layer **HISTOGRAM** |
| TH2F * | **[_hitmap_frag](/Classes/classWaveDaqReconstruction.md#variable--hitmap-frag)** <br>2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM** |
| TH2F * | **[_hitmap_fragSW](/Classes/classWaveDaqReconstruction.md#variable--hitmap-fragsw)** <br>2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM** |
| TH2F * | **[_hitmap_MB](/Classes/classWaveDaqReconstruction.md#variable--hitmap-mb)** <br>2D Hitmap of TW for Minimum Bias events **HISTOGRAM** |
| TH2F * | **[_hTGEN_all](/Classes/classWaveDaqReconstruction.md#variable--htgen-all)** <br>Trigger generation (TGEN) for all acquired events **HISTOGRAM** |
| TH2F * | **[_hTGEN_frag](/Classes/classWaveDaqReconstruction.md#variable--htgen-frag)** <br>Trigger generation (TGEN) for Fragmentation Trigger Events **HISTOGRAM** |
| TH2F * | **[_hTGEN_MB](/Classes/classWaveDaqReconstruction.md#variable--htgen-mb)** <br>Trigger generation (TGEN) for Minimum Bias Events **HISTOGRAM** |
| TH1F ** | **[_hTrigAmp](/Classes/classWaveDaqReconstruction.md#variable--htrigamp)** <br>Trigger amplitude of Fragmentation trigger channels **HISTOGRAM** |
| TH1I * | **[_hTriggerPattern](/Classes/classWaveDaqReconstruction.md#variable--htriggerpattern)** <br>Trigger pattern (TRGI) **HISTOGRAM** |
| TH1I * | **[_hTriggerRates](/Classes/classWaveDaqReconstruction.md#variable--htriggerrates)** <br>Trigger rates (TRGC) **HISTOGRAM** |
| std::string | **[_InputFileName](/Classes/classWaveDaqReconstruction.md#variable--inputfilename)** <br>Input file name.  |
| Bool_t | **[_IsFragTriggerOn](/Classes/classWaveDaqReconstruction.md#variable--isfragtriggeron)** <br>Flag that tells if the fragmentation trigger fired in the event.  |
| Bool_t | **[_IsFragTriggerSWOn](/Classes/classWaveDaqReconstruction.md#variable--isfragtriggerswon)** <br>Flag that tells if the fragmentation trigger fired in the event.  |
| Bool_t | **[_IsPossiblePileUp](/Classes/classWaveDaqReconstruction.md#variable--ispossiblepileup)** <br>Flag for signaling possible Pile-Up events.  |
| Bool_t | **[_IsPossiblePileUpRC](/Classes/classWaveDaqReconstruction.md#variable--ispossiblepileuprc)** <br>Flag for signaling possible Pile-Up events in RC.  |
| bool | **[_IsTDAQ](/Classes/classWaveDaqReconstruction.md#variable--istdaq)** <br>Flag that signals if the file comes from the TDAQ.  |
| int | **[_LastEventToSave](/Classes/classWaveDaqReconstruction.md#variable--lasteventtosave)** <br>Last event saved in Debug Mode.  |
| UShort_t | **[_NbFast](/Classes/classWaveDaqReconstruction.md#variable--nbfast)** <br>Serial number of Neutron Fast board.  |
| UShort_t | **[_NbSlow](/Classes/classWaveDaqReconstruction.md#variable--nbslow)** <br>Serial number of Neutron Slow board.  |
| Bool_t | **[_NeutronOn](/Classes/classWaveDaqReconstruction.md#variable--neutronon)** <br>Flag for Neutron detectors status in the event.  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NF_WF](/Classes/classWaveDaqReconstruction.md#variable--nf-wf)** <br>Container for signals of Fast channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| Float_t | **[_NFAmp](/Classes/classWaveDaqReconstruction.md#variable--nfamp)** <br>Neutron Fast channel amplitude (<0) [V].  |
| Float_t | **[_NFCharge](/Classes/classWaveDaqReconstruction.md#variable--nfcharge)** <br>Neutron Fast channel integral charge [V*ns].  |
| Float_t | **[_NFPed](/Classes/classWaveDaqReconstruction.md#variable--nfped)** <br>Neutron Fast channel pedestal [V].  |
| Float_t | **[_NFPedRMS](/Classes/classWaveDaqReconstruction.md#variable--nfpedrms)** <br>Neutron Fast channel pedestal RMS [V].  |
| Float_t | **[_NFRiseTime](/Classes/classWaveDaqReconstruction.md#variable--nfrisetime)** <br>Neutron Fast channel rise time [ns].  |
| Float_t | **[_NFTime](/Classes/classWaveDaqReconstruction.md#variable--nftime)** <br>Neutron Fast channel raw time [ns].  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NS_WF](/Classes/classWaveDaqReconstruction.md#variable--ns-wf)** <br>Container for signals of Slow channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| Float_t | **[_NSAmp](/Classes/classWaveDaqReconstruction.md#variable--nsamp)** <br>Neutron Slow channel amplitude (<0) [V].  |
| Float_t | **[_NSCharge](/Classes/classWaveDaqReconstruction.md#variable--nscharge)** <br>Neutron Slow channel integral charge [V*ns].  |
| Float_t | **[_NSPed](/Classes/classWaveDaqReconstruction.md#variable--nsped)** <br>Neutron Slow channel pedestal [V].  |
| Float_t | **[_NSPedRMS](/Classes/classWaveDaqReconstruction.md#variable--nspedrms)** <br>Neutron Slow channel pedestal RMS [V].  |
| Float_t | **[_NSRiseTime](/Classes/classWaveDaqReconstruction.md#variable--nsrisetime)** <br>Neutron Slow channel rise time [ns].  |
| Float_t | **[_NSTime](/Classes/classWaveDaqReconstruction.md#variable--nstime)** <br>Neutron Slow channel raw time [ns].  |
| std::ofstream | **[_ofsBeamRate](/Classes/classWaveDaqReconstruction.md#variable--ofsbeamrate)** <br>Ofstream file for beam rate output (online monitoring)  |
| std::string | **[_OutputFileName](/Classes/classWaveDaqReconstruction.md#variable--outputfilename)** <br>Output file name.  |
| Float_t | **[_RC_CLK_phase](/Classes/classWaveDaqReconstruction.md#variable--rc-clk-phase)** <br>Phase of Rome Counter CLK [ns].  |
| Float_t | **[_RCAmplitude](/Classes/classWaveDaqReconstruction.md#variable--rcamplitude)** <br>RC channel amplitude (<0) [V].  |
| Float_t | **[_RCCharge](/Classes/classWaveDaqReconstruction.md#variable--rccharge)** <br>RC channel integral charge [V*ns].  |
| Float_t | **[_RCPedestal](/Classes/classWaveDaqReconstruction.md#variable--rcpedestal)** <br>RC channel pedestal [V].  |
| Float_t | **[_RCPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--rcpedestalrms)** <br>RC channel pedestal RMS [V].  |
| Float_t | **[_RCRiseTime](/Classes/classWaveDaqReconstruction.md#variable--rcrisetime)** <br>RC channel rise time [ns].  |
| Float_t | **[_RCTime](/Classes/classWaveDaqReconstruction.md#variable--rctime)** <br>RC channel time [ns].  |
| Float_t | **[_RCTimeTot](/Classes/classWaveDaqReconstruction.md#variable--rctimetot)** <br>RC raw time [ns].  |
| Float_t | **[_RCTotCharge](/Classes/classWaveDaqReconstruction.md#variable--rctotcharge)** <br>RC raw total energy loss [V*ns].  |
| bool | **[_SaveBeamRate](/Classes/classWaveDaqReconstruction.md#variable--savebeamrate)** <br>Flag that signals if the executable has to save the beam rate (used for online monitoring)  |
| Bool_t | **[_SaveNeutrons](/Classes/classWaveDaqReconstruction.md#variable--saveneutrons)** <br>Global flag that checks if the neutron waveforms have to be saved or not in the output.  |
| Float_t | **[_SC_CLK_phase](/Classes/classWaveDaqReconstruction.md#variable--sc-clk-phase)** <br>Phase of Start Counter CLK [ns].  |
| Float_t | **[_SCAmplitude](/Classes/classWaveDaqReconstruction.md#variable--scamplitude)** <br>SC channel amplitude (<0) [V] **DEBUG ONLY** |
| Float_t | **[_SCCharge](/Classes/classWaveDaqReconstruction.md#variable--sccharge)** <br>SC channel integral charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_SCPedestal](/Classes/classWaveDaqReconstruction.md#variable--scpedestal)** <br>SC channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_SCPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--scpedestalrms)** <br>SC channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_SCRiseTime](/Classes/classWaveDaqReconstruction.md#variable--scrisetime)** <br>SC channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_SCTime](/Classes/classWaveDaqReconstruction.md#variable--sctime)** <br>SC raw time [ns].  |
| Float_t | **[_SCTotCharge](/Classes/classWaveDaqReconstruction.md#variable--sctotcharge)** <br>SC raw total energy loss [V*ns].  |
| std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > | **[_TCBdata](/Classes/classWaveDaqReconstruction.md#variable--tcbdata)** <br>Container for TCB raw data.  |
| [TDAQTag](/Classes/classTDAQTag.md) | **[_TDAQTags](/Classes/classWaveDaqReconstruction.md#variable--tdaqtags)** <br>Tags of TDAQ files.  |
| Float_t | **[_TOF](/Classes/classWaveDaqReconstruction.md#variable--tof)** <br>TW bar raw Time-Of-Flight [ns].  |
| UInt_t | **[_TotalTimeWD](/Classes/classWaveDaqReconstruction.md#variable--totaltimewd)** <br>Total acquisition time for current run [s].  |
| std::map< Int_t, std::pair< Float_t, Float_t > > | **[_TrigCalMap](/Classes/classWaveDaqReconstruction.md#variable--trigcalmap)** <br>Fragmentation trigger discriminator amplitude calibration map.  |
| Int_t | **[_TrigFN](/Classes/classWaveDaqReconstruction.md#variable--trigfn)** <br>Number of False Negative events in firmware-software quality checks.  |
| Int_t | **[_TrigFP](/Classes/classWaveDaqReconstruction.md#variable--trigfp)** <br>Number of False Positive events in firmware-software quality checks.  |
| bool | **[_TriggerEnable](/Classes/classWaveDaqReconstruction.md#variable--triggerenable)** <br>Flag for enabling studies on fragmentation trigger.  |
| Float_t | **[_TriggerRates](/Classes/classWaveDaqReconstruction.md#variable--triggerrates)** <br>Trigger rates [Hz].  |
| Float_t | **[_TriggerTh](/Classes/classWaveDaqReconstruction.md#variable--triggerth)** <br>Calibrated trigger thresholds [V].  |
| Int_t | **[_TriggerType](/Classes/classWaveDaqReconstruction.md#variable--triggertype)** <br>Trigger type of the event.  |
| Int_t | **[_TrigTN](/Classes/classWaveDaqReconstruction.md#variable--trigtn)** <br>Number of True Negative events in firmware-software quality checks.  |
| Int_t | **[_TrigTP](/Classes/classWaveDaqReconstruction.md#variable--trigtp)** <br>Number of True Positive events in firmware-software quality checks.  |
| std::vector< [WaveFormContainer](/Classes/classWaveFormContainer.md) * > | **[_WaveFormContainer](/Classes/classWaveDaqReconstruction.md#variable--waveformcontainer)** <br>Container for WaveDREAM raw waveforms and signal processing methods.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classWaveDaqReconstruction.md#variable--wdchannelmap)** <br>WaveDAQ Channel Map.  |
| [WDTag](/Classes/classWDTag.md) | **[_WDTags](/Classes/classWaveDaqReconstruction.md#variable--wdtags)** <br>Tags of WaveDREAM stand-alone files.  |


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


### function SetIncludeCLKs

```cpp
void SetIncludeCLKs()
```

Set the flag for CLK signal display. 

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


### function ClearPlots

```cpp
void ClearPlots()
```

Clear all the plots for the next event. 

### function DisplayWaveForms

```cpp
void DisplayWaveForms()
```

Display all the waveforms in their dedicated canvas. 

### function GoToPreviousEvent

```cpp
Bool_t GoToPreviousEvent()
```

Go to the previous event of the file. 

**Return**: True if previous event is found, False if it is the first event of the file 

### function PlotAll

```cpp
void PlotAll()
```

Plot all the waveforms in their canvas. 

### function SavePlots

```cpp
void SavePlots()
```

Save the plots to a file for the current event. 

### function WaitForNextEventSignal

```cpp
void WaitForNextEventSignal()
```

Wait until a command is given to the input. 

## Protected Attributes Documentation

### variable _CanvasMap

```cpp
std::map< TString, TCanvas * > _CanvasMap;
```

Map containing all the canvas for the WaveDAQ detectors. 

### variable _EventSize

```cpp
std::vector< UInt_t > _EventSize;
```

Vector of read event sizes in bytes. 

### variable _IncludeCLKs

```cpp
Bool_t _IncludeCLKs;
```

Flag to check wether to display CLK signals or not. 

### variable _WFmap

```cpp
std::map< TString, std::vector< TGraph * > > _WFmap;
```

Map containing all the TGraphs for the WaveDAQ detectors. 

-------------------------------

Updated on 2025-01-27 at 18:13:43 +0000