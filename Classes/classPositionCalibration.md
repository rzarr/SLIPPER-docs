---
title: PositionCalibration
summary: Main class used by the CalibratePosition executable. 

---

# PositionCalibration



Main class used by the CalibratePosition executable.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[PositionCalibration](/Classes/classPositionCalibration.md#function-positioncalibration)**(TString InputFileName)<br>Default constructor.  |
| virtual | **[~PositionCalibration](/Classes/classPositionCalibration.md#function-~positioncalibration)**()<br>Default destructor.  |
| void | **[Calibrate](/Classes/classPositionCalibration.md#function-calibrate)**()<br>Main function for position calibration.  |
| void | **[SetSavePlots](/Classes/classPositionCalibration.md#function-setsaveplots)**()<br>Declare a dedicated output rootfile where to save output plots.  |

## Detailed Description

```cpp
class PositionCalibration;
```

Main class used by the CalibratePosition executable. 

This class performs all the operations needed to produce the TW position calibration maps in SHOE format. These maps allow to reconstruct the hit position of a particle along TW bars from the time difference between the two channels of the bar. 

## Public Functions Documentation

### function PositionCalibration

```cpp
PositionCalibration(
    TString InputFileName
)
```

Default constructor. 

**Parameters**: 

  * **InputFileName** Name of the input root file 


### function ~PositionCalibration

```cpp
virtual ~PositionCalibration()
```

Default destructor. 

### function Calibrate

```cpp
void Calibrate()
```

Main function for position calibration. 

Perform the whole TW position calibration and write in output the corresponding maps in SHOE-like format 


### function SetSavePlots

```cpp
void SetSavePlots()
```

Declare a dedicated output rootfile where to save output plots. 

If this function is called, all position plots and fits are saved in an output file 


-------------------------------

Updated on 2025-01-27 at 18:20:31 +0000