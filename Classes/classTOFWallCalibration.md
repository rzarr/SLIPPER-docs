---
title: TOFWallCalibration
summary: Main class used to handle the whole dE-TOF Calibration process. 

---

# TOFWallCalibration



Main class used to handle the whole dE-TOF Calibration process.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TOFWallCalibration](/Classes/classTOFWallCalibration.md#function-tofwallcalibration)**()<br>Default constructor.  |
| void | **[RunCalibration](/Classes/classTOFWallCalibration.md#function-runcalibration)**(TString OutputDir)<br>Global function that calls the calibration routines.  |
| void | **[LoadRecData](/Classes/classTOFWallCalibration.md#function-loadrecdata)**(TString InputDataDir)<br>Function used to load the reconstructed data.  |
| void | **[LoadMCRefValues](/Classes/classTOFWallCalibration.md#function-loadmcrefvalues)**(TString MCRefValuesFile)<br>Function needed to load the MC reference values for TW calibration.  |
| void | **[SetDebugMode](/Classes/classTOFWallCalibration.md#function-setdebugmode)**()<br>Function that sets the debug mode.  |

## Detailed Description

```cpp
class TOFWallCalibration;
```

Main class used to handle the whole dE-TOF Calibration process. 

This class is the main one used by the alibration executable. It handles the whole time and energy calibration of the dE-TOF system: 

## Public Functions Documentation

### function TOFWallCalibration

```cpp
TOFWallCalibration()
```

Default constructor. 

### function RunCalibration

```cpp
void RunCalibration(
    TString OutputDir
)
```

Global function that calls the calibration routines. 

**Parameters**: 

  * **OutputDir** Output directory name 


### function LoadRecData

```cpp
void LoadRecData(
    TString InputDataDir
)
```

Function used to load the reconstructed data. 

**Parameters**: 

  * **InputDataDir** Name of the input file directory 


### function LoadMCRefValues

```cpp
void LoadMCRefValues(
    TString MCRefValuesFile
)
```

Function needed to load the MC reference values for TW calibration. 

The MC table needs to contain the fields:

* campaign name (string) (to be added?)
* particle ID (string)
* beam energy (Float_t, MeV/u)
* mean dE_MC in the x and y layer (Float_t, MeV)
* mean TOF_MC in the x and y layer (Float_t, ns) MCRefValuesFileName of the MC table file 


### function SetDebugMode

```cpp
void SetDebugMode()
```

Function that sets the debug mode. 

This mode saves all the raw data histograms in a .root file inside the output directory 


-------------------------------

Updated on 2021-12-29 at 15:21:51 +0000