---
title: ReadBinary
summary: Class that handles all the decoding of WaveDAQ events from binary files. 

---

# ReadBinary



Class that handles all the decoding of WaveDAQ events from binary files.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ReadBinary](/Classes/classReadBinary.md#function-readbinary)**(std::vector< [WaveFormContainer](/Classes/classWaveFormContainer.md) * > * wdb_data_ptr, std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > * tcb_data_ptr, [WDChannelMap](/Classes/classWDChannelMap.md) * WDchMap, std::map< UShort_t, Int_t > * _WDBIdToIdMap, std::map< UShort_t, Int_t > * ActiveBoards)<br>Read binary constructor.  |
| virtual | **[~ReadBinary](/Classes/classReadBinary.md#function-~readbinary)**()<br>Default destructor.  |
| void | **[CheckBinaryFileHeader](/Classes/classReadBinary.md#function-checkbinaryfileheader)**(FILE * f)<br>Check that the binary file header is correct.  |
| void | **[LoadWaveDreamTimeCalibration](/Classes/classReadBinary.md#function-loadwavedreamtimecalibration)**(FILE * f)<br>Load the time calibration of all WaveDAQ boards (WDBs and TCBs)  |
| Int_t | **[DecodeEvent](/Classes/classReadBinary.md#function-decodeevent)**(FILE * f)<br>Decode a single WaveDAQ event.  |
| void | **[SetHistograms](/Classes/classReadBinary.md#function-sethistograms)**(TH2F * hTGEN_MB, TH2F * hTGEN_frag, TH1I * hTriggerPattern, TH1I * hTriggerRates)<br>Propagate the histogram pointers for all variables observed directly during decoding.  |
| void | **[FillHistoTrigRates](/Classes/classReadBinary.md#function-fillhistotrigrates)**()<br>Fill histogram containing the mean trigger rates for the acquistion.  |
| Float_t | **[GetBeamRate](/Classes/classReadBinary.md#function-getbeamrate)**()<br>Get the rate of particles crossing the setup.  |
| void | **[SaveBeamRate](/Classes/classReadBinary.md#function-savebeamrate)**(std::ofstream * ofsBeamRate)<br>Save the total time of the acquisition and the beam rate to an output file for online monitoring.  |
| Bool_t | **[IsFragTriggerOn](/Classes/classReadBinary.md#function-isfragtriggeron)**()<br>Check if the Fragmentation Trigger is enabled in the event.  |
| void | **[ResetFragTrigger](/Classes/classReadBinary.md#function-resetfragtrigger)**()<br>Reset the fragmentation trigger value to False.  |
| Bool_t | **[ReadEvtStartWords](/Classes/classReadBinary.md#function-readevtstartwords)**(FILE * f)<br>Read the initial words of the binary file and jump to the WaveDAQ event.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[ReadTDCData](/Classes/classReadBinary.md#function-readtdcdata)**(FILE * f)<br>Read the data of the TDC.  |
| void | **[ReadWDBEvent](/Classes/classReadBinary.md#function-readwdbevent)**(FILE * f)<br>Decode data of a single WaveDREAM board.  |
| void | **[ReadTCBEvent](/Classes/classReadBinary.md#function-readtcbevent)**(FILE * f)<br>Read data for a TCB.  |
| void | **[AlignTriggerCell](/Classes/classReadBinary.md#function-aligntriggercell)**()<br>Align signals using trigger cell #0 of all channels as reference.  |
| void | **[AlignSignalsRight](/Classes/classReadBinary.md#function-alignsignalsright)**()<br>Align signals to the moment a write instruction arrives to the WaveDAQ.  |
| void | **[CheckRangeOverflow](/Classes/classReadBinary.md#function-checkrangeoverflow)**(Float_t * w_ptr)<br>Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary.  |
| void | **[FillHistoTGEN](/Classes/classReadBinary.md#function-fillhistotgen)**(TH2F * hTGEN)<br>Fill Histograms with information from the TGEN bank of a TCB.  |
| void | **[FillHistoTrigPattern](/Classes/classReadBinary.md#function-fillhistotrigpattern)**(uint64_t TriggerPattern)<br>Fill histogram with trigger pattern from TRGI bank.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| int | **[Nev](/Classes/classReadBinary.md#variable-nev)** <br>Event number.  |
| std::vector< WDBBIN > | **[_bins](/Classes/classReadBinary.md#variable--bins)** <br>WaveDREAM time calibration container.  |
| std::vector< [WaveFormContainer](/Classes/classWaveFormContainer.md) * > * | **[_data_wdb](/Classes/classReadBinary.md#variable--data-wdb)** <br>WaveDREAM board data container.  |
| std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > * | **[_data_tcb](/Classes/classReadBinary.md#variable--data-tcb)** <br>TCB data container.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) * | **[_WDChannelMap](/Classes/classReadBinary.md#variable--wdchannelmap)** <br>pointer to WaveDAQ channel map  |
| std::map< UShort_t, int > * | **[_wdb_index](/Classes/classReadBinary.md#variable--wdb-index)**  |
| std::map< UShort_t, int > | **[_tcb_index](/Classes/classReadBinary.md#variable--tcb-index)** <br>Maps for WDB and TCB indexing: serial number -> index.  |
| std::map< UShort_t, int > * | **[_ActiveBoards](/Classes/classReadBinary.md#variable--activeboards)** <br>Map o the active WaveDREAM boards in the event: Serial number -> index.  |
| TH2F * | **[_hTGEN_MB](/Classes/classReadBinary.md#variable--htgen-mb)** <br>Histogram for trigger generation -> MINIMUM BIAS.  |
| TH2F * | **[_hTGEN_frag](/Classes/classReadBinary.md#variable--htgen-frag)** <br>Histogram for trigger generation -> FRAGMENTATION.  |
| TH1I * | **[_hTriggerPattern](/Classes/classReadBinary.md#variable--htriggerpattern)** <br>Histogram for trigger pattern.  |
| TH1I * | **[_hTriggerRates](/Classes/classReadBinary.md#variable--htriggerrates)** <br>Histogram for trigger rates.  |
| UInt_t | **[_TotalTime](/Classes/classReadBinary.md#variable--totaltime)** <br>Total time of the acquisition [us] -> used for trigger rates.  |
| Float_t | **[_WDAQBeamRate](/Classes/classReadBinary.md#variable--wdaqbeamrate)** <br>Rate of Minimum Bias events calculated by the WaveDAQ (beam rate, Hz)  |
| unsigned int | **[_TriggerCount](/Classes/classReadBinary.md#variable--triggercount)** <br>Array containing the counts of each trigger implemented in the WaveDAQ firmware.  |
| DRSBHEADER | **[drsbh](/Classes/classReadBinary.md#variable-drsbh)** <br>DRS board header.  |
| EHEADER | **[eh](/Classes/classReadBinary.md#variable-eh)** <br>Event header.  |
| CHEADER | **[ch](/Classes/classReadBinary.md#variable-ch)** <br>Channel header.  |
| THEADER | **[th](/Classes/classReadBinary.md#variable-th)** <br>Time header.  |
| BHEADER | **[bh](/Classes/classReadBinary.md#variable-bh)** <br>WAVEDREAM Board header.  |
| DRSCHEADER | **[drsch](/Classes/classReadBinary.md#variable-drsch)** <br>DRS channel header.  |
| unsigned short | **[voltage](/Classes/classReadBinary.md#variable-voltage)** <br>Local variable for storing waveform raw amplitude values.  |
| unsigned long | **[scaler_data](/Classes/classReadBinary.md#variable-scaler-data)**  |
| unsigned long | **[scaler_data_old](/Classes/classReadBinary.md#variable-scaler-data-old)** <br>Scaler data.  |
| unsigned long | **[scaler_time](/Classes/classReadBinary.md#variable-scaler-time)**  |
| unsigned long | **[scaler_time_old](/Classes/classReadBinary.md#variable-scaler-time-old)** <br>Scaler time.  |
| uint64_t | **[_TriggerGenerationBin](/Classes/classReadBinary.md#variable--triggergenerationbin)** <br>Array used for TGEN bank decoding.  |
| Bool_t | **[_IsFragTriggerOn](/Classes/classReadBinary.md#variable--isfragtriggeron)** <br>Boolean flag that tells if the fragmentation trigger bit was enabled in the event.  |
| Float_t * | **[_TDCTime](/Classes/classReadBinary.md#variable--tdctime)** <br>TDC time.  |
| std::map< int, int > * | **[_TDCchMap](/Classes/classReadBinary.md#variable--tdcchmap)** <br>TCH channel map.  |

## Detailed Description

```cpp
class ReadBinary;
```

Class that handles all the decoding of WaveDAQ events from binary files. 

The class is capable of handling both WaveDAQ stand-alone files and TDAQ files. In this latter case, every information outside WaveDAQ events is ignored. 

## Public Functions Documentation

### function ReadBinary

```cpp
ReadBinary(
    std::vector< WaveFormContainer * > * wdb_data_ptr,
    std::vector< TCBDATA * > * tcb_data_ptr,
    WDChannelMap * WDchMap,
    std::map< UShort_t, Int_t > * _WDBIdToIdMap,
    std::map< UShort_t, Int_t > * ActiveBoards
)
```

Read binary constructor. 

**Parameters**: 

  * **wdb_data_ptr** Pointer to vector of WaveFormContainer* for WDB data 
  * **tcb_data_ptr** Pointer to vector of TCBDATA* for TCB data 
  * **WDchMap** Pointer to WaveDAQ channel map 
  * **_WDBIdtoIdMap** Pointer to map of WaveDREAM boards serial numbers to their indices 
  * **ActiveBoards** Pointer to map of the Active boards in the event 


Propagate all the needed pointers from main reconstruction class to [ReadBinary](/Classes/classReadBinary.md)


### function ~ReadBinary

```cpp
virtual ~ReadBinary()
```

Default destructor. 

Clear all data containers and delete them 


### function CheckBinaryFileHeader

```cpp
void CheckBinaryFileHeader(
    FILE * f
)
```

Check that the binary file header is correct. 

**Parameters**: 

  * **f** Pointer to binary input file 


### function LoadWaveDreamTimeCalibration

```cpp
void LoadWaveDreamTimeCalibration(
    FILE * f
)
```

Load the time calibration of all WaveDAQ boards (WDBs and TCBs) 

**Parameters**: 

  * **f** Pointer to binary input file 


The function also takes care of resizing the corresponding data containers (vectors) 


### function DecodeEvent

```cpp
Int_t DecodeEvent(
    FILE * f
)
```

Decode a single WaveDAQ event. 

**Parameters**: 

  * **f** Pointer to input binary file 


**Return**: Trigger type of the event 

Called by the event loop inside the WavedaqReconstruction class 


### function SetHistograms

```cpp
void SetHistograms(
    TH2F * hTGEN_MB,
    TH2F * hTGEN_frag,
    TH1I * hTriggerPattern,
    TH1I * hTriggerRates
)
```

Propagate the histogram pointers for all variables observed directly during decoding. 

**Parameters**: 

  * **hTGEN_MB** Pointer to histo filled by TGEN bank -> MB trigger 
  * **hTGEN_frag** Pointer to histo filled by TGEN bank -> Frag trigger 
  * **hTriggerPattern** Pointer to histo filled by TRGI bank -> Trigger pattern 
  * **hTriggerRates** Pointer to histo filled by TRGC bank -> Trigger rates 


### function FillHistoTrigRates

```cpp
void FillHistoTrigRates()
```

Fill histogram containing the mean trigger rates for the acquistion. 

The trigger count vector is filled when decoding the TRGC bank 


### function GetBeamRate

```cpp
Float_t GetBeamRate()
```

Get the rate of particles crossing the setup. 

**Return**: Rate of Minimum Bias events calculated by the WaveDAQ [Hz] 

If either the TRGC or TRGI banks are not present in the input file, the function returns 0 


### function SaveBeamRate

```cpp
void SaveBeamRate(
    std::ofstream * ofsBeamRate
)
```

Save the total time of the acquisition and the beam rate to an output file for online monitoring. 

**Parameters**: 

  * **std::ofstream*** Pointer to output ofstream object 


### function IsFragTriggerOn

```cpp
Bool_t IsFragTriggerOn()
```

Check if the Fragmentation Trigger is enabled in the event. 

**Return**: True if the fragmentation trigger bit was enabled in the event 

### function ResetFragTrigger

```cpp
void ResetFragTrigger()
```

Reset the fragmentation trigger value to False. 

Function called from outside at the end of the event reconstruction 


### function ReadEvtStartWords

```cpp
Bool_t ReadEvtStartWords(
    FILE * f
)
```

Read the initial words of the binary file and jump to the WaveDAQ event. 

**Parameters**: 

  * **f** Pointer to input binary file 


**Return**: True if a WaveDAQ event is found before End Of File, False otherwise 

This function is used only when working with TDAQ files and is needed to skip everything outside of WaveDAQ events 


## Protected Functions Documentation

### function ReadTDCData

```cpp
Bool_t ReadTDCData(
    FILE * f
)
```

Read the data of the TDC. 

**Parameters**: 

  * **f** Pointer to input binary file 


**Return**: True if the decoding was successful 

Function copied from TDAQ software &ndash; Currently not used! 


### function ReadWDBEvent

```cpp
void ReadWDBEvent(
    FILE * f
)
```

Decode data of a single WaveDREAM board. 

**Parameters**: 

  * **f** Pointer to input binary file 


### function ReadTCBEvent

```cpp
void ReadTCBEvent(
    FILE * f
)
```

Read data for a TCB. 

**Parameters**: 

  * **f** Pointer to input binary file 


This function decodes all the data banks found inside a TCB and stores the extracted information 


### function AlignTriggerCell

```cpp
void AlignTriggerCell()
```

Align signals using trigger cell #0 of all channels as reference. 

Old algorithm, used for SC and TW boards when they have the same sampling frequency 


### function AlignSignalsRight

```cpp
void AlignSignalsRight()
```

Align signals to the moment a write instruction arrives to the WaveDAQ. 

This moment corresponds to the "right" side of the acquisition window. This alignment algorithm substitutes the old one since we now work with different sampling frequencies between WDBs 


### function CheckRangeOverflow

```cpp
void CheckRangeOverflow(
    Float_t * w_ptr
)
```

Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary. 

**Parameters**: 

  * **w_ptr** Pointer to element 1 (not 0) of the WF amplitude vector 


### function FillHistoTGEN

```cpp
void FillHistoTGEN(
    TH2F * hTGEN
)
```

Fill Histograms with information from the TGEN bank of a TCB. 

**Parameters**: 

  * **hTGEN** Pointer to histo to be filled, depends on trigger type 


### function FillHistoTrigPattern

```cpp
void FillHistoTrigPattern(
    uint64_t TriggerPattern
)
```

Fill histogram with trigger pattern from TRGI bank. 

**Parameters**: 

  * **TriggerPattern** Trigger pattern in hex format from TRGI bank 


## Protected Attributes Documentation

### variable Nev

```cpp
int Nev;
```

Event number. 

### variable _bins

```cpp
std::vector< WDBBIN > _bins;
```

WaveDREAM time calibration container. 

### variable _data_wdb

```cpp
std::vector< WaveFormContainer * > * _data_wdb;
```

WaveDREAM board data container. 

### variable _data_tcb

```cpp
std::vector< TCBDATA * > * _data_tcb;
```

TCB data container. 

### variable _WDChannelMap

```cpp
WDChannelMap * _WDChannelMap;
```

pointer to WaveDAQ channel map 

### variable _wdb_index

```cpp
std::map< UShort_t, int > * _wdb_index;
```


### variable _tcb_index

```cpp
std::map< UShort_t, int > _tcb_index;
```

Maps for WDB and TCB indexing: serial number -> index. 

### variable _ActiveBoards

```cpp
std::map< UShort_t, int > * _ActiveBoards;
```

Map o the active WaveDREAM boards in the event: Serial number -> index. 

### variable _hTGEN_MB

```cpp
TH2F * _hTGEN_MB;
```

Histogram for trigger generation -> MINIMUM BIAS. 

### variable _hTGEN_frag

```cpp
TH2F * _hTGEN_frag;
```

Histogram for trigger generation -> FRAGMENTATION. 

### variable _hTriggerPattern

```cpp
TH1I * _hTriggerPattern;
```

Histogram for trigger pattern. 

### variable _hTriggerRates

```cpp
TH1I * _hTriggerRates;
```

Histogram for trigger rates. 

### variable _TotalTime

```cpp
UInt_t _TotalTime;
```

Total time of the acquisition [us] -> used for trigger rates. 

### variable _WDAQBeamRate

```cpp
Float_t _WDAQBeamRate;
```

Rate of Minimum Bias events calculated by the WaveDAQ (beam rate, Hz) 

### variable _TriggerCount

```cpp
unsigned int _TriggerCount;
```

Array containing the counts of each trigger implemented in the WaveDAQ firmware. 

### variable drsbh

```cpp
DRSBHEADER drsbh;
```

DRS board header. 

### variable eh

```cpp
EHEADER eh;
```

Event header. 

### variable ch

```cpp
CHEADER ch;
```

Channel header. 

### variable th

```cpp
THEADER th;
```

Time header. 

### variable bh

```cpp
BHEADER bh;
```

WAVEDREAM Board header. 

### variable drsch

```cpp
DRSCHEADER drsch;
```

DRS channel header. 

### variable voltage

```cpp
unsigned short voltage;
```

Local variable for storing waveform raw amplitude values. 

### variable scaler_data

```cpp
unsigned long scaler_data;
```


### variable scaler_data_old

```cpp
unsigned long scaler_data_old = {0};
```

Scaler data. 

### variable scaler_time

```cpp
unsigned long scaler_time;
```


### variable scaler_time_old

```cpp
unsigned long scaler_time_old = 0;
```

Scaler time. 

### variable _TriggerGenerationBin

```cpp
uint64_t _TriggerGenerationBin;
```

Array used for TGEN bank decoding. 

### variable _IsFragTriggerOn

```cpp
Bool_t _IsFragTriggerOn;
```

Boolean flag that tells if the fragmentation trigger bit was enabled in the event. 

### variable _TDCTime

```cpp
Float_t * _TDCTime;
```

TDC time. 

### variable _TDCchMap

```cpp
std::map< int, int > * _TDCchMap;
```

TCH channel map. 

-------------------------------

Updated on 2022-07-11 at 14:43:07 +0000