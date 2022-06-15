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

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[InitHists](/Classes/classTOFWallCalibration.md#function-inithists)**(TLayer Layer)<br>Function used to initialize the histograms of a new Particle-BeamEnergy pair.  |
| void | **[LoadSingleFileData](/Classes/classTOFWallCalibration.md#function-loadsinglefiledata)**(TString FileName)<br>Load the raw data from a single root file and store them in the histograms of the class.  |
| void | **[EnergyCalibration](/Classes/classTOFWallCalibration.md#function-energycalibration)**(TString OutputDir)<br>Function that contains the routine used for the energy calibration of the TW.  |
| void | **[CalibrateLayerDeltaE](/Classes/classTOFWallCalibration.md#function-calibratelayerdeltae)**(std::ofstream * ofsSHOE, TLayer layer, TString OutputDir, TFile * fOut)<br>Function containing the energy calibration routine used for one TW layer.  |
| void | **[TOFCalibration](/Classes/classTOFWallCalibration.md#function-tofcalibration)**(TString OutputDir)<br>Function that contains the routine used for the TOF calibration of the dE-TOF.  |
| void | **[CalibrateLayerTOF](/Classes/classTOFWallCalibration.md#function-calibratelayertof)**(std::ofstream * ofsSHOE, PartEnPairType PartEn, TLayer layer, TString OutputDir, TFile * fOut)<br>Function containing the actual TOF calibration routine for single layers.  |
| void | **[SaveRawHistograms](/Classes/classTOFWallCalibration.md#function-saverawhistograms)**(TString OutputDir)<br>Additional function that can be used to save the raw data histograms to a .root file in the outuput directory.  |
| void | **[ClearData](/Classes/classTOFWallCalibration.md#function-cleardata)**(TLayer layer)<br>Function used to clear histogram data.  |
| Int_t | **[CalculatePositionID](/Classes/classTOFWallCalibration.md#function-calculatepositionid)**(Int_t XBar, Int_t YBar)<br>Function that calcualtes the Position ID form bar numbers.  |
| void | **[CalculatePosIDtoBarsMap](/Classes/classTOFWallCalibration.md#function-calculateposidtobarsmap)**()<br>Function that fills the _PosIDtoXYBarsMap map with the actual values.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< PartEnPairType, MCRefType > | **[_MCRef](/Classes/classTOFWallCalibration.md#variable--mcref)** <br>Map used to store MC reference values.  |
| std::map< Int_t, std::pair< Int_t, Int_t > > | **[_PosIDtoXYBarsMap](/Classes/classTOFWallCalibration.md#variable--posidtoxybarsmap)** <br>Map used to store the X and Y bars corresponding to a TW position.  |
| std::vector< PartEnPairType > | **[_PartEnPairsMC](/Classes/classTOFWallCalibration.md#variable--partenpairsmc)** <br>Vector storing the beams found in the MC table; Used to control the MC table, initialize histograms and deallocate memory at the end.  |
| std::vector< PartEnPairType > | **[_PartEnPairsData](/Classes/classTOFWallCalibration.md#variable--partenpairsdata)** <br>Vector storing the beams found in data; Used to run the calibration on the beams found.  |
| std::map< PartEnPairType, std::vector< TH1F * > > | **[_hQ](/Classes/classTOFWallCalibration.md#variable--hq)** <br>Raw energy loss histograms for each position of both TW layers (0=LayerY, 1=LayerX). Key is the beam type (particle-energy)  |
| std::map< PartEnPairType, std::vector< TH1F * > > | **[_hTOF](/Classes/classTOFWallCalibration.md#variable--htof)** <br>Raw Time-Of-Flight histograms for each position of both TW layers (0=LayerY, 1=LayerX). Key is the beam type (particle-energy)  |
| TF1 * | **[_funcdECal](/Classes/classTOFWallCalibration.md#variable--funcdecal)** <br>Function used for the light output model -> Energy calibration.  |
| Bool_t | **[_Debug](/Classes/classTOFWallCalibration.md#variable--debug)** <br>Flag used to set debug mode.  |

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

**Parameters**: 

  * **MCRefValuesFile** Name of the MC table file 


The MC table needs to contain the fields:

* campaign name (string) (to be added?)
* particle ID (string)
* beam energy (Float_t, MeV/u)
* mean dE_MC in the x and y layer (Float_t, MeV)
* mean TOF_MC in the x and y layer (Float_t, ns)


### function SetDebugMode

```cpp
void SetDebugMode()
```

Function that sets the debug mode. 

This mode saves all the raw data histograms in a .root file inside the output directory 


## Protected Functions Documentation

### function InitHists

```cpp
void InitHists(
    TLayer Layer
)
```

Function used to initialize the histograms of a new Particle-BeamEnergy pair. 

**Parameters**: 

  * **layer** TW layer 


### function LoadSingleFileData

```cpp
void LoadSingleFileData(
    TString FileName
)
```

Load the raw data from a single root file and store them in the histograms of the class. 

**Parameters**: 

  * **FileName** ROOT input file name 


### function EnergyCalibration

```cpp
void EnergyCalibration(
    TString OutputDir
)
```

Function that contains the routine used for the energy calibration of the TW. 

**Parameters**: 

  * **OutputDir** Output directory name, where maps are saved 


The function saves a calibration map for each TW layer where every line contains:

* Position ID
* p0, "gain" factor of the Birks model [a.u./MeV]
* p1, "saturation" parameter of the Birks model [1/MeV]
* one flag indicating if the fit was successful. In the current version: -> 0 = not good for low statistics/number of beams -> 1 = good statistics, both CNAO and GSI data -> 2 = good statistics, only CNAO data -> 3 = good statistics, fit was unsuccessful anyway (high chi2)


### function CalibrateLayerDeltaE

```cpp
void CalibrateLayerDeltaE(
    std::ofstream * ofsSHOE,
    TLayer layer,
    TString OutputDir,
    TFile * fOut
)
```

Function containing the energy calibration routine used for one TW layer. 

**Parameters**: 

  * **ofsSHOE** Pointer to SHOE-like ofstream 
  * **layer** TW layer 
  * **OutputDir** Name of output directory 
  * **fOut** Pointer to output file used to store debug histograms 


### function TOFCalibration

```cpp
void TOFCalibration(
    TString OutputDir
)
```

Function that contains the routine used for the TOF calibration of the dE-TOF. 

**Parameters**: 

  * **OutputDir** Output directory name, where maps are saved 


The maps contain:

* Position ID
* Bar ID for layer X
* Bar ID for layer Y
* Time difference between the raw TOF and the associated MC reference value [ns]
* DeltaT2 [ns] -> TO BE DEFINED!!


### function CalibrateLayerTOF

```cpp
void CalibrateLayerTOF(
    std::ofstream * ofsSHOE,
    PartEnPairType PartEn,
    TLayer layer,
    TString OutputDir,
    TFile * fOut
)
```

Function containing the actual TOF calibration routine for single layers. 

**Parameters**: 

  * **ofsSHOE** Pointer to SHOE-like ofstream 
  * **PartEn** Beam identifier (partID, En) 
  * **layer** TW layer 
  * **OutputDir** Name of output directory 
  * **fOut** Pointer to output file for debug histograms 


### function SaveRawHistograms

```cpp
void SaveRawHistograms(
    TString OutputDir
)
```

Additional function that can be used to save the raw data histograms to a .root file in the outuput directory. 

**Parameters**: 

  * **OutputDir** Output directory name 


CURRENTLY USED FOR DEBUG PURPOSES IN SHOE 


### function ClearData

```cpp
void ClearData(
    TLayer layer
)
```

Function used to clear histogram data. 

**Parameters**: 

  * **layer** TW layer 


### function CalculatePositionID

```cpp
Int_t CalculatePositionID(
    Int_t XBar,
    Int_t YBar
)
```

Function that calcualtes the Position ID form bar numbers. 

**Parameters**: 

  * **XBar** Id of the X layer bar 
  * **YBar** Id of the Y layer bar 


**Return**: Id of the corresponding TW position 

Modify if we change PosID convention 


### function CalculatePosIDtoBarsMap

```cpp
void CalculatePosIDtoBarsMap()
```

Function that fills the _PosIDtoXYBarsMap map with the actual values. 

## Protected Attributes Documentation

### variable _MCRef

```cpp
std::map< PartEnPairType, MCRefType > _MCRef;
```

Map used to store MC reference values. 

### variable _PosIDtoXYBarsMap

```cpp
std::map< Int_t, std::pair< Int_t, Int_t > > _PosIDtoXYBarsMap;
```

Map used to store the X and Y bars corresponding to a TW position. 

### variable _PartEnPairsMC

```cpp
std::vector< PartEnPairType > _PartEnPairsMC;
```

Vector storing the beams found in the MC table; Used to control the MC table, initialize histograms and deallocate memory at the end. 

### variable _PartEnPairsData

```cpp
std::vector< PartEnPairType > _PartEnPairsData;
```

Vector storing the beams found in data; Used to run the calibration on the beams found. 

### variable _hQ

```cpp
std::map< PartEnPairType, std::vector< TH1F * > > _hQ;
```

Raw energy loss histograms for each position of both TW layers (0=LayerY, 1=LayerX). Key is the beam type (particle-energy) 

### variable _hTOF

```cpp
std::map< PartEnPairType, std::vector< TH1F * > > _hTOF;
```

Raw Time-Of-Flight histograms for each position of both TW layers (0=LayerY, 1=LayerX). Key is the beam type (particle-energy) 

### variable _funcdECal

```cpp
TF1 * _funcdECal;
```

Function used for the light output model -> Energy calibration. 

### variable _Debug

```cpp
Bool_t _Debug;
```

Flag used to set debug mode. 

-------------------------------

Updated on 2022-06-15 at 14:10:15 +0000