---
title: src/WFProcessing/TWWaveFormContainer.h
summary: Header of TWWaveFormContainer.cxx. 

---

# src/WFProcessing/TWWaveFormContainer.h

Header of [TWWaveFormContainer.cxx](/Files/TWWaveFormContainer_8cxx.md#file-twwaveformcontainer.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TWWaveFormContainer](/Classes/classTWWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms for the TOF-Wall detector.  |

## Detailed Description

Header of [TWWaveFormContainer.cxx](/Files/TWWaveFormContainer_8cxx.md#file-twwaveformcontainer.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef TWWAVEFORMCONTAINER_H
#define TWWAVEFORMCONTAINER_H

#include "WaveFormContainer.h"

class TWWaveFormContainer : public WaveFormContainer
{

public:
    TWWaveFormContainer();

virtual Float_t     GetTimeLinear(Int_t channel, UShort_t board = 0, Int_t event=-1, TFile* fOut=nullptr, TString detector="");

};


#endif
```


-------------------------------

Updated on 2022-03-05 at 18:47:20 +0000
