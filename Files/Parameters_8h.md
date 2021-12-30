---
title: src/Utilities/Parameters.h
summary: File containing all Parameters used in the processing and calibration executables. 

---

# src/Utilities/Parameters.h

File containing all Parameters used in the processing and calibration executables.  [More...](#detailed-description)

## Types

|                | Name           |
| -------------- | -------------- |
| enum| **[ParticleType](/Files/Parameters_8h.md#enum-particletype)** { None =-1, Proton, Helium, Carbon, Oxygen}<br>Type of beam particles.  |
| enum| **[TLayer](/Files/Parameters_8h.md#enum-tlayer)** { NoLayer =-1, LayerX =1, LayerY =0}<br>TW X-Y layer definition.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< [TLayer](/Files/Parameters_8h.md#enum-tlayer), std::string > | **[LayerName](/Files/Parameters_8h.md#variable-layername)** <br>Map linking the TLayer enum to the TW layer name.  |
| std::map< [ParticleType](/Files/Parameters_8h.md#enum-particletype), std::string > | **[ParticleName](/Files/Parameters_8h.md#variable-particlename)** <br>Map linking the ParticleType enum to the actual name of the particle.  |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[WAVEFORMBINS](/Files/Parameters_8h.md#define-waveformbins)** <br>Number of bins in a Waveform.  |
|  | **[MAXNUMBEROFBOARDS](/Files/Parameters_8h.md#define-maxnumberofboards)** <br>Maximum number of WaveDREAM boards.  |
|  | **[NUMBEROFCHANNELS](/Files/Parameters_8h.md#define-numberofchannels)** <br>Number of channel per WaveDREAM board.  |
|  | **[NUMBEROFTWBARS](/Files/Parameters_8h.md#define-numberoftwbars)** <br>Number of bars in the TW.  |
|  | **[NUMBEROFTWLAYERS](/Files/Parameters_8h.md#define-numberoftwlayers)** <br>Number of TW layers.  |
|  | **[NUMBEROFGLOBALCHANNELSTW](/Files/Parameters_8h.md#define-numberofglobalchannelstw)** <br>Number of channels used for the TW.  |
|  | **[NUMBEROFCALOMODULES](/Files/Parameters_8h.md#define-numberofcalomodules)** <br>Number of Calorimeter modules in the acquisition.  |
|  | **[NUMBEROFCRYSTALS](/Files/Parameters_8h.md#define-numberofcrystals)** <br>Number of Calorimeter crystals in the acquisition.  |
|  | **[NUMBEROFSCCHANNELS](/Files/Parameters_8h.md#define-numberofscchannels)** <br>Number of Start Counter channels.  |
|  | **[SCSUMSTARTBIN](/Files/Parameters_8h.md#define-scsumstartbin)** <br>First bin for SC waveform sum.  |
|  | **[SCSUMSTOPBIN](/Files/Parameters_8h.md#define-scsumstopbin)** <br>Last bin for SC waveform sum.  |
|  | **[SCCFDTHRESHOLD](/Files/Parameters_8h.md#define-sccfdthreshold)** <br>Threshold for Costant Fraction Discriminator in SC time calculation.  |
|  | **[SCBOARD](/Files/Parameters_8h.md#define-scboard)** <br>Serial number of the SC WaveDREAM board.  |
|  | **[CLKSTARTBIN](/Files/Parameters_8h.md#define-clkstartbin)** <br>First bin for CLK phase calculation.  |
|  | **[CLKSTOPBIN](/Files/Parameters_8h.md#define-clkstopbin)** <br>Last bin for CLK phase calculation.  |
|  | **[CLKPERIOD](/Files/Parameters_8h.md#define-clkperiod)** <br>CLK period [ns].  |
|  | **[PEDESTALSTARTBIN](/Files/Parameters_8h.md#define-pedestalstartbin)** <br>First bin for TW pedestal calculation.  |
|  | **[PEDESTALSTOPBIN](/Files/Parameters_8h.md#define-pedestalstopbin)** <br>Last bin for TW pedestal calculation.  |
|  | **[AMPLITUDESTARTBIN](/Files/Parameters_8h.md#define-amplitudestartbin)** <br>First bin for TW amplitude calculation.  |
|  | **[AMPLITUDESTOPBIN](/Files/Parameters_8h.md#define-amplitudestopbin)** <br>Last bin for TW amplitude calculation.  |
|  | **[CHARGESTARTBIN](/Files/Parameters_8h.md#define-chargestartbin)** <br>First bin for TW charge calculation.  |
|  | **[CHARGESTOPBIN](/Files/Parameters_8h.md#define-chargestopbin)** <br>Last bin for TW charge calculation.  |
|  | **[TIMESTAMPSTARTBIN](/Files/Parameters_8h.md#define-timestampstartbin)** <br>First bin for TW raw time calculation.  |
|  | **[TIMESTAMPSTOPBIN](/Files/Parameters_8h.md#define-timestampstopbin)** <br>Last bin for TW raw time calculation.  |
|  | **[DEFAULTCFDTHRESHOLD](/Files/Parameters_8h.md#define-defaultcfdthreshold)** <br>Threshold for Costant Fraction Discriminator in TW time calculation.  |
|  | **[NEUTRONSLOWCHANNELS](/Files/Parameters_8h.md#define-neutronslowchannels)** <br>Total number of SLOW channels of Neutron detectors.  |
|  | **[NEUTRONFASTCHANNELS](/Files/Parameters_8h.md#define-neutronfastchannels)** <br>Total number of FAST channels of Neutron detectors.  |
|  | **[FRAGTRIGGERBOARD](/Files/Parameters_8h.md#define-fragtriggerboard)** <br>Serial number of WaveDREAM board used for the fragmentation trigger VETO.  |
|  | **[NUMBEROFTRIGGERCHANNELS](/Files/Parameters_8h.md#define-numberoftriggerchannels)** <br>Number of channels used in the fragmentation trigger.  |
|  | **[EMPTYSTARTBIN](/Files/Parameters_8h.md#define-emptystartbin)** <br>First bin used to check if the channel is empty.  |
|  | **[EMPTYSTOPBIN](/Files/Parameters_8h.md#define-emptystopbin)** <br>Last bin used to check if the channel is empty.  |
|  | **[EMPTYTS](/Files/Parameters_8h.md#define-emptyts)** <br>Threshold for empty channel surpassing the Zero-Suppression of the firmware [V].  |
|  | **[LAYERXBARMIN](/Files/Parameters_8h.md#define-layerxbarmin)** <br>Maximum index of a TW bar in the X layer.  |
|  | **[LAYERXBARMAX](/Files/Parameters_8h.md#define-layerxbarmax)** <br>Minimum index of a TW bar in the X layer.  |
|  | **[LAYERYBARMIN](/Files/Parameters_8h.md#define-layerybarmin)** <br>Maximum index of a TW bar in the Y layer.  |
|  | **[LAYERYBARMAX](/Files/Parameters_8h.md#define-layerybarmax)** <br>Minimum index of a TW bar in the Y layer.  |
|  | **[NUMBEROFTWPOSITIONS](/Files/Parameters_8h.md#define-numberoftwpositions)** <br>Total number of TW positions.  |
|  | **[QMIN](/Files/Parameters_8h.md#define-qmin)** <br>Lower bound of raw energy loss histograms [V*ns].  |
|  | **[QMAX](/Files/Parameters_8h.md#define-qmax)** <br>Higher bound of raw energy loss histograms [V*ns].  |
|  | **[QBINS](/Files/Parameters_8h.md#define-qbins)** <br>Number of bins in energy loss histograms.  |
|  | **[TOFMIN](/Files/Parameters_8h.md#define-tofmin)** <br>Lower bound of raw Time-Of-Flight histograms[ns].  |
|  | **[TOFMAX](/Files/Parameters_8h.md#define-tofmax)** <br>Higher bound of raw Time-Of-Flight histograms[ns].  |
|  | **[TOFBINS](/Files/Parameters_8h.md#define-tofbins)** <br>Number of bins in raw Time-Of-Flight histograms.  |
|  | **[DEMIN](/Files/Parameters_8h.md#define-demin)** <br>Minimum expected calibrated energy loss [MeV].  |
|  | **[DEMAX](/Files/Parameters_8h.md#define-demax)** <br>Maximum expected calibrated energy loss [MeV].  |

## Detailed Description

File containing all Parameters used in the processing and calibration executables. 

**Author**: R. Zarrella


This file needs to be carefully checked everytime a different campaign is analyzed 

## Types Documentation

### enum ParticleType

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| None | =-1|   |
| Proton | |   |
| Helium | |   |
| Carbon | |   |
| Oxygen | |   |



Type of beam particles. 

### enum TLayer

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| NoLayer | =-1|   |
| LayerX | =1|   |
| LayerY | =0|   |



TW X-Y layer definition. 



## Attributes Documentation

### variable LayerName

```cpp
static std::map< TLayer, std::string > LayerName ={{LayerX,"LayerX"},{LayerY,"LayerY"}};
```

Map linking the TLayer enum to the TW layer name. 

### variable ParticleName

```cpp
static std::map< ParticleType, std::string > ParticleName ={{None,"None"},{Proton,"Proton"},{Helium,"Helium"},{Carbon,"Carbon"},{Oxygen,"Oxygen"}};
```

Map linking the ParticleType enum to the actual name of the particle. 


## Macros Documentation

### define WAVEFORMBINS

```cpp
#define WAVEFORMBINS 1024
```

Number of bins in a Waveform. 

### define MAXNUMBEROFBOARDS

```cpp
#define MAXNUMBEROFBOARDS 32
```

Maximum number of WaveDREAM boards. 

### define NUMBEROFCHANNELS

```cpp
#define NUMBEROFCHANNELS 18
```

Number of channel per WaveDREAM board. 

### define NUMBEROFTWBARS

```cpp
#define NUMBEROFTWBARS 40
```

Number of bars in the TW. 

### define NUMBEROFTWLAYERS

```cpp
#define NUMBEROFTWLAYERS 2
```

Number of TW layers. 

### define NUMBEROFGLOBALCHANNELSTW

```cpp
#define NUMBEROFGLOBALCHANNELSTW 80
```

Number of channels used for the TW. 

### define NUMBEROFCALOMODULES

```cpp
#define NUMBEROFCALOMODULES 2
```

Number of Calorimeter modules in the acquisition. 

### define NUMBEROFCRYSTALS

```cpp
#define NUMBEROFCRYSTALS 13
```

Number of Calorimeter crystals in the acquisition. 

### define NUMBEROFSCCHANNELS

```cpp
#define NUMBEROFSCCHANNELS 8
```

Number of Start Counter channels. 

### define SCSUMSTARTBIN

```cpp
#define SCSUMSTARTBIN 100
```

First bin for SC waveform sum. 

### define SCSUMSTOPBIN

```cpp
#define SCSUMSTOPBIN 700
```

Last bin for SC waveform sum. 

### define SCCFDTHRESHOLD

```cpp
#define SCCFDTHRESHOLD 0.2
```

Threshold for Costant Fraction Discriminator in SC time calculation. 

### define SCBOARD

```cpp
#define SCBOARD 173
```

Serial number of the SC WaveDREAM board. 

### define CLKSTARTBIN

```cpp
#define CLKSTARTBIN 500
```

First bin for CLK phase calculation. 

### define CLKSTOPBIN

```cpp
#define CLKSTOPBIN 1023
```

Last bin for CLK phase calculation. 

### define CLKPERIOD

```cpp
#define CLKPERIOD 12.5
```

CLK period [ns]. 

### define PEDESTALSTARTBIN

```cpp
#define PEDESTALSTARTBIN 10
```

First bin for TW pedestal calculation. 

### define PEDESTALSTOPBIN

```cpp
#define PEDESTALSTOPBIN 50
```

Last bin for TW pedestal calculation. 

### define AMPLITUDESTARTBIN

```cpp
#define AMPLITUDESTARTBIN 100
```

First bin for TW amplitude calculation. 

### define AMPLITUDESTOPBIN

```cpp
#define AMPLITUDESTOPBIN 900
```

Last bin for TW amplitude calculation. 

### define CHARGESTARTBIN

```cpp
#define CHARGESTARTBIN 5
```

First bin for TW charge calculation. 

### define CHARGESTOPBIN

```cpp
#define CHARGESTOPBIN 1018
```

Last bin for TW charge calculation. 

### define TIMESTAMPSTARTBIN

```cpp
#define TIMESTAMPSTARTBIN 100
```

First bin for TW raw time calculation. 

### define TIMESTAMPSTOPBIN

```cpp
#define TIMESTAMPSTOPBIN 900
```

Last bin for TW raw time calculation. 

### define DEFAULTCFDTHRESHOLD

```cpp
#define DEFAULTCFDTHRESHOLD 0.3
```

Threshold for Costant Fraction Discriminator in TW time calculation. 

### define NEUTRONSLOWCHANNELS

```cpp
#define NEUTRONSLOWCHANNELS 6
```

Total number of SLOW channels of Neutron detectors. 

### define NEUTRONFASTCHANNELS

```cpp
#define NEUTRONFASTCHANNELS 5
```

Total number of FAST channels of Neutron detectors. 

### define FRAGTRIGGERBOARD

```cpp
#define FRAGTRIGGERBOARD 166
```

Serial number of WaveDREAM board used for the fragmentation trigger VETO. 

### define NUMBEROFTRIGGERCHANNELS

```cpp
#define NUMBEROFTRIGGERCHANNELS 12
```

Number of channels used in the fragmentation trigger. 

### define EMPTYSTARTBIN

```cpp
#define EMPTYSTARTBIN 50
```

First bin used to check if the channel is empty. 

### define EMPTYSTOPBIN

```cpp
#define EMPTYSTOPBIN 950
```

Last bin used to check if the channel is empty. 

### define EMPTYTS

```cpp
#define EMPTYTS 0.01
```

Threshold for empty channel surpassing the Zero-Suppression of the firmware [V]. 

### define LAYERXBARMIN

```cpp
#define LAYERXBARMIN 20
```

Maximum index of a TW bar in the X layer. 

### define LAYERXBARMAX

```cpp
#define LAYERXBARMAX 39
```

Minimum index of a TW bar in the X layer. 

### define LAYERYBARMIN

```cpp
#define LAYERYBARMIN 0
```

Maximum index of a TW bar in the Y layer. 

### define LAYERYBARMAX

```cpp
#define LAYERYBARMAX 19
```

Minimum index of a TW bar in the Y layer. 

### define NUMBEROFTWPOSITIONS

```cpp
#define NUMBEROFTWPOSITIONS 400
```

Total number of TW positions. 

### define QMIN

```cpp
#define QMIN 0.
```

Lower bound of raw energy loss histograms [V*ns]. 

### define QMAX

```cpp
#define QMAX 50.
```

Higher bound of raw energy loss histograms [V*ns]. 

### define QBINS

```cpp
#define QBINS 300
```

Number of bins in energy loss histograms. 

### define TOFMIN

```cpp
#define TOFMIN 0.
```

Lower bound of raw Time-Of-Flight histograms[ns]. 

### define TOFMAX

```cpp
#define TOFMAX 50.
```

Higher bound of raw Time-Of-Flight histograms[ns]. 

### define TOFBINS

```cpp
#define TOFBINS 5000
```

Number of bins in raw Time-Of-Flight histograms. 

### define DEMIN

```cpp
#define DEMIN 0.
```

Minimum expected calibrated energy loss [MeV]. 

### define DEMAX

```cpp
#define DEMAX 250.
```

Maximum expected calibrated energy loss [MeV]. 

## Source code

```cpp

#ifndef PARAMETERS_H
#define PARAMETERS_H

#include <utility>
#include <vector>
#include <map>
#include <tuple>
#include <TF1.h>

#define WAVEFORMBINS 1024                   
#define MAXNUMBEROFBOARDS 32                
#define NUMBEROFCHANNELS 18                 

#define NUMBEROFTWBARS 40                   
#define NUMBEROFTWLAYERS 2                  
#define NUMBEROFGLOBALCHANNELSTW 80         

#define NUMBEROFCALOMODULES 2               
#define NUMBEROFCRYSTALS 13                 

//SC analysis parameters
#define NUMBEROFSCCHANNELS 8                
#define SCSUMSTARTBIN 100                   
#define SCSUMSTOPBIN 700                    
#define SCCFDTHRESHOLD 0.2                  
#define SCBOARD 173                         

//Range of CLK analysis
#define CLKSTARTBIN 500                     
#define CLKSTOPBIN 1023                     
#define CLKPERIOD 12.5                      

//Ranges for TW analysis
#define PEDESTALSTARTBIN 10                 
#define PEDESTALSTOPBIN 50                  
#define AMPLITUDESTARTBIN 100               
#define AMPLITUDESTOPBIN  900               
#define CHARGESTARTBIN 5                    
#define CHARGESTOPBIN  1018                 
#define TIMESTAMPSTARTBIN 100               
#define TIMESTAMPSTOPBIN  900               
#define DEFAULTCFDTHRESHOLD 0.3             

#define NEUTRONSLOWCHANNELS 6               
#define NEUTRONFASTCHANNELS 5               

#define FRAGTRIGGERBOARD 166                
#define NUMBEROFTRIGGERCHANNELS 12          

#define EMPTYSTARTBIN 50                    
#define EMPTYSTOPBIN 950                    
#define EMPTYTS 0.01                        

//Parameters for TOFWallCalibration: ADJUST FOR EACH CAMPAIGN!!
#define LAYERXBARMIN 20                     
#define LAYERXBARMAX 39                     
#define LAYERYBARMIN 0                      
#define LAYERYBARMAX 19                     
#define NUMBEROFTWPOSITIONS 400             
#define QMIN 0.                             
#define QMAX 50.                            
#define QBINS 300                           
#define TOFMIN 0.                           
#define TOFMAX 50.                          
#define TOFBINS 5000                        
#define DEMIN 0.                            
#define DEMAX 250.                          

enum ParticleType {None=-1, Proton, Helium, Carbon, Oxygen};

enum TLayer {NoLayer=-1,LayerX=1,LayerY=0};  // layer1--> horizontal bars, layer0--> vertical bars

static std::map<TLayer, std::string> LayerName={{LayerX,"LayerX"},{LayerY,"LayerY"}};   

static std::map<ParticleType, std::string> ParticleName={{None,"None"},{Proton,"Proton"},{Helium,"Helium"},{Carbon,"Carbon"},{Oxygen,"Oxygen"}};    

#endif
```


-------------------------------

Updated on 2021-12-30 at 11:00:09 +0000
