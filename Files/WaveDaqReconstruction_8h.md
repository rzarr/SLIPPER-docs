---
title: src/WaveDaqReconstruction.h
summary: Header of WaveDaqReconstruction.cxx. 

---

# src/WaveDaqReconstruction.h

Header of [WaveDaqReconstruction.cxx](/Files/WaveDaqReconstruction_8cxx.md#file-wavedaqreconstruction.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[WaveDaqReconstruction](/Classes/classWaveDaqReconstruction.md)** <br>Main class used to handle the whole Reconstruction process.  |

## Detailed Description

Header of [WaveDaqReconstruction.cxx](/Files/WaveDaqReconstruction_8cxx.md#file-wavedaqreconstruction.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef WaveDaqReconstruction_H
#define WaveDaqReconstruction_H
#include <stdio.h>
#include <TMath.h>
#include <TTree.h>
#include <TBranch.h>
#include <TString.h>
#include <TCanvas.h>
#include "TGaxis.h"

#include "CWaveFormContainer.h"
#include "WDChannelMap.h"
#include "CReadBinary.h"


class WaveDaqReconstruction
{
protected:
    //Output TFile
    TFile* fout;                                                    
    std::string OutputFileName;                                     

    // Channel maps
    WDChannelMap _WDChannelMap;                                     
    TGlobalToBarChIDpairMap _GlobalToBarChIDpairMap;                
    std::map<int, int> _TDCchMap;                                   
    
    // parameters
    Float_t _Gain;                                                  
    bool _IsTDAQ;                                                   
    
    //Map from board serial number to Id
    std::map<UShort_t ,Int_t> _BoardIdToIdMap;                      
    std::map<UShort_t, Int_t> _ActiveBoards;                        

    //Containers for binary file decoding and waveform analysis
    CReadBinary* _BinaryReader;                                     
    std::vector<CWaveFormContainer*> _WaveFormContainer;            
    std::vector<TCBDATA*> _TCBdata;                                 


    //Start Counter variables
    Float_t _SCTime;                                                
    Float_t _SCPedestal[NUMBEROFSCCHANNELS];                        
    Float_t _SCPedestalRMS[NUMBEROFSCCHANNELS];                     
    Float_t _SCAmplitude[NUMBEROFSCCHANNELS];                       
    Float_t _SCCharge[NUMBEROFSCCHANNELS];                          
    Float_t _SCRiseTime[NUMBEROFSCCHANNELS];                        

    //TW Debug or non-plotted variables
    Float_t _CPedestal[NUMBEROFGLOBALCHANNELSTW];                   
    Float_t _CPedestalRMS[NUMBEROFGLOBALCHANNELSTW];                
    Float_t _CAmplitude[NUMBEROFGLOBALCHANNELSTW];                  
    Float_t _CCharge[NUMBEROFGLOBALCHANNELSTW];                     
    Float_t _CRiseTime[NUMBEROFGLOBALCHANNELSTW];                   
    Float_t _CTimestamps[NUMBEROFGLOBALCHANNELSTW];                 
    Float_t _CTimestampsCorrJit[NUMBEROFGLOBALCHANNELSTW];          
    Float_t _CLK_Jitter[NUMBEROFGLOBALCHANNELSTW];                  
    Float_t _CLK_phase[MAXNUMBEROFBOARDS][2];                       
    Float_t _SC_CLK_phase;                                          

    //TW Channel level variables
    Float_t _CPedA[NUMBEROFTWBARS];                                 
    Float_t _CPedB[NUMBEROFTWBARS];                                 
    Float_t _CPedRMSA[NUMBEROFTWBARS];                              
    Float_t _CPedRMSB[NUMBEROFTWBARS];                              
    Float_t _CAmpA[NUMBEROFTWBARS];                                 
    Float_t _CAmpB[NUMBEROFTWBARS];                                 
    Float_t _CChargeA[NUMBEROFTWBARS];                              
    Float_t _CChargeB[NUMBEROFTWBARS];                              
    Float_t _CRiseTimeA[NUMBEROFTWBARS];                            
    Float_t _CRiseTimeB[NUMBEROFTWBARS];                            
    Float_t _CTimeA[NUMBEROFTWBARS];                                
    Float_t _CTimeB[NUMBEROFTWBARS];                                

    //CALO variables
    Float_t _CALOPedestal[NUMBEROFCRYSTALS];                        
    Float_t _CALOPedestalRMS[NUMBEROFCRYSTALS];                     
    Float_t _CALOAmplitude[NUMBEROFCRYSTALS];                       
    Float_t _CALOCharge[NUMBEROFCRYSTALS];                          
    Float_t _CALORiseTime[NUMBEROFCRYSTALS];                        
    Float_t _CALOTimestamps[NUMBEROFCRYSTALS];                      
    Float_t _CALOTimestampsCorrJit[NUMBEROFCRYSTALS];               

    //Neutron variables
    Float_t _NFPed[NEUTRONFASTCHANNELS];                            
    Float_t _NFPedRMS[NEUTRONFASTCHANNELS];                         
    Float_t _NFAmp[NEUTRONFASTCHANNELS];                            
    Float_t _NFCharge[NEUTRONFASTCHANNELS];                         
    Float_t _NFTime[NEUTRONFASTCHANNELS];                           
    Float_t _NFRiseTime[NEUTRONFASTCHANNELS];                       
    Float_t _NSPed[NEUTRONSLOWCHANNELS];                            
    Float_t _NSPedRMS[NEUTRONSLOWCHANNELS];                         
    Float_t _NSAmp[NEUTRONSLOWCHANNELS];                            
    Float_t _NSCharge[NEUTRONSLOWCHANNELS];                         
    Float_t _NSTime[NEUTRONSLOWCHANNELS];                           
    Float_t _NSRiseTime[NEUTRONSLOWCHANNELS];                       

    //TW Bar level variables
    Float_t _BCharge[NUMBEROFTWBARS];                               
    Float_t _BTimestamps[NUMBEROFTWBARS];                           
    Float_t _BDeltaT[NUMBEROFTWBARS];                               
    Float_t _BCratio[NUMBEROFTWBARS];                               

    //Higher level variables
    Float_t _TOF[NUMBEROFTWBARS];                                   

    //Varibles for neutron waveforms saving
    NeutronWF* _NS_WF;                                              
    NeutronWF* _NF_WF;                                              
    UShort_t _NbSlow;                                               
    UShort_t _NbFast;                                               
    Bool_t _NeutronOn;                                              
    Bool_t _SaveNeutrons;                                           

    //TDC Timestamp
    Float_t _TDCTime[4];                                            

    //Trigger variables
    Int_t _TriggerType;                                             
    Bool_t _IsFragTriggerOn;                                        
    Int_t _TrigTP;                                                  
    Int_t _TrigFP;                                                  
    Int_t _TrigTN;                                                  
    Int_t _TrigFN;                                                  
    std::map<Int_t, std::pair<Float_t, Float_t>> _TrigCalMap;       
    Float_t _TriggerTh[NUMBEROFTRIGGERCHANNELS];                    

    //Tags
    WDTag _WDTags;                                                  
    TDAQTag _TDAQTags;                                              

    //Debug variables
    bool _Debug;                                                    
    bool _EnableHisto;                                              
    bool _TriggerEnable;                                            
    int _FirstEventToSave;                                          
    int _LastEventToSave;                                           
    int _Event;                                                     

    //Histograms declaration
    TH1F* _hitmap_Bars;                                             
    TH1F* _hitmap_Channels_Rear;                                    
    TH1F* _hitmap_Channels_Front;                                   
    TH2F* _hitmap_MB;                                               
    TH2F* _hitmap_frag;                                             
    TH2F* _hitmap_all;                                              
    TH2F* _hTGEN_MB = nullptr;                                      
    TH2F* _hTGEN_frag = nullptr;                                    
    TH1I* _hTriggerPattern = nullptr;                               
    TH1I* _hTriggerRates = nullptr;                                 
    TH1F** _hTrigAmp = new TH1F*[NUMBEROFTRIGGERCHANNELS];          
    TH1I* _hCALOMultiplicity;                                       

    //Main event loop for reconstruction
    void    LoopEvent(TTree* RecTree);

    //Waveform level analysis
    void    AnalyzeWaveformsSC(UShort_t board);
    void    AnalyzeWaveformsTW(UShort_t board);
    void    AnalyzeWaveformsCALO(UShort_t board);
    void    AnalyzeWaveformsNeutrons(UShort_t board);
    void    FillNeutronWaveforms(UShort_t board);
    void    EvalCLKJitter(int boardindex, Int_t globalch, int channel);
    Float_t CLKAnalysis(int boardindex, int channel);

    //TW bar level information
    void    AnalyzeSingleBarEvent(Int_t BarId);
    Float_t GetEventRawTimestamp(Int_t BarId);
    Float_t GetEventRawEnergy(Int_t BarId);
    Float_t GetDeltaT(Int_t BarId);
    Float_t GetCRatio(Int_t BarId);
    Float_t TimeOfFlight(Int_t BarId);

    //Trigger functions
    void    CheckFragTriggerConditions();
    void    PrintTriggerEfficiency();

    //Input/Output + checks
    void    GetFileTags(std::string FileName); //Get the file tags from the name
    void    SetOutputTreeBranches(TTree* RecTree); //Set the branches of the output tree
    void    SetOutputNeutronWF(TTree* RecTree); //Set the branches of the output tree when neutron WFs are saved
    void    SetOutputDataToZero(); //Initialize data of output tree to zero at the beginning of each cycle
    void    CheckLoadedBoards();

    //Histograms
    void    CreateHistograms();
    void    FillHistograms();

public:
    WaveDaqReconstruction();
    
    void    RunReconstruction(std::string FileName, std::string TimeCalFileName, int nEv);

    //Configuration files
    void    LoadChannelMap(std::string FileName);
    void    LoadTriggerCalibration(std::string FileName);

    //Input/Output + global flags
    void    SetOutputFileName(std::string FileName);
    void    SetDebugMode(Int_t first_ev, Int_t last_ev);
    void    EnableHistograms();
    void    SetTDAQfile();
    void    SetSaveNeutrons();
    void    SetGain(Float_t Gain);
};
#endif
```


-------------------------------

Updated on 2022-01-12 at 10:56:23 +0000
