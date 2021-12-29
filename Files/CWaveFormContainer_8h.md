---
title: src/CWaveFormContainer.h
summary: Header of CWaveFormContainer.cxx. 

---

# src/CWaveFormContainer.h

Header of [CWaveFormContainer.cxx](/Files/CWaveFormContainer_8cxx.md#file-cwaveformcontainer.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CWaveFormContainer](/Classes/classCWaveFormContainer.md)** <br>Class that handles all the processing of raw WaveDAQ waveforms.  |

## Detailed Description

Header of [CWaveFormContainer.cxx](/Files/CWaveFormContainer_8cxx.md#file-cwaveformcontainer.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef CWAVEFORM_CONTAINER
#define CWAVEFORM_CONTAINER

#include <TGraph.h>
#include <TH2D.h>
#include "TFile.h"
#include "TLinearFitter.h"

#include "CUtils.h"

class CWaveFormContainer
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
    virtual void        SumSCWavefoms(std::vector<Int_t>* Channels, std::vector<Float_t>* SC_Sum_W, std::vector<Float_t>* SC_Sum_T);
    virtual void        SaveWF(Int_t board, Int_t channel, Int_t event, TFile* fOut, TString detector, TString tag="");

public:

    WDBDATA data;                           

    CWaveFormContainer();
    
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
    
    //_SC functions
    virtual Float_t     GetTimeSC(std::vector<Int_t>* Channels, UShort_t BoardId = 0, Int_t event = -1, TFile* fOut = nullptr);
    virtual Float_t     GetTimeSC_Linear(std::vector<Int_t>* Channels);

    //TW functions
    virtual Float_t     GetTimeCFD(Int_t channel, UShort_t board = 0, Int_t event=-1, TFile* fOut=nullptr, TString detector="");
    virtual Float_t     GetTimeLinear(Int_t channel, UShort_t board = 0, Int_t event=-1, TFile* fOut=nullptr, TString detector="");

    //CALO functions
    virtual Float_t     GetChargeCALO(Int_t channel);

    //CLK functions
    virtual Float_t     GetCLKPhase(Int_t channel, UShort_t board = 0, Int_t event = -1, TFile* fOut = nullptr);

};
#endif
```


-------------------------------

Updated on 2021-12-29 at 15:02:03 +0100
