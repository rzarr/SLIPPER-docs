---
title: CReadBinary
summary: Class that handles all the decoding of WaveDAQ events from binary files. 

---

# CReadBinary



Class that handles all the decoding of WaveDAQ events from binary files.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CReadBinary](/Classes/classCReadBinary.md#function-creadbinary)**(std::vector< [CWaveFormContainer](/Classes/classCWaveFormContainer.md) * > * wdb_data_ptr, std::vector< [TCBDATA](/Classes/classTCBDATA.md) * > * tcb_data_ptr, std::map< UShort_t, Int_t > * _WDBIdToIdMap, std::map< UShort_t, Int_t > * ActiveBoards, Float_t * TDCTime, std::map< int, int > * TDCchMap, TH2F * hTGEN_MB, TH2F * hTGEN_frag, TH1I * hTriggerPattern, TH1I * hTriggerRates)<br>Read binary constructor.  |
| virtual | **[~CReadBinary](/Classes/classCReadBinary.md#function-~creadbinary)**()<br>Default destructor.  |
| void | **[CheckBinaryFileHeader](/Classes/classCReadBinary.md#function-checkbinaryfileheader)**(FILE * f)<br>Check that the binary file header is correct.  |
| void | **[LoadWaveDreamTimeCalibration](/Classes/classCReadBinary.md#function-loadwavedreamtimecalibration)**(FILE * f)<br>Load the time calibration of all WaveDAQ boards (WDBs and TCBs)  |
| Int_t | **[DecodeEvent](/Classes/classCReadBinary.md#function-decodeevent)**(FILE * f)<br>Decode a single WaveDAQ event.  |
| void | **[FillHistoTrigRates](/Classes/classCReadBinary.md#function-fillhistotrigrates)**()<br>Fill histogram containing the mean trigger rates for the acquistion.  |
| Bool_t | **[IsFragTriggerOn](/Classes/classCReadBinary.md#function-isfragtriggeron)**()<br>Check if the Fragmentation Trigger is enabled in the event.  |
| void | **[ResetFragTrigger](/Classes/classCReadBinary.md#function-resetfragtrigger)**()<br>Reset the fragmentation trigger value to False.  |
| Bool_t | **[ReadEvtStartWords](/Classes/classCReadBinary.md#function-readevtstartwords)**(FILE * f)<br>Read the initial words of the binary file and jump to the WaveDAQ event.  |

## Detailed Description

```cpp
class CReadBinary;
```

Class that handles all the decoding of WaveDAQ events from binary files. 

The class is capable of handling both WaveDAQ stand-alone files and TDAQ files. In this latter case, every information outside WaveDAQ events is ignored. 

## Public Functions Documentation

### function CReadBinary

```cpp
CReadBinary(
    std::vector< CWaveFormContainer * > * wdb_data_ptr,
    std::vector< TCBDATA * > * tcb_data_ptr,
    std::map< UShort_t, Int_t > * _WDBIdToIdMap,
    std::map< UShort_t, Int_t > * ActiveBoards,
    Float_t * TDCTime,
    std::map< int, int > * TDCchMap,
    TH2F * hTGEN_MB,
    TH2F * hTGEN_frag,
    TH1I * hTriggerPattern,
    TH1I * hTriggerRates
)
```

Read binary constructor. 

**Parameters**: 

  * **wdb_data_ptr** Pointer to vector of CWaveFormContainer* for WDB data 
  * **tcb_data_ptr** Pointer to vector of TCBDATA* for TCB data 
  * **_WDBIdtoIdMap** Pointer to map of WaveDREAM boards serial numbers to their indices 
  * **ActiveBoards** Pointer to map of the Active boards in the event 
  * **TDCTime** Pointer to TDCtime float 
  * **TDCchMap** Pointer to TDC channel map 
  * **hTGEN_MB** Pointer to histo filled by TGEN bank -> MB trigger 
  * **hTGEN_frag** Pointer to histo filled by TGEN bank -> Frag trigger 
  * **hTriggerPattern** Pointer to histo filled by TRGI bank -> Trigger pattern 
  * **hTriggerRates** Pointer to histo filled by TRGC bank -> Trigger rates 


Propagate all the needed pointers from main reconstruction class to ReadBinary 


### function ~CReadBinary

```cpp
virtual ~CReadBinary()
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


### function FillHistoTrigRates

```cpp
void FillHistoTrigRates()
```

Fill histogram containing the mean trigger rates for the acquistion. 

The trigger count vector is filled when decoding the TRGC bank 


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


-------------------------------

Updated on 2021-12-29 at 15:02:03 +0100