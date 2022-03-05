---
title: src/WFProcessing/WaveFormContainer.h
summary: Header of WaveFormContainer.cxx. 

---

# src/WFProcessing/WaveFormContainer.h

Header of [WaveFormContainer.cxx](/Files/WaveFormContainer_8cxx.md#file-waveformcontainer.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[WaveFormContainer](/Classes/classWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms.  |

## Detailed Description

Header of [WaveFormContainer.cxx](/Files/WaveFormContainer_8cxx.md#file-waveformcontainer.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef WAVEFORM_CONTAINER
#define WAVEFORM_CONTAINER

#include <TGraph.h>
#include <TH2D.h>
#include "TFile.h"
#include "TLinearFitter.h"

#include "CUtils.h"

class WaveFormContainer
{
protected:
    Float_t _Ped[NUMBEROFCHANNELS];         
    Float_t _PedRMS[NUMBEROFCHANNELS];      
    Float_t _Amp[NUMBEROFCHANNELS];         
    Float_t _Charge[NUMBEROFCHANNELS];      
    Float_t _Time[NUMBEROFCHANNELS];        
    Float_t _RiseTime[NUMBEROFCHANNELS];    

    //Generic WF functions
    virtual void        RescaleTime(std::vector<Float_t>* tmp_time);
    virtual void        MedianFilter(Int_t channel);
    virtual void        SaveWF(Int_t board, Int_t channel, Int_t event, TFile* fOut, TString detector, TString tag="");

public:

    WDBDATA data;                           

    WaveFormContainer();
    virtual ~WaveFormContainer();
    
    //Generic utility functions
    virtual Bool_t      IsEmpty(Int_t channel);
    virtual Bool_t      IsEmptyTest(Int_t channel);
    virtual void        CopyWaveform(NeutronWF* nWF, int channel);
    virtual void        ClearData();

    //General WF processing
    virtual std::pair<Float_t, Float_t> GetPedestal(Int_t channel);
    virtual Float_t     GetAmplitude(Int_t channel);
    virtual Float_t     GetCharge(Int_t channel, Int_t start_bin = CHARGESTARTBIN, Int_t stop_bin = CHARGESTOPBIN);
    virtual Float_t     GetRiseTime(Int_t channel);
    virtual Float_t     GetTimeCFD(Int_t channel, UShort_t board = 0, Int_t event=-1, TFile* fOut=nullptr, TString detector="");

    //CLK functions
    virtual Float_t     GetCLKPhase(Int_t channel, UShort_t board = 0, Int_t event = -1, TFile* fOut = nullptr);

};
#endif
```


-------------------------------

Updated on 2022-03-05 at 18:47:20 +0000
