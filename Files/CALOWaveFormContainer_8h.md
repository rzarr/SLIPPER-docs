---
title: src/WFProcessing/CALOWaveFormContainer.h
summary: Header of CALOWaveFormContainer.cxx. 

---

# src/WFProcessing/CALOWaveFormContainer.h

Header of CALOWaveFormContainer.cxx.  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CALOWaveFormContainer](/Classes/classCALOWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms for the Calorimeter.  |

## Detailed Description

Header of CALOWaveFormContainer.cxx. 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef CALOWAVEFORMCONTAINER_H
#define CALOWAVEFORMCONTAINER_H

#include "WaveFormContainer.h"

class CALOWaveFormContainer : public WaveFormContainer
{

public:
    CALOWaveFormContainer();

    virtual Float_t     GetChargeCALO(Int_t channel, Int_t start_bin = CHARGESTARTBIN, Int_t stop_bin = CHARGESTOPBIN);

};


#endif
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
