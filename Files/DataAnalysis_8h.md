---
title: src/DataAnalysis.h
summary: Header of DataAnalysis.cxx. 

---

# src/DataAnalysis.h

Header of DataAnalysis.cxx.  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[DataAnalysis](/Classes/classDataAnalysis.md)** <br>Main class used by the Analysis executable.  |

## Detailed Description

Header of DataAnalysis.cxx. 

**Author**: M. Montefiori and R. Zarrella 



## Source code

```cpp

#ifndef DATAANALYSIS_H
#define DATAANALYSIS_H
#include <string>
#include <TString.h>
#include "TFile.h"
#include "TTree.h"
#include "TH1F.h"
#include "TH2F.h"
#include "TGraphErrors.h"
#include "TLegend.h"
#include "TCanvas.h"

#include "Parameters.h"
#include "Message.h"

class DataAnalysis
{
protected:
    Int_t RearBar;                                      
    Int_t FrontBar;                                     

    Float_t _Charge[NUMBEROFTWBARS];                    
    Float_t _Charge_A[NUMBEROFTWBARS];                  
    Float_t _Charge_B[NUMBEROFTWBARS];                  
    Float_t _Ampl_A[NUMBEROFTWBARS];                    
    Float_t _Ampl_B[NUMBEROFTWBARS];                    
    Float_t _DeltaT_AB[NUMBEROFTWBARS];                 

    Int_t _NumberOfGhosts;                              

    //Output TFile
    TFile* fOut;                                        

    // Charge histogram for the two layers
    TH1F *_hist_Charge_Front[NUMBEROFTWPOSITIONS];      
    TH1F *_hist_Charge_Rear[NUMBEROFTWPOSITIONS];       

    // Amplitude histogram for the two layers
    TH1F *_hist_Ampl_A_Rear[NUMBEROFTWPOSITIONS];       
    TH1F *_hist_Ampl_B_Rear[NUMBEROFTWPOSITIONS];       
    TH1F *_hist_Ampl_A_Front[NUMBEROFTWPOSITIONS];      
    TH1F *_hist_Ampl_B_Front[NUMBEROFTWPOSITIONS];      

    // Difference time AB histogram for the two layers
    TH1F *_hist_DeltaT_AB_Front[NUMBEROFTWPOSITIONS];   
    TH1F *_hist_DeltaT_AB_Rear[NUMBEROFTWPOSITIONS];    

    // Graphs of DeltaT_AB vs position for each bar
    TGraphErrors* _DeltaT_AB_Bar[NUMBEROFTWBARS];       
    TH2F* _hitmap_DeltaT_Front;                         
    TH2F* _hitmap_DeltaT_Rear;                          

    TH1F *_hitmap_Channels_A;                           
    TH1F *_hitmap_Channels_B;                           


    bool CheckTriggeredBars();
    void InitHistos();
    void SetOutputStructures(TTree* t);
    void FillHistograms();
    TF1* FitGauss(TH1F *hist);
    void AnalyzeDeltaT();

public:
    DataAnalysis();
    void DoAll(TString InputFileName, TString OutputFileName);

};
#endif
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
