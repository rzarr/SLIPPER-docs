---
title: WaveDaqReconstruction
summary: Main class used to handle the whole Reconstruction process. 

---

# WaveDaqReconstruction



Main class used to handle the whole Reconstruction process.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md#function-wavedaqreconstruction)**()<br>Default constructor.  |
| void | **[RunReconstruction](/Classes/classWaveDaqReconstruction.md#function-runreconstruction)**(std::string FileName, std::string TimeCalFileName, int nEv)<br>Perform the whole WaveDAQ reconstruction.  |
| void | **[LoadChannelMap](/Classes/classWaveDaqReconstruction.md#function-loadchannelmap)**(std::string FileName)<br>Load xml containing the channel map, i.e. the mapping between channels,boards and bar.  |
| void | **[LoadTriggerCalibration](/Classes/classWaveDaqReconstruction.md#function-loadtriggercalibration)**(std::string FileName)<br>Load the trigger calibration map.  |
| void | **[SetOutputFileName](/Classes/classWaveDaqReconstruction.md#function-setoutputfilename)**(std::string FileName)<br>Set the output file name.  |
| void | **[SetDebugMode](/Classes/classWaveDaqReconstruction.md#function-setdebugmode)**(Int_t first_ev, Int_t last_ev)<br>Activate debug mode if requested and set event range.  |
| void | **[EnableHistograms](/Classes/classWaveDaqReconstruction.md#function-enablehistograms)**()<br>Enable histogram writing in the output.  |
| void | **[SetTDAQfile](/Classes/classWaveDaqReconstruction.md#function-settdaqfile)**()<br>Signal that the file is produced through the TDAQ.  |
| void | **[SetSaveNeutrons](/Classes/classWaveDaqReconstruction.md#function-setsaveneutrons)**()<br>Set the SaveNeutrons flag to true.  |
| void | **[SetGain](/Classes/classWaveDaqReconstruction.md#function-setgain)**(Float_t Gain)<br>Set the frontend gain.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[LoopEvent](/Classes/classWaveDaqReconstruction.md#function-loopevent)**(TTree * RecTree)<br>Main event loop.  |
| void | **[AnalyzeWaveformsSC](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformssc)**(UShort_t board)<br>Analysis of SC Waveforms (WFs)  |
| void | **[AnalyzeWaveformsTW](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformstw)**(UShort_t board)<br>Analyze the WFs of TW.  |
| void | **[AnalyzeWaveformsCALO](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformscalo)**(UShort_t board)<br>Analysis of CALO Waveforms (WFs)  |
| void | **[AnalyzeWaveformsNeutrons](/Classes/classWaveDaqReconstruction.md#function-analyzewaveformsneutrons)**(UShort_t board)<br>Analysis of Neutron detector WFs.  |
| void | **[FillNeutronWaveforms](/Classes/classWaveDaqReconstruction.md#function-fillneutronwaveforms)**(UShort_t board)<br>Fill the output structures with neutron waveforms.  |
| void | **[EvalCLKJitter](/Classes/classWaveDaqReconstruction.md#function-evalclkjitter)**(int boardindex, Int_t globalch, int channel)<br>Calculate the clock phase jitter between TW and SC.  |
| Float_t | **[CLKAnalysis](/Classes/classWaveDaqReconstruction.md#function-clkanalysis)**(int boardindex, int channel) |
| void | **[AnalyzeSingleBarEvent](/Classes/classWaveDaqReconstruction.md#function-analyzesinglebarevent)**(Int_t BarId)<br>Compute the information at the bar level.  |
| Float_t | **[GetEventRawTimestamp](/Classes/classWaveDaqReconstruction.md#function-geteventrawtimestamp)**(Int_t BarId)<br>Bar timestamp of the event: mean of the channels' timestamps.  |
| Float_t | **[GetEventRawEnergy](/Classes/classWaveDaqReconstruction.md#function-geteventrawenergy)**(Int_t BarId)<br>Raw energy of the event: geometric mean of the A-B charges.  |
| Float_t | **[GetDeltaT](/Classes/classWaveDaqReconstruction.md#function-getdeltat)**(Int_t BarId)<br>Time difference between the two channels.  |
| Float_t | **[GetCRatio](/Classes/classWaveDaqReconstruction.md#function-getcratio)**(Int_t BarId)<br>Charge logarithmic ratio.  |
| Float_t | **[TimeOfFlight](/Classes/classWaveDaqReconstruction.md#function-timeofflight)**(Int_t BarId)<br>Uncorrected TOF of the event in ns.  |
| void | **[CheckFragTriggerConditions](/Classes/classWaveDaqReconstruction.md#function-checkfragtriggerconditions)**()<br>Check if the fragmentation trigger conditions are satisfied.  |
| void | **[PrintTriggerEfficiency](/Classes/classWaveDaqReconstruction.md#function-printtriggerefficiency)**()<br>Print the fragmentation trigger efficiency.  |
| void | **[GetFileTags](/Classes/classWaveDaqReconstruction.md#function-getfiletags)**(std::string FileName)<br>Get the file tags.  |
| void | **[SetOutputTreeBranches](/Classes/classWaveDaqReconstruction.md#function-setoutputtreebranches)**(TTree * RecTree)<br>Booking of the output tree branches.  |
| void | **[SetOutputNeutronWF](/Classes/classWaveDaqReconstruction.md#function-setoutputneutronwf)**(TTree * RecTree)<br>Set the output for neutron waveforms.  |
| void | **[SetOutputDataToZero](/Classes/classWaveDaqReconstruction.md#function-setoutputdatatozero)**()<br>Function called at the beginning of each event to reset the output data.  |
| void | **[CheckLoadedBoards](/Classes/classWaveDaqReconstruction.md#function-checkloadedboards)**()<br>Check and print all the loaded WaveDREAM boars.  |
| void | **[CreateHistograms](/Classes/classWaveDaqReconstruction.md#function-createhistograms)**()<br>Booking of the histograms.  |
| void | **[FillHistograms](/Classes/classWaveDaqReconstruction.md#function-fillhistograms)**()<br>Fill the histograms.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| TFile * | **[_fOut](/Classes/classWaveDaqReconstruction.md#variable--fout)** <br>Pointer to output file.  |
| std::string | **[_OutputFileName](/Classes/classWaveDaqReconstruction.md#variable--outputfilename)** <br>Output file name.  |
| std::string | **[_InputFileName](/Classes/classWaveDaqReconstruction.md#variable--inputfilename)** <br>Input file name.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classWaveDaqReconstruction.md#variable--wdchannelmap)** <br>WaveDAQ Channel Map.  |
| TGlobalToBarChIDpairMap | **[_GlobalToBarChIDpairMap](/Classes/classWaveDaqReconstruction.md#variable--globaltobarchidpairmap)** <br>Map linking the TW global channel to the bar and side ("A"/"B")  |
| Float_t | **[_Gain](/Classes/classWaveDaqReconstruction.md#variable--gain)** <br>Frontend Gain of the WaveDAQ system.  |
| bool | **[_IsTDAQ](/Classes/classWaveDaqReconstruction.md#variable--istdaq)** <br>Flag that signals if the file comes from the TDAQ.  |
| std::map< UShort_t,Int_t > | **[_BoardIdToIdMap](/Classes/classWaveDaqReconstruction.md#variable--boardidtoidmap)** <br>Map that links the WaveDREAM board serial number to its index in the [WaveFormContainer](/Classes/classWaveFormContainer.md) vector.  |
| std::map< UShort_t, Int_t > | **[_ActiveBoards](/Classes/classWaveDaqReconstruction.md#variable--activeboards)** <br>Subset of the _BoardIdtoIdMap containing only the boards w/ at least one active channel; This variable is updated at each event.  |
| [CReadBinary](/Classes/classCReadBinary.md) * | **[_BinaryReader](/Classes/classWaveDaqReconstruction.md#variable--binaryreader)** <br>Pointer to binary reader object.  |
| std::vector< [WaveFormContainer](/Classes/classWaveFormContainer.md) * > | **[_WaveFormContainer](/Classes/classWaveDaqReconstruction.md#variable--waveformcontainer)** <br>Container for WaveDREAM raw waveforms and signal processing methods.  |
| std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > | **[_TCBdata](/Classes/classWaveDaqReconstruction.md#variable--tcbdata)** <br>Container for TCB raw data.  |
| Bool_t | **[_IsPossiblePileUp](/Classes/classWaveDaqReconstruction.md#variable--ispossiblepileup)** <br>Flag for signaling possible Pile-Up events.  |
| Float_t | **[_SCTime](/Classes/classWaveDaqReconstruction.md#variable--sctime)** <br>SC raw time [ns].  |
| Float_t | **[_SCTotCharge](/Classes/classWaveDaqReconstruction.md#variable--sctotcharge)** <br>SC raw total energy loss [V*ns].  |
| Float_t | **[_SCPedestal](/Classes/classWaveDaqReconstruction.md#variable--scpedestal)** <br>SC channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_SCPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--scpedestalrms)** <br>SC channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_SCAmplitude](/Classes/classWaveDaqReconstruction.md#variable--scamplitude)** <br>SC channel amplitude (<0) [V] **DEBUG ONLY** |
| Float_t | **[_SCCharge](/Classes/classWaveDaqReconstruction.md#variable--sccharge)** <br>SC channel integral charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_SCRiseTime](/Classes/classWaveDaqReconstruction.md#variable--scrisetime)** <br>SC channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_CPedestal](/Classes/classWaveDaqReconstruction.md#variable--cpedestal)** <br>TW global channel pedestal [V] **DEBUG ONLY** |
| Float_t | **[_CPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--cpedestalrms)** <br>TW global channel pedestal RMS [V] **DEBUG ONLY** |
| Float_t | **[_CAmplitude](/Classes/classWaveDaqReconstruction.md#variable--camplitude)** <br>TW global channel amplitude [V] **DEBUG ONLY** |
| Float_t | **[_CCharge](/Classes/classWaveDaqReconstruction.md#variable--ccharge)** <br>TW global channel total charge [V*ns] **DEBUG ONLY** |
| Float_t | **[_CRiseTime](/Classes/classWaveDaqReconstruction.md#variable--crisetime)** <br>TW global channel rise time [ns] **DEBUG ONLY** |
| Float_t | **[_CTimestamps](/Classes/classWaveDaqReconstruction.md#variable--ctimestamps)** <br>TW global channel raw time [ns] **DEBUG ONLY** |
| Float_t | **[_CTimestampsCorrJit](/Classes/classWaveDaqReconstruction.md#variable--ctimestampscorrjit)** <br>TW global channel time with CLK jitter correction [ns] **DEBUG ONLY** |
| Float_t | **[_CLK_Jitter](/Classes/classWaveDaqReconstruction.md#variable--clk-jitter)** <br>TW global channel CLK jitter correction [ns] **DEBUG ONLY** |
| Float_t | **[_CLK_phase](/Classes/classWaveDaqReconstruction.md#variable--clk-phase)** <br>CLK phase of all boards [ns] **DEBUG ONLY** |
| Float_t | **[_SC_CLK_phase](/Classes/classWaveDaqReconstruction.md#variable--sc-clk-phase)** <br>Phase of Start Counter CLK [ns].  |
| Float_t | **[_CPedA](/Classes/classWaveDaqReconstruction.md#variable--cpeda)** <br>TW channel "A" pedestal [V].  |
| Float_t | **[_CPedB](/Classes/classWaveDaqReconstruction.md#variable--cpedb)** <br>TW channel "B" pedestal [V].  |
| Float_t | **[_CPedRMSA](/Classes/classWaveDaqReconstruction.md#variable--cpedrmsa)** <br>TW channel "A" pedestal RMS [V].  |
| Float_t | **[_CPedRMSB](/Classes/classWaveDaqReconstruction.md#variable--cpedrmsb)** <br>TW channel "B" pedestal RMS [V].  |
| Float_t | **[_CAmpA](/Classes/classWaveDaqReconstruction.md#variable--campa)** <br>TW channel "A" amplitude (<0) [V].  |
| Float_t | **[_CAmpB](/Classes/classWaveDaqReconstruction.md#variable--campb)** <br>TW channel "B" amplitude (<0) [V].  |
| Float_t | **[_CChargeA](/Classes/classWaveDaqReconstruction.md#variable--cchargea)** <br>TW channel "A" integral charge [V*ns].  |
| Float_t | **[_CChargeB](/Classes/classWaveDaqReconstruction.md#variable--cchargeb)** <br>TW channel "B" integral charge [V*ns].  |
| Float_t | **[_CRiseTimeA](/Classes/classWaveDaqReconstruction.md#variable--crisetimea)** <br>TW channel "A" rise time [ns].  |
| Float_t | **[_CRiseTimeB](/Classes/classWaveDaqReconstruction.md#variable--crisetimeb)** <br>TW channel "B" rise time [ns].  |
| Float_t | **[_CTimeA](/Classes/classWaveDaqReconstruction.md#variable--ctimea)** <br>TW channel "A" time with CLK jitter correction [ns].  |
| Float_t | **[_CTimeB](/Classes/classWaveDaqReconstruction.md#variable--ctimeb)** <br>TW channel "B" time with CLK jitter correction [ns].  |
| Float_t | **[_CALOPedestal](/Classes/classWaveDaqReconstruction.md#variable--calopedestal)** <br>CALO crystal pedestal [V].  |
| Float_t | **[_CALOPedestalRMS](/Classes/classWaveDaqReconstruction.md#variable--calopedestalrms)** <br>CALO crystal pedestal RMS [V].  |
| Float_t | **[_CALOAmplitude](/Classes/classWaveDaqReconstruction.md#variable--caloamplitude)** <br>CALO crystal amplitude (<0) [V].  |
| Float_t | **[_CALOCharge](/Classes/classWaveDaqReconstruction.md#variable--calocharge)** <br>CALO crystal integral charge [V*ns].  |
| Float_t | **[_CALORiseTime](/Classes/classWaveDaqReconstruction.md#variable--calorisetime)** <br>CALO crystal rise time [ns].  |
| Float_t | **[_CALOTimestamps](/Classes/classWaveDaqReconstruction.md#variable--calotimestamps)** <br>CALO crystal raw time [ns].  |
| Float_t | **[_CALOTimestampsCorrJit](/Classes/classWaveDaqReconstruction.md#variable--calotimestampscorrjit)** <br>CALO crystal time with CLK jitter correction [ns].  |
| Float_t | **[_NFPed](/Classes/classWaveDaqReconstruction.md#variable--nfped)** <br>Neutron Fast channel pedestal [V].  |
| Float_t | **[_NFPedRMS](/Classes/classWaveDaqReconstruction.md#variable--nfpedrms)** <br>Neutron Fast channel pedestal RMS [V].  |
| Float_t | **[_NFAmp](/Classes/classWaveDaqReconstruction.md#variable--nfamp)** <br>Neutron Fast channel amplitude (<0) [V].  |
| Float_t | **[_NFCharge](/Classes/classWaveDaqReconstruction.md#variable--nfcharge)** <br>Neutron Fast channel integral charge [V*ns].  |
| Float_t | **[_NFTime](/Classes/classWaveDaqReconstruction.md#variable--nftime)** <br>Neutron Fast channel raw time [ns].  |
| Float_t | **[_NFRiseTime](/Classes/classWaveDaqReconstruction.md#variable--nfrisetime)** <br>Neutron Fast channel rise time [ns].  |
| Float_t | **[_NSPed](/Classes/classWaveDaqReconstruction.md#variable--nsped)** <br>Neutron Slow channel pedestal [V].  |
| Float_t | **[_NSPedRMS](/Classes/classWaveDaqReconstruction.md#variable--nspedrms)** <br>Neutron Slow channel pedestal RMS [V].  |
| Float_t | **[_NSAmp](/Classes/classWaveDaqReconstruction.md#variable--nsamp)** <br>Neutron Slow channel amplitude (<0) [V].  |
| Float_t | **[_NSCharge](/Classes/classWaveDaqReconstruction.md#variable--nscharge)** <br>Neutron Slow channel integral charge [V*ns].  |
| Float_t | **[_NSTime](/Classes/classWaveDaqReconstruction.md#variable--nstime)** <br>Neutron Slow channel raw time [ns].  |
| Float_t | **[_NSRiseTime](/Classes/classWaveDaqReconstruction.md#variable--nsrisetime)** <br>Neutron Slow channel rise time [ns].  |
| Float_t | **[_BCharge](/Classes/classWaveDaqReconstruction.md#variable--bcharge)** <br>TW bar charge (raw energy loss) [V*ns].  |
| Float_t | **[_BTimestamps](/Classes/classWaveDaqReconstruction.md#variable--btimestamps)** <br>TW bar raw time [ns].  |
| Float_t | **[_BDeltaT](/Classes/classWaveDaqReconstruction.md#variable--bdeltat)** <br>TW bar raw time difference between channels "A" and "B" [ns].  |
| Float_t | **[_BCratio](/Classes/classWaveDaqReconstruction.md#variable--bcratio)** <br>TW bar logarithmic ratio of charge "A" over charge "B" [ns].  |
| Float_t | **[_TOF](/Classes/classWaveDaqReconstruction.md#variable--tof)** <br>TW bar raw Time-Of-Flight [ns].  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NS_WF](/Classes/classWaveDaqReconstruction.md#variable--ns-wf)** <br>Container for signals of Slow channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| [NeutronWF](/Classes/classNeutronWF.md) * | **[_NF_WF](/Classes/classWaveDaqReconstruction.md#variable--nf-wf)** <br>Container for signals of Fast channels of Neutron detectors (only used when _SaveNeutrons is True)  |
| UShort_t | **[_NbSlow](/Classes/classWaveDaqReconstruction.md#variable--nbslow)** <br>Serial number of Neutron Slow board.  |
| UShort_t | **[_NbFast](/Classes/classWaveDaqReconstruction.md#variable--nbfast)** <br>Serial number of Neutron Fast board.  |
| Bool_t | **[_NeutronOn](/Classes/classWaveDaqReconstruction.md#variable--neutronon)** <br>Flag for Neutron detectors status in the event.  |
| Bool_t | **[_SaveNeutrons](/Classes/classWaveDaqReconstruction.md#variable--saveneutrons)** <br>Global flag that checks if the neutron waveforms have to be saved or not in the output.  |
| Int_t | **[_TriggerType](/Classes/classWaveDaqReconstruction.md#variable--triggertype)** <br>Trigger type of the event.  |
| Bool_t | **[_IsFragTriggerOn](/Classes/classWaveDaqReconstruction.md#variable--isfragtriggeron)** <br>Flag that tells if the fragmentation trigger fired in the event.  |
| Int_t | **[_TrigTP](/Classes/classWaveDaqReconstruction.md#variable--trigtp)** <br>Number of True Positive events in firmware-software quality checks.  |
| Int_t | **[_TrigFP](/Classes/classWaveDaqReconstruction.md#variable--trigfp)** <br>Number of False Positive events in firmware-software quality checks.  |
| Int_t | **[_TrigTN](/Classes/classWaveDaqReconstruction.md#variable--trigtn)** <br>Number of True Negative events in firmware-software quality checks.  |
| Int_t | **[_TrigFN](/Classes/classWaveDaqReconstruction.md#variable--trigfn)** <br>Number of False Negative events in firmware-software quality checks.  |
| std::map< Int_t, std::pair< Float_t, Float_t > > | **[_TrigCalMap](/Classes/classWaveDaqReconstruction.md#variable--trigcalmap)** <br>Fragmentation trigger discriminator amplitude calibration map.  |
| Float_t | **[_TriggerTh](/Classes/classWaveDaqReconstruction.md#variable--triggerth)** <br>Calibrated trigger thresholds [V].  |
| [WDTag](/Classes/classWDTag.md) | **[_WDTags](/Classes/classWaveDaqReconstruction.md#variable--wdtags)** <br>Tags of WaveDREAM stand-alone files.  |
| [TDAQTag](/Classes/classTDAQTag.md) | **[_TDAQTags](/Classes/classWaveDaqReconstruction.md#variable--tdaqtags)** <br>Tags of TDAQ files.  |
| bool | **[_Debug](/Classes/classWaveDaqReconstruction.md#variable--debug)** <br>Global debug flag.  |
| bool | **[_EnableHisto](/Classes/classWaveDaqReconstruction.md#variable--enablehisto)** <br>Flag for enabling histogram saving.  |
| bool | **[_TriggerEnable](/Classes/classWaveDaqReconstruction.md#variable--triggerenable)** <br>Flag for enabling studies on fragmentation trigger.  |
| int | **[_FirstEventToSave](/Classes/classWaveDaqReconstruction.md#variable--firsteventtosave)** <br>First event saved in Debug Mode.  |
| int | **[_LastEventToSave](/Classes/classWaveDaqReconstruction.md#variable--lasteventtosave)** <br>Last event saved in Debug Mode.  |
| int | **[_Event](/Classes/classWaveDaqReconstruction.md#variable--event)** <br>Current event number.  |
| TH1F * | **[_hitmap_Bars](/Classes/classWaveDaqReconstruction.md#variable--hitmap-bars)** <br>1D Hitmap of TW bars **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Rear](/Classes/classWaveDaqReconstruction.md#variable--hitmap-channels-rear)** <br>1D Hitmap of TW channels in rear layer **HISTOGRAM** |
| TH1F * | **[_hitmap_Channels_Front](/Classes/classWaveDaqReconstruction.md#variable--hitmap-channels-front)** <br>1D Hitmap of TW channels in front layer **HISTOGRAM** |
| TH2F * | **[_hitmap_MB](/Classes/classWaveDaqReconstruction.md#variable--hitmap-mb)** <br>2D Hitmap of TW for Minimum Bias events **HISTOGRAM** |
| TH2F * | **[_hitmap_frag](/Classes/classWaveDaqReconstruction.md#variable--hitmap-frag)** <br>2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM** |
| TH2F * | **[_hitmap_all](/Classes/classWaveDaqReconstruction.md#variable--hitmap-all)** <br>2D Hitmap of TW for all events **HISTOGRAM** |
| TH2F * | **[_hTGEN_MB](/Classes/classWaveDaqReconstruction.md#variable--htgen-mb)** <br>Trigger generation (TGEN) for Minimum Bias Events **HISTOGRAM** |
| TH2F * | **[_hTGEN_frag](/Classes/classWaveDaqReconstruction.md#variable--htgen-frag)** <br>Trigger generation (TGEN) for Fragmentation Trigger Events **HISTOGRAM** |
| TH1I * | **[_hTriggerPattern](/Classes/classWaveDaqReconstruction.md#variable--htriggerpattern)** <br>Trigger pattern (TRGI) **HISTOGRAM** |
| TH1I * | **[_hTriggerRates](/Classes/classWaveDaqReconstruction.md#variable--htriggerrates)** <br>Trigger rates (TRGC) **HISTOGRAM** |
| TH1F ** | **[_hTrigAmp](/Classes/classWaveDaqReconstruction.md#variable--htrigamp)** <br>Trigger amplitude of Fragmentation trigger channels **HISTOGRAM** |
| TH1I * | **[_hCALOMultiplicity](/Classes/classWaveDaqReconstruction.md#variable--hcalomultiplicity)** <br>Multiplicity of CALO crystals **HISTOGRAM** |

## Detailed Description

```cpp
class WaveDaqReconstruction;
```

Main class used to handle the whole Reconstruction process. 

This class is the main one used by the Reconstruction executable. It handles the whole signal processing and contains:

* Input/Output file setting
* Channel Map xml configuration loading
* Raw waveform and trigger information decoding
* Signal processing
* Reconstruction of higher level variables (such as TW bar variables and Time-Of-Flight) 

## Public Functions Documentation

### function WaveDaqReconstruction

```cpp
WaveDaqReconstruction()
```

Default constructor. 

Set some global variables to initial dummy values 


### function RunReconstruction

```cpp
void RunReconstruction(
    std::string FileName,
    std::string TimeCalFileName,
    int nEv
)
```

Perform the whole WaveDAQ reconstruction. 

**Parameters**: 

  * **FileName** Name of the input binary file 
  * **TimeCalFileName** Name of the time calibration file. Equal to the previous parameter for WaveDAQ files 
  * **nEv** Number of events to be processed (optional, default=-1) 


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


### function SetOutputFileName

```cpp
void SetOutputFileName(
    std::string FileName
)
```

Set the output file name. 

**Parameters**: 

  * **FileName** Name of the output file 


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


### function EnableHistograms

```cpp
void EnableHistograms()
```

Enable histogram writing in the output. 

### function SetTDAQfile

```cpp
void SetTDAQfile()
```

Signal that the file is produced through the TDAQ. 

### function SetSaveNeutrons

```cpp
void SetSaveNeutrons()
```

Set the SaveNeutrons flag to true. 

### function SetGain

```cpp
void SetGain(
    Float_t Gain
)
```

Set the frontend gain. 

**Parameters**: 

  * **Gain** Frontend gain of the acquisition 


## Protected Functions Documentation

### function LoopEvent

```cpp
void LoopEvent(
    TTree * RecTree
)
```

Main event loop. 

**Parameters**: 

  * **RecTree** Pointer to the output tree 


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


### function FillNeutronWaveforms

```cpp
void FillNeutronWaveforms(
    UShort_t board
)
```

Fill the output structures with neutron waveforms. 

**Parameters**: 

  * **board** Board serial number 


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


### function CLKAnalysis

```cpp
Float_t CLKAnalysis(
    int boardindex,
    int channel
)
```


### function AnalyzeSingleBarEvent

```cpp
void AnalyzeSingleBarEvent(
    Int_t BarId
)
```

Compute the information at the bar level. 

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


### function GetEventRawEnergy

```cpp
Float_t GetEventRawEnergy(
    Int_t BarId
)
```

Raw energy of the event: geometric mean of the A-B charges. 

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


### function GetCRatio

```cpp
Float_t GetCRatio(
    Int_t BarId
)
```

Charge logarithmic ratio. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function TimeOfFlight

```cpp
Float_t TimeOfFlight(
    Int_t BarId
)
```

Uncorrected TOF of the event in ns. 

**Parameters**: 

  * **BarId** Id of the TW bar to analyze 


### function CheckFragTriggerConditions

```cpp
void CheckFragTriggerConditions()
```

Check if the fragmentation trigger conditions are satisfied. 

### function PrintTriggerEfficiency

```cpp
void PrintTriggerEfficiency()
```

Print the fragmentation trigger efficiency. 

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


### function SetOutputTreeBranches

```cpp
void SetOutputTreeBranches(
    TTree * RecTree
)
```

Booking of the output tree branches. 

**Parameters**: 

  * **RecTree** Pointer to the output tree 


### function SetOutputNeutronWF

```cpp
void SetOutputNeutronWF(
    TTree * RecTree
)
```

Set the output for neutron waveforms. 

**Parameters**: 

  * **RecTree** Pointer to output tree 


### function SetOutputDataToZero

```cpp
void SetOutputDataToZero()
```

Function called at the beginning of each event to reset the output data. 

### function CheckLoadedBoards

```cpp
void CheckLoadedBoards()
```

Check and print all the loaded WaveDREAM boars. 

### function CreateHistograms

```cpp
void CreateHistograms()
```

Booking of the histograms. 

### function FillHistograms

```cpp
void FillHistograms()
```

Fill the histograms. 

## Protected Attributes Documentation

### variable _fOut

```cpp
TFile * _fOut;
```

Pointer to output file. 

### variable _OutputFileName

```cpp
std::string _OutputFileName;
```

Output file name. 

### variable _InputFileName

```cpp
std::string _InputFileName;
```

Input file name. 

### variable _WDChannelMap

```cpp
WDChannelMap _WDChannelMap;
```

WaveDAQ Channel Map. 

### variable _GlobalToBarChIDpairMap

```cpp
TGlobalToBarChIDpairMap _GlobalToBarChIDpairMap;
```

Map linking the TW global channel to the bar and side ("A"/"B") 

### variable _Gain

```cpp
Float_t _Gain;
```

Frontend Gain of the WaveDAQ system. 

### variable _IsTDAQ

```cpp
bool _IsTDAQ;
```

Flag that signals if the file comes from the TDAQ. 

### variable _BoardIdToIdMap

```cpp
std::map< UShort_t,Int_t > _BoardIdToIdMap;
```

Map that links the WaveDREAM board serial number to its index in the [WaveFormContainer](/Classes/classWaveFormContainer.md) vector. 

### variable _ActiveBoards

```cpp
std::map< UShort_t, Int_t > _ActiveBoards;
```

Subset of the _BoardIdtoIdMap containing only the boards w/ at least one active channel; This variable is updated at each event. 

### variable _BinaryReader

```cpp
CReadBinary * _BinaryReader;
```

Pointer to binary reader object. 

### variable _WaveFormContainer

```cpp
std::vector< WaveFormContainer * > _WaveFormContainer;
```

Container for WaveDREAM raw waveforms and signal processing methods. 

### variable _TCBdata

```cpp
std::vector< TCBDATA * > _TCBdata;
```

Container for TCB raw data. 

### variable _IsPossiblePileUp

```cpp
Bool_t _IsPossiblePileUp;
```

Flag for signaling possible Pile-Up events. 

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

### variable _SCRiseTime

```cpp
Float_t _SCRiseTime;
```

SC channel rise time [ns] **DEBUG ONLY**

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

### variable _CAmplitude

```cpp
Float_t _CAmplitude;
```

TW global channel amplitude [V] **DEBUG ONLY**

### variable _CCharge

```cpp
Float_t _CCharge;
```

TW global channel total charge [V*ns] **DEBUG ONLY**

### variable _CRiseTime

```cpp
Float_t _CRiseTime;
```

TW global channel rise time [ns] **DEBUG ONLY**

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

### variable _SC_CLK_phase

```cpp
Float_t _SC_CLK_phase;
```

Phase of Start Counter CLK [ns]. 

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

### variable _NFTime

```cpp
Float_t _NFTime;
```

Neutron Fast channel raw time [ns]. 

### variable _NFRiseTime

```cpp
Float_t _NFRiseTime;
```

Neutron Fast channel rise time [ns]. 

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

### variable _NSTime

```cpp
Float_t _NSTime;
```

Neutron Slow channel raw time [ns]. 

### variable _NSRiseTime

```cpp
Float_t _NSRiseTime;
```

Neutron Slow channel rise time [ns]. 

### variable _BCharge

```cpp
Float_t _BCharge;
```

TW bar charge (raw energy loss) [V*ns]. 

### variable _BTimestamps

```cpp
Float_t _BTimestamps;
```

TW bar raw time [ns]. 

### variable _BDeltaT

```cpp
Float_t _BDeltaT;
```

TW bar raw time difference between channels "A" and "B" [ns]. 

### variable _BCratio

```cpp
Float_t _BCratio;
```

TW bar logarithmic ratio of charge "A" over charge "B" [ns]. 

### variable _TOF

```cpp
Float_t _TOF;
```

TW bar raw Time-Of-Flight [ns]. 

### variable _NS_WF

```cpp
NeutronWF * _NS_WF;
```

Container for signals of Slow channels of Neutron detectors (only used when _SaveNeutrons is True) 

### variable _NF_WF

```cpp
NeutronWF * _NF_WF;
```

Container for signals of Fast channels of Neutron detectors (only used when _SaveNeutrons is True) 

### variable _NbSlow

```cpp
UShort_t _NbSlow;
```

Serial number of Neutron Slow board. 

### variable _NbFast

```cpp
UShort_t _NbFast;
```

Serial number of Neutron Fast board. 

### variable _NeutronOn

```cpp
Bool_t _NeutronOn;
```

Flag for Neutron detectors status in the event. 

### variable _SaveNeutrons

```cpp
Bool_t _SaveNeutrons;
```

Global flag that checks if the neutron waveforms have to be saved or not in the output. 

### variable _TriggerType

```cpp
Int_t _TriggerType;
```

Trigger type of the event. 

### variable _IsFragTriggerOn

```cpp
Bool_t _IsFragTriggerOn;
```

Flag that tells if the fragmentation trigger fired in the event. 

### variable _TrigTP

```cpp
Int_t _TrigTP;
```

Number of True Positive events in firmware-software quality checks. 

### variable _TrigFP

```cpp
Int_t _TrigFP;
```

Number of False Positive events in firmware-software quality checks. 

### variable _TrigTN

```cpp
Int_t _TrigTN;
```

Number of True Negative events in firmware-software quality checks. 

### variable _TrigFN

```cpp
Int_t _TrigFN;
```

Number of False Negative events in firmware-software quality checks. 

### variable _TrigCalMap

```cpp
std::map< Int_t, std::pair< Float_t, Float_t > > _TrigCalMap;
```

Fragmentation trigger discriminator amplitude calibration map. 

### variable _TriggerTh

```cpp
Float_t _TriggerTh;
```

Calibrated trigger thresholds [V]. 

### variable _WDTags

```cpp
WDTag _WDTags;
```

Tags of WaveDREAM stand-alone files. 

### variable _TDAQTags

```cpp
TDAQTag _TDAQTags;
```

Tags of TDAQ files. 

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

### variable _TriggerEnable

```cpp
bool _TriggerEnable;
```

Flag for enabling studies on fragmentation trigger. 

### variable _FirstEventToSave

```cpp
int _FirstEventToSave;
```

First event saved in Debug Mode. 

### variable _LastEventToSave

```cpp
int _LastEventToSave;
```

Last event saved in Debug Mode. 

### variable _Event

```cpp
int _Event;
```

Current event number. 

### variable _hitmap_Bars

```cpp
TH1F * _hitmap_Bars;
```

1D Hitmap of TW bars **HISTOGRAM**

### variable _hitmap_Channels_Rear

```cpp
TH1F * _hitmap_Channels_Rear;
```

1D Hitmap of TW channels in rear layer **HISTOGRAM**

### variable _hitmap_Channels_Front

```cpp
TH1F * _hitmap_Channels_Front;
```

1D Hitmap of TW channels in front layer **HISTOGRAM**

### variable _hitmap_MB

```cpp
TH2F * _hitmap_MB;
```

2D Hitmap of TW for Minimum Bias events **HISTOGRAM**

### variable _hitmap_frag

```cpp
TH2F * _hitmap_frag;
```

2D Hitmap of TW for Fragmentation Trigger events **HISTOGRAM**

### variable _hitmap_all

```cpp
TH2F * _hitmap_all;
```

2D Hitmap of TW for all events **HISTOGRAM**

### variable _hTGEN_MB

```cpp
TH2F * _hTGEN_MB = nullptr;
```

Trigger generation (TGEN) for Minimum Bias Events **HISTOGRAM**

### variable _hTGEN_frag

```cpp
TH2F * _hTGEN_frag = nullptr;
```

Trigger generation (TGEN) for Fragmentation Trigger Events **HISTOGRAM**

### variable _hTriggerPattern

```cpp
TH1I * _hTriggerPattern = nullptr;
```

Trigger pattern (TRGI) **HISTOGRAM**

### variable _hTriggerRates

```cpp
TH1I * _hTriggerRates = nullptr;
```

Trigger rates (TRGC) **HISTOGRAM**

### variable _hTrigAmp

```cpp
TH1F ** _hTrigAmp = new TH1F*[NUMBEROFTRIGGERCHANNELS];
```

Trigger amplitude of Fragmentation trigger channels **HISTOGRAM**

### variable _hCALOMultiplicity

```cpp
TH1I * _hCALOMultiplicity;
```

Multiplicity of CALO crystals **HISTOGRAM**

-------------------------------

Updated on 2022-03-04 at 14:25:58 +0000