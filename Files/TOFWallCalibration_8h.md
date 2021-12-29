---
title: src/TOFWallCalibration.h
summary: Header of TOFWallCalibration.cxx. 

---

# src/TOFWallCalibration.h

Header of [TOFWallCalibration.cxx](/Files/TOFWallCalibration_8cxx.md#file-tofwallcalibration.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TOFWallCalibration](/Classes/classTOFWallCalibration.md)** <br>Main class used to handle the whole dE-TOF Calibration process.  |

## Types

|                | Name           |
| -------------- | -------------- |
| typedef std::pair< [ParticleType](/Files/Parameters_8h.md#enum-particletype), Float_t > | **[PartEnPairType](/Files/TOFWallCalibration_8h.md#typedef-partenpairtype)**  |

## Detailed Description

Header of [TOFWallCalibration.cxx](/Files/TOFWallCalibration_8cxx.md#file-tofwallcalibration.cxx). 

**Author**: R. Zarrella 
## Types Documentation

### typedef PartEnPairType

```cpp
typedef std::pair<ParticleType, Float_t> PartEnPairType;
```





## Source code

```cpp

#ifndef TOFWALLCALIBRATION_H
#define TOFWALLCALIBRATION_H
#include <algorithm>
#include <fstream>

#include <TSystem.h>
#include <TTree.h>
#include <TBranch.h>
#include <TH1F.h>
#include <TFile.h>
#include <TStyle.h>
#include <TGraph.h>
#include <TCanvas.h>
#include <TMath.h>
#include <TGraphErrors.h>
#include <TSystemDirectory.h>
#include "TH2D.h"

#include "Message.h"
#include "CUtils.h"


typedef std::pair<ParticleType, Float_t> PartEnPairType;

typedef struct{
    std::map<TLayer, Float_t> dE_MC;
    std::map<TLayer, Float_t> TOF_MC;
} MCRefType;

class TOFWallCalibration
{
    //Utility maps
    std::map<PartEnPairType, MCRefType> _MCRef;                 
    std::map<Int_t, std::pair<Int_t, Int_t>> _PosIDtoXYBarsMap; 
    std::vector<PartEnPairType> _PartEnPairsMC;                 
    std::vector<PartEnPairType> _PartEnPairsData;               

    //Raw Q and TOF histograms
    std::map<PartEnPairType, std::vector<TH1F*>> _hQ[2];        
    std::map<PartEnPairType, std::vector<TH1F*>> _hTOF[2];      

    TF1* _funcdECal;                                            

    Bool_t _Debug;                                              

    //Functions
    void    InitHists(TLayer Layer);
    void    LoadSingleFileData(TString FileName);

    void    EnergyCalibration(TString OutputDir);
    void    CalibrateLayerDeltaE(std::ofstream *ofsSHOE, TLayer layer, TString OutputDir, TFile* fOut);
    void    TOFCalibration(TString OutputDir);
    void    CalibrateLayerTOF(std::ofstream *ofsSHOE, PartEnPairType PartEn, TLayer layer, TString OutputDir, TFile* fOut);

    void    SaveRawHistograms(TString OutputDir);
    void    ClearData(TLayer layer);

    Int_t   CalculatePositionID(Int_t XBar, Int_t YBar);
    void    CalculatePosIDtoBarsMap();

public:
    TOFWallCalibration();
    void    RunCalibration(TString OutputDir);
    void    LoadRecData(TString InputDataDir);
    void    LoadMCRefValues(TString MCRefValuesFile);
    void    SetDebugMode();
};

#endif
```


-------------------------------

Updated on 2021-12-29 at 15:21:51 +0000
