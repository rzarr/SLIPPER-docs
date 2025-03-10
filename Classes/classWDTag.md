---
title: WDTag
summary: Class for WaveDREAM stand-alone files tagging. 

---

# WDTag



Class for WaveDREAM stand-alone files tagging.  [More...](#detailed-description)


`#include <CUtils.h>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[BeamEnergy](/Classes/classWDTag.md#variable-beamenergy)** <br>Kinetic energy per nucleon of the Primary beam.  |
| Int_t | **[FileNumber](/Classes/classWDTag.md#variable-filenumber)** <br>Number of the file.  |
| ParticleType | **[PrimaryParticle](/Classes/classWDTag.md#variable-primaryparticle)** <br>Primary particle identifier.  |

## Detailed Description

```cpp
class WDTag;
```

Class for WaveDREAM stand-alone files tagging. 

Different tags are already available in the current version and can be activated by un-commenting some lines of code. The variables that can be activated right now are:

* Gain: Frontend WaveDAQ gain
* BeamEnergy: Primary beam kinetic energy per nucleon
* BeamPositionX: TO BE IMPLEMENTED
* BeamPositionY: TO BE IMPLEMENTED
* PrimaryParticle: Identifier for the primary beam particle
* FileNumber: Number of the processed file (currently used only for CNAO2021) 

## Public Attributes Documentation

### variable BeamEnergy

```cpp
Float_t BeamEnergy;
```

Kinetic energy per nucleon of the Primary beam. 

### variable FileNumber

```cpp
Int_t FileNumber;
```

Number of the file. 

### variable PrimaryParticle

```cpp
ParticleType PrimaryParticle;
```

Primary particle identifier. 

-------------------------------

Updated on 2025-02-26 at 13:36:50 +0000