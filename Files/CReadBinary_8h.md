---
title: src/CReadBinary.h
summary: Header of CReadBinary.cxx. 

---

# src/CReadBinary.h

Header of [CReadBinary.cxx](/Files/CReadBinary_8cxx.md#file-creadbinary.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CReadBinary](/Classes/classCReadBinary.md)** <br>Class that handles all the decoding of WaveDAQ events from binary files.  |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[ALLINFO](/Files/CReadBinary_8h.md#define-allinfo)**  |
|  | **[DBG](/Files/CReadBinary_8h.md#define-dbg)**  |

## Detailed Description

Header of [CReadBinary.cxx](/Files/CReadBinary_8cxx.md#file-creadbinary.cxx). 

**Author**: R. Zarrella 



## Macros Documentation

### define ALLINFO

```cpp
#define ALLINFO 0
```


### define DBG

```cpp
#define DBG 1
```


## Source code

```cpp

#ifndef CREAD_BINARY_H
#define CREAD_BINARY_H

#include <string.h>
#include <iostream>
#include "CWaveFormContainer.h"

#define ALLINFO 0
#define DBG 1

class CReadBinary {
private:
    //Local variables and indices
    int garbage;
    int b, chn, chn_index;
    double t1, t2, dt;

protected:
    //Main control and data variables
    int Nev;                                                    
    std::vector<WDBBIN> _bins;                                  
    std::vector<CWaveFormContainer*>* _data_wdb;                
    std::vector<TCBDATA*>* _data_tcb;                           
    std::map<UShort_t, int>* _wdb_index, _tcb_index;            
    std::map<UShort_t, int>* _ActiveBoards;                     
    TH2F* _hTGEN_MB;                                            
    TH2F* _hTGEN_frag;                                          
    TH1I* _hTriggerPattern;                                     
    TH1I* _hTriggerRates;                                       

    Float_t _TotalTime;                                         
    unsigned int _TriggerCount[64];                             

    //Variables used for WaveDREAM event decoding
    DRSBHEADER drsbh;                                           
    EHEADER eh;                                                 
    CHEADER ch;                                                 
    THEADER th;                                                 
    BHEADER bh;                                                 
    DRSCHEADER drsch[18];                                       

    unsigned short voltage[1024];                               
    unsigned long scaler_data[18], scaler_data_old[18] = {0};   
    unsigned long scaler_time, scaler_time_old = 0;             

    uint64_t _TriggerGenerationBin[32];                         
    Bool_t _IsFragTriggerOn;                                    

    //TDC variables
    Float_t* _TDCTime;                                          
    std::map<int, int>* _TDCchMap;                              


    Bool_t      ReadTDCData(FILE *f);
    void        ReadWDBEvent(FILE *f);
    void        ReadTCBEvent(FILE *f);
    void        AlignTriggerCell();
    void        AlignSignalsRight();
    void        CheckRangeOverflow(Float_t* w_ptr);

    void        FillHistoTGEN(TH2F* hTGEN);
    void        FillHistoTrigPattern(uint64_t TriggerPattern);

public:
    CReadBinary(std::vector<CWaveFormContainer*>* wdb_data_ptr, std::vector<TCBDATA*>* tcb_data_ptr, std::map<UShort_t, Int_t>* _WDBIdToIdMap, std::map<UShort_t, Int_t>* ActiveBoards, Float_t* TDCTime, std::map<int, int>* TDCchMap, TH2F* hTGEN_MB, TH2F* hTGEN_frag, TH1I* hTriggerPattern, TH1I* hTriggerRates);
    virtual ~CReadBinary();
    void        CheckBinaryFileHeader(FILE* f);
    void        LoadWaveDreamTimeCalibration(FILE* f);
    Int_t       DecodeEvent(FILE* f);
    void        FillHistoTrigRates();

    Bool_t      IsFragTriggerOn();
    void        ResetFragTrigger();

    //TDAQ functions
    Bool_t      ReadEvtStartWords(FILE* f);
};

#endif
```


-------------------------------

Updated on 2022-02-10 at 12:05:07 +0000
