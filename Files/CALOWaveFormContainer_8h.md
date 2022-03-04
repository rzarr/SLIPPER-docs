---
title: src/WFProcessing/CALOWaveFormContainer.h
summary: Header of CALOWaveFormContainer.cxx. 

---

# src/WFProcessing/CALOWaveFormContainer.h

Header of [CALOWaveFormContainer.cxx](/Files/CALOWaveFormContainer_8cxx.md#file-calowaveformcontainer.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CALOWaveFormContainer](/Classes/classCALOWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms for the Calorimeter.  |

## Detailed Description

Header of [CALOWaveFormContainer.cxx](/Files/CALOWaveFormContainer_8cxx.md#file-calowaveformcontainer.cxx). 

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

Updated on 2022-03-04 at 14:25:58 +0000
