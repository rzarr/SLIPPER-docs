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


-------------------------------

Updated on 2021-12-29 at 14:24:53 +0000