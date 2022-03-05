---
title: src/WFProcessing/SCWaveFormContainer.h
summary: Header of SCWaveFormContainer.cxx. 

---

# src/WFProcessing/SCWaveFormContainer.h

Header of [SCWaveFormContainer.cxx](/Files/SCWaveFormContainer_8cxx.md#file-scwaveformcontainer.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[SCWaveFormContainer](/Classes/classSCWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms for the Start Counter detector.  |

## Detailed Description

Header of [SCWaveFormContainer.cxx](/Files/SCWaveFormContainer_8cxx.md#file-scwaveformcontainer.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef SCWAVEFORMCONTAINER_H
#define SCWAVEFORMCONTAINER_H

#include "WaveFormContainer.h"


class SCWaveFormContainer : public WaveFormContainer
{
protected:
    std::vector<Float_t> _SC_Sum_W;         
    std::vector<Float_t> _SC_Sum_T;         
    Float_t _SCped;                         
    Float_t _SCpedRMS;                      
    
    //SC total signal functions
    virtual void        SumSCWavefoms(std::vector<Int_t>* Channels);
    virtual Bool_t      CheckForPileUp(std::vector<Float_t>* w_ptr, std::vector<Float_t>* t_ptr, Int_t event=-1, TFile* fOut=nullptr);
public:
    SCWaveFormContainer();

    //_SC functions
    virtual Float_t     GetSCTotalCharge(std::vector<Int_t>* Channels);
    virtual Float_t     GetTimeSC(Bool_t* IsPossiblePileUp, std::vector<Int_t>* Channels, UShort_t BoardId = 0, Int_t event = -1, TFile* fOut = nullptr);
    virtual Float_t     GetTimeSC_Linear(std::vector<Int_t>* Channels);
    virtual Float_t     GetChargeSC(Int_t channel, Int_t start_bin = CHARGESTARTBIN, Int_t stop_bin = CHARGESTOPBIN);

    virtual void        ClearData();

};


#endif
```


-------------------------------

Updated on 2022-03-05 at 18:47:20 +0000
