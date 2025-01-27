---
title: LivePlots
summary: Class containing all the methods used in the LivePlotter executable. 

---

# LivePlots



Class containing all the methods used in the LivePlotter executable. 

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[LivePlots](/Classes/classLivePlots.md#function-liveplots)**([SlipperGUI](/Classes/classSlipperGUI.md) * GUI)<br>Default constructor.  |
| virtual | **[~LivePlots](/Classes/classLivePlots.md#function-~liveplots)**()<br>Default destructor.  |
| virtual void | **[LoadChannelMap](/Classes/classLivePlots.md#function-loadchannelmap)**(std::string channelmap)<br>Load the WaveDAQ channel map of the campaign.  |
| virtual void | **[Run](/Classes/classLivePlots.md#function-run)**()<br>Run the online plotting.  |
| virtual void | **[SetOutputDirectory](/Classes/classLivePlots.md#function-setoutputdirectory)**(std::string outputdir)<br>Set the name of the output directory of the Reconstruction executable.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[AttachInputVariables](/Classes/classLivePlots.md#function-attachinputvariables)**(TTree * t)<br>Attach all the needed input variables, depending on the loaded detectors.  |
| virtual void | **[BookPlots](/Classes/classLivePlots.md#function-bookplots)**()<br>Book the plots to be updated online.  |
| virtual Float_t | **[GetGamma](/Classes/classLivePlots.md#function-getgamma)**(Float_t tof)<br>Return the Lorentz gamma factor for a specific TOF value.  |
| virtual Bool_t | **[UpdateFileList](/Classes/classLivePlots.md#function-updatefilelist)**()<br>Update the list of files in the directory.  |
| virtual void | **[UpdatePlots](/Classes/classLivePlots.md#function-updateplots)**()<br>Update the booked plots.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_CALOAmp](/Classes/classLivePlots.md#variable--caloamp)** <br>Variable for CALO amplitude reading.  |
| Float_t | **[_CALOEnergy](/Classes/classLivePlots.md#variable--caloenergy)** <br>Variable for CALO energy reading.  |
| UInt_t | **[_FileCount](/Classes/classLivePlots.md#variable--filecount)** <br>Counter for number of files found.  |
| TGraph * | **[_gPileUp](/Classes/classLivePlots.md#variable--gpileup)** <br>Graph for Pile-Up monitoring.  |
| TGraph * | **[_gPileUpRC](/Classes/classLivePlots.md#variable--gpileuprc)** <br>Graph for RC Pile-Up monitoring.  |
| std::map< Int_t, TGraph * > | **[_gTrigRate](/Classes/classLivePlots.md#variable--gtrigrate)** <br>Map of Graphs for single trigger rate plots.  |
| TMultiGraph * | **[_gTrigRatesAll](/Classes/classLivePlots.md#variable--gtrigratesall)** <br>MultiGraph for cumulative trigger rate monitoring.  |
| std::map< Int_t, THStack * > | **[_hAllvsFragSW](/Classes/classLivePlots.md#variable--hallvsfragsw)** <br>Stack for comparison in TW charge spectra w/ or w/out or SW-simulated fargmentation trigger.  |
| std::map< Int_t, TH1F * > | **[_hCALOAmp](/Classes/classLivePlots.md#variable--hcaloamp)** <br>Histograms for CALO amplitude.  |
| std::map< Int_t, THStack * > | **[_hCALOAmpStack](/Classes/classLivePlots.md#variable--hcaloampstack)** <br>Histograms stacks for CALO amplitude.  |
| TH2F * | **[_hCALOenCorr](/Classes/classLivePlots.md#variable--hcaloencorr)** <br>Histogram for CALO energy correlation plots in events with multiplicity = 2.  |
| std::map< Int_t, TH1F * > | **[_hCALOEnergy](/Classes/classLivePlots.md#variable--hcaloenergy)** <br>Histograms for CALO energy release.  |
| std::map< Int_t, THStack * > | **[_hCALOEnStack](/Classes/classLivePlots.md#variable--hcaloenstack)** <br>Histograms stacks for CALO energy release.  |
| TH2F * | **[_hCALOenTOF](/Classes/classLivePlots.md#variable--hcaloentof)** <br>Histogram for CALO energy vs TOF plots.  |
| TH2D * | **[_hCALOhitmap](/Classes/classLivePlots.md#variable--hcalohitmap)** <br>2D histogram for CALO hitmap  |
| TH1F * | **[_hDeltaT_FR](/Classes/classLivePlots.md#variable--hdeltat-fr)** <br>Histogram for DeltaT Front-Rear at TW center.  |
| TH2F * | **[_hdEvsTOFbar](/Classes/classLivePlots.md#variable--hdevstofbar)** <br>histogram for front/rear layer raw dEvsTOF  |
| TH2F * | **[_hdEvsTOFcenter](/Classes/classLivePlots.md#variable--hdevstofcenter)** <br>histogram for front/rear layer raw dEvsTOF  |
| std::map< Int_t, TH1F * > | **[_hFragCharge](/Classes/classLivePlots.md#variable--hfragcharge)** <br>Histograms of Fragmentation Trigger charge spectra.  |
| THStack * | **[_hFragChargeStack](/Classes/classLivePlots.md#variable--hfragchargestack)** <br>Stacks for TW charge spectra of central bars w/ Frag trigger.  |
| std::map< Int_t, TH1F * > | **[_hFragSWCharge](/Classes/classLivePlots.md#variable--hfragswcharge)** <br>Histograms of SW-simulated Fragmentation Trigger charge spectra.  |
| THStack * | **[_hFragSWChargeStack](/Classes/classLivePlots.md#variable--hfragswchargestack)** <br>Stacks for TW charge spectra of central bars w/ Frag trigger simulated with SW.  |
| std::map< Int_t, TH1F * > | **[_hMBCharge](/Classes/classLivePlots.md#variable--hmbcharge)** <br>Histograms of MB charge spectra.  |
| THStack * | **[_hMBChargeStack](/Classes/classLivePlots.md#variable--hmbchargestack)** <br>Stacks for TW charge spectra of central bars w/ MB trigger.  |
| std::map< Int_t, TH1F * > | **[_hRC_SC_TOF](/Classes/classLivePlots.md#variable--hrc-sc-tof)** <br>Histograms for RC-SC TOF plots.  |
| THStack * | **[_hRC_SC_TOF_Stack](/Classes/classLivePlots.md#variable--hrc-sc-tof-stack)** <br>Stack for RC-SC TOF plots.  |
| std::map< Int_t, TH1F * > | **[_hRC_TW_TOF](/Classes/classLivePlots.md#variable--hrc-tw-tof)** <br>Histograms for RC-TW TOF plots.  |
| THStack * | **[_hRC_TW_TOF_Stack](/Classes/classLivePlots.md#variable--hrc-tw-tof-stack)** <br>Stack for RC-TW TOF plots.  |
| std::map< Int_t, TH1F * > | **[_hRCcharge](/Classes/classLivePlots.md#variable--hrccharge)** <br>Histograms for RC charge plots.  |
| THStack * | **[_hRCchargeStack](/Classes/classLivePlots.md#variable--hrcchargestack)** <br>Stack for RC charge plots.  |
| std::map< Int_t, TH1F * > | **[_hSCchAmp](/Classes/classLivePlots.md#variable--hscchamp)** <br>Histograms for channel amplitudes in SC.  |
| THStack * | **[_hSCchAmpStack](/Classes/classLivePlots.md#variable--hscchampstack)** <br>Histogram stack for SC channel amplitudes.  |
| TH1F * | **[_hSCcharge](/Classes/classLivePlots.md#variable--hsccharge)** <br>Histogram for charge spectra in SC.  |
| TH1F * | **[_hSCchargeNoPU](/Classes/classLivePlots.md#variable--hscchargenopu)** <br>Histogram for charge spectra in SC w/out Pile-Up.  |
| THStack * | **[_hSCchargeStack](/Classes/classLivePlots.md#variable--hscchargestack)** <br>Histogram stack for charge spectra in SC w/ and w/out Pile-Up.  |
| TH2F * | **[_hTGEN_all](/Classes/classLivePlots.md#variable--htgen-all)** <br>Trigger generation (TGEN) for all acquired events.  |
| TH2F * | **[_hTGEN_frag](/Classes/classLivePlots.md#variable--htgen-frag)** <br>Trigger generation (TGEN) for Fragmentation Trigger Events.  |
| TH2F * | **[_hTGEN_MB](/Classes/classLivePlots.md#variable--htgen-mb)** <br>Trigger generation (TGEN) for Minimum Bias Events.  |
| TH1F * | **[_hTrigAmp](/Classes/classLivePlots.md#variable--htrigamp)** <br>Histogram to check triggre amplitudes.  |
| std::map< Int_t, TH1F * > | **[_hTWCharge](/Classes/classLivePlots.md#variable--htwcharge)** <br>Histograms of TW charge spectra of central bars.  |
| THStack * | **[_hTWChargeStack](/Classes/classLivePlots.md#variable--htwchargestack)** <br>Stacks for TW charge spectra of central bars.  |
| TH1I * | **[_hTWchCounts](/Classes/classLivePlots.md#variable--htwchcounts)** <br>Histograms for TW channel counts monitoring.  |
| THStack * | **[_hTWchCountsStack](/Classes/classLivePlots.md#variable--htwchcountsstack)** <br>Histogram stack for TW channel counts.  |
| TH1I * | **[_hTWchSat](/Classes/classLivePlots.md#variable--htwchsat)** <br>Histograms for TW channel saturation monitoring.  |
| THStack * | **[_hTWchSatStack](/Classes/classLivePlots.md#variable--htwchsatstack)** <br>Histogram stack for TW channel saturation counts.  |
| TH2F * | **[_hTWhitmapAll](/Classes/classLivePlots.md#variable--htwhitmapall)** <br>Histogram for TW hitmap w/ MB trigger.  |
| TH2F * | **[_hTWhitmapFrag](/Classes/classLivePlots.md#variable--htwhitmapfrag)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hTWhitmapFragSW](/Classes/classLivePlots.md#variable--htwhitmapfragsw)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hTWhitmapMB](/Classes/classLivePlots.md#variable--htwhitmapmb)** <br>Histogram for TW hitmap w/ MB trigger and NOT Fragmentation.  |
| TH2I * | **[_hTWmultiChVsCALOmulti](/Classes/classLivePlots.md#variable--htwmultichvscalomulti)** <br>2D histogram for TW-CALO multiplivity  |
| TH2I * | **[_hTWmultiVsCALOmulti](/Classes/classLivePlots.md#variable--htwmultivscalomulti)** <br>2D histogram for TW-CALO multiplivity  |
| std::vector< TString > | **[_ListOfFiles](/Classes/classLivePlots.md#variable--listoffiles)** <br>List of the .root files in the wanted directory.  |
| [SlipperGUI](/Classes/classSlipperGUI.md) * | **[_MyGUI](/Classes/classLivePlots.md#variable--mygui)** <br>Pointer to Graphical User Interface object.  |
| TSystemDirectory * | **[_OutDir](/Classes/classLivePlots.md#variable--outdir)** <br>Output directory of the reconstruction executable.  |
| Bool_t | **[_pUpFlag](/Classes/classLivePlots.md#variable--pupflag)** <br>Variable for pile-up flagging in SC.  |
| Bool_t | **[_pUpFlagRC](/Classes/classLivePlots.md#variable--pupflagrc)** <br>Variable for pile-up flagging in RC.  |
| Float_t | **[_RCCharge](/Classes/classLivePlots.md#variable--rccharge)** <br>Variable for RC raw channel charge.  |
| Float_t | **[_RCTime](/Classes/classLivePlots.md#variable--rctime)** <br>Variable for RC raw time readout.  |
| Float_t | **[_RCTotCharge](/Classes/classLivePlots.md#variable--rctotcharge)** <br>Variable for RC raw total charge.  |
| Float_t | **[_SCchAmp](/Classes/classLivePlots.md#variable--scchamp)** <br>Variable for SC channel amplitude.  |
| Float_t | **[_SCTime](/Classes/classLivePlots.md#variable--sctime)** <br>Variable for SC raw time readout.  |
| Float_t | **[_SCTotCharge](/Classes/classLivePlots.md#variable--sctotcharge)** <br>Variable for SC raw total charge.  |
| std::map< TString, Int_t > | **[_TriggersToPlot](/Classes/classLivePlots.md#variable--triggerstoplot)** <br>Map of trigger rates to monitor with WaveDAQ Id.  |
| Float_t | **[_TWampA](/Classes/classLivePlots.md#variable--twampa)** <br>Variable for TW channel A amplitude.  |
| Float_t | **[_TWampB](/Classes/classLivePlots.md#variable--twampb)** <br>Variable for TW channel B amplitude.  |
| Float_t | **[_TWCharge](/Classes/classLivePlots.md#variable--twcharge)** <br>Variable for TW raw dE readout.  |
| Float_t | **[_TWTime](/Classes/classLivePlots.md#variable--twtime)** <br>Variable for TW raw bar time readout.  |
| Float_t | **[_TWtof](/Classes/classLivePlots.md#variable--twtof)** <br>Variable for TW raw TOF readout.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classLivePlots.md#variable--wdchannelmap)** <br>Channel Map.  |
| UInt_t | **[_WDtime](/Classes/classLivePlots.md#variable--wdtime)** <br>variable for WaveDAQ acquisition time  |
| Int_t | **[_WDtriggerType](/Classes/classLivePlots.md#variable--wdtriggertype)** <br>variable for WaveDAQ trigger type  |
| Float_t | **[_WDtrigRates](/Classes/classLivePlots.md#variable--wdtrigrates)** <br>Variable for trigger rates.  |
| std::vector< Int_t > | **[_xPileUpRC](/Classes/classLivePlots.md#variable--xpileuprc)** <br>x-values of RC Pile-Up plot  |
| std::vector< Float_t > | **[_yPileUpRC](/Classes/classLivePlots.md#variable--ypileuprc)** <br>y-values of RC Pile-Up plot  |

## Public Functions Documentation

### function LivePlots

```cpp
LivePlots(
    SlipperGUI * GUI
)
```

Default constructor. 

### function ~LivePlots

```cpp
virtual ~LivePlots()
```

Default destructor. 

### function LoadChannelMap

```cpp
virtual void LoadChannelMap(
    std::string channelmap
)
```

Load the WaveDAQ channel map of the campaign. 

**Parameters**: 

  * **channelmap** path of the XML configuration file containing the WaveDAQ channel map 


### function Run

```cpp
virtual void Run()
```

Run the online plotting. 

This function checks if new files have been written to the output directory of Reconstruction and, if so, updates the relative plots. If an exception gets raised, the function terminates 


### function SetOutputDirectory

```cpp
virtual void SetOutputDirectory(
    std::string outputdir
)
```

Set the name of the output directory of the Reconstruction executable. 

**Parameters**: 

  * **outputdir** Path to the output directory 


This function sets the location where to find the .root files processed by the Reconstruction executable 


## Protected Functions Documentation

### function AttachInputVariables

```cpp
virtual void AttachInputVariables(
    TTree * t
)
```

Attach all the needed input variables, depending on the loaded detectors. 

**Parameters**: 

  * **t** Pointer to the input tree for the file being included 


### function BookPlots

```cpp
virtual void BookPlots()
```

Book the plots to be updated online. 

Contains all the definitions of canvases and histograms/graphs 


### function GetGamma

```cpp
virtual Float_t GetGamma(
    Float_t tof
)
```

Return the Lorentz gamma factor for a specific TOF value. 

**Parameters**: 

  * **tof** Time-Of-Flight of the particle 


**Return**: Lorentz gamma factor 

### function UpdateFileList

```cpp
virtual Bool_t UpdateFileList()
```

Update the list of files in the directory. 

**Return**: True if the list of files changed 

### function UpdatePlots

```cpp
virtual void UpdatePlots()
```

Update the booked plots. 

This function cycles through the newly found files and updates the single plots one by one. 


## Protected Attributes Documentation

### variable _CALOAmp

```cpp
Float_t _CALOAmp;
```

Variable for CALO amplitude reading. 

### variable _CALOEnergy

```cpp
Float_t _CALOEnergy;
```

Variable for CALO energy reading. 

### variable _FileCount

```cpp
UInt_t _FileCount;
```

Counter for number of files found. 

### variable _gPileUp

```cpp
TGraph * _gPileUp;
```

Graph for Pile-Up monitoring. 

### variable _gPileUpRC

```cpp
TGraph * _gPileUpRC;
```

Graph for RC Pile-Up monitoring. 

### variable _gTrigRate

```cpp
std::map< Int_t, TGraph * > _gTrigRate;
```

Map of Graphs for single trigger rate plots. 

### variable _gTrigRatesAll

```cpp
TMultiGraph * _gTrigRatesAll;
```

MultiGraph for cumulative trigger rate monitoring. 

### variable _hAllvsFragSW

```cpp
std::map< Int_t, THStack * > _hAllvsFragSW;
```

Stack for comparison in TW charge spectra w/ or w/out or SW-simulated fargmentation trigger. 

### variable _hCALOAmp

```cpp
std::map< Int_t, TH1F * > _hCALOAmp;
```

Histograms for CALO amplitude. 

### variable _hCALOAmpStack

```cpp
std::map< Int_t, THStack * > _hCALOAmpStack;
```

Histograms stacks for CALO amplitude. 

### variable _hCALOenCorr

```cpp
TH2F * _hCALOenCorr;
```

Histogram for CALO energy correlation plots in events with multiplicity = 2. 

### variable _hCALOEnergy

```cpp
std::map< Int_t, TH1F * > _hCALOEnergy;
```

Histograms for CALO energy release. 

### variable _hCALOEnStack

```cpp
std::map< Int_t, THStack * > _hCALOEnStack;
```

Histograms stacks for CALO energy release. 

### variable _hCALOenTOF

```cpp
TH2F * _hCALOenTOF;
```

Histogram for CALO energy vs TOF plots. 

### variable _hCALOhitmap

```cpp
TH2D * _hCALOhitmap;
```

2D histogram for CALO hitmap 

### variable _hDeltaT_FR

```cpp
TH1F * _hDeltaT_FR;
```

Histogram for DeltaT Front-Rear at TW center. 

### variable _hdEvsTOFbar

```cpp
TH2F * _hdEvsTOFbar;
```

histogram for front/rear layer raw dEvsTOF 

### variable _hdEvsTOFcenter

```cpp
TH2F * _hdEvsTOFcenter;
```

histogram for front/rear layer raw dEvsTOF 

### variable _hFragCharge

```cpp
std::map< Int_t, TH1F * > _hFragCharge;
```

Histograms of Fragmentation Trigger charge spectra. 

### variable _hFragChargeStack

```cpp
THStack * _hFragChargeStack;
```

Stacks for TW charge spectra of central bars w/ Frag trigger. 

### variable _hFragSWCharge

```cpp
std::map< Int_t, TH1F * > _hFragSWCharge;
```

Histograms of SW-simulated Fragmentation Trigger charge spectra. 

### variable _hFragSWChargeStack

```cpp
THStack * _hFragSWChargeStack;
```

Stacks for TW charge spectra of central bars w/ Frag trigger simulated with SW. 

### variable _hMBCharge

```cpp
std::map< Int_t, TH1F * > _hMBCharge;
```

Histograms of MB charge spectra. 

### variable _hMBChargeStack

```cpp
THStack * _hMBChargeStack;
```

Stacks for TW charge spectra of central bars w/ MB trigger. 

### variable _hRC_SC_TOF

```cpp
std::map< Int_t, TH1F * > _hRC_SC_TOF;
```

Histograms for RC-SC TOF plots. 

### variable _hRC_SC_TOF_Stack

```cpp
THStack * _hRC_SC_TOF_Stack;
```

Stack for RC-SC TOF plots. 

### variable _hRC_TW_TOF

```cpp
std::map< Int_t, TH1F * > _hRC_TW_TOF;
```

Histograms for RC-TW TOF plots. 

### variable _hRC_TW_TOF_Stack

```cpp
THStack * _hRC_TW_TOF_Stack;
```

Stack for RC-TW TOF plots. 

### variable _hRCcharge

```cpp
std::map< Int_t, TH1F * > _hRCcharge;
```

Histograms for RC charge plots. 

### variable _hRCchargeStack

```cpp
THStack * _hRCchargeStack;
```

Stack for RC charge plots. 

### variable _hSCchAmp

```cpp
std::map< Int_t, TH1F * > _hSCchAmp;
```

Histograms for channel amplitudes in SC. 

### variable _hSCchAmpStack

```cpp
THStack * _hSCchAmpStack;
```

Histogram stack for SC channel amplitudes. 

### variable _hSCcharge

```cpp
TH1F * _hSCcharge;
```

Histogram for charge spectra in SC. 

### variable _hSCchargeNoPU

```cpp
TH1F * _hSCchargeNoPU;
```

Histogram for charge spectra in SC w/out Pile-Up. 

### variable _hSCchargeStack

```cpp
THStack * _hSCchargeStack;
```

Histogram stack for charge spectra in SC w/ and w/out Pile-Up. 

### variable _hTGEN_all

```cpp
TH2F * _hTGEN_all;
```

Trigger generation (TGEN) for all acquired events. 

### variable _hTGEN_frag

```cpp
TH2F * _hTGEN_frag;
```

Trigger generation (TGEN) for Fragmentation Trigger Events. 

### variable _hTGEN_MB

```cpp
TH2F * _hTGEN_MB;
```

Trigger generation (TGEN) for Minimum Bias Events. 

### variable _hTrigAmp

```cpp
TH1F * _hTrigAmp;
```

Histogram to check triggre amplitudes. 

### variable _hTWCharge

```cpp
std::map< Int_t, TH1F * > _hTWCharge;
```

Histograms of TW charge spectra of central bars. 

### variable _hTWChargeStack

```cpp
THStack * _hTWChargeStack;
```

Stacks for TW charge spectra of central bars. 

### variable _hTWchCounts

```cpp
TH1I * _hTWchCounts;
```

Histograms for TW channel counts monitoring. 

### variable _hTWchCountsStack

```cpp
THStack * _hTWchCountsStack;
```

Histogram stack for TW channel counts. 

### variable _hTWchSat

```cpp
TH1I * _hTWchSat;
```

Histograms for TW channel saturation monitoring. 

### variable _hTWchSatStack

```cpp
THStack * _hTWchSatStack;
```

Histogram stack for TW channel saturation counts. 

### variable _hTWhitmapAll

```cpp
TH2F * _hTWhitmapAll;
```

Histogram for TW hitmap w/ MB trigger. 

### variable _hTWhitmapFrag

```cpp
TH2F * _hTWhitmapFrag;
```

Histogram for TW hitmap w/ fragmentation trigger. 

### variable _hTWhitmapFragSW

```cpp
TH2F * _hTWhitmapFragSW;
```

Histogram for TW hitmap w/ fragmentation trigger. 

### variable _hTWhitmapMB

```cpp
TH2F * _hTWhitmapMB;
```

Histogram for TW hitmap w/ MB trigger and NOT Fragmentation. 

### variable _hTWmultiChVsCALOmulti

```cpp
TH2I * _hTWmultiChVsCALOmulti;
```

2D histogram for TW-CALO multiplivity 

### variable _hTWmultiVsCALOmulti

```cpp
TH2I * _hTWmultiVsCALOmulti;
```

2D histogram for TW-CALO multiplivity 

### variable _ListOfFiles

```cpp
std::vector< TString > _ListOfFiles;
```

List of the .root files in the wanted directory. 

### variable _MyGUI

```cpp
SlipperGUI * _MyGUI;
```

Pointer to Graphical User Interface object. 

### variable _OutDir

```cpp
TSystemDirectory * _OutDir;
```

Output directory of the reconstruction executable. 

### variable _pUpFlag

```cpp
Bool_t _pUpFlag;
```

Variable for pile-up flagging in SC. 

### variable _pUpFlagRC

```cpp
Bool_t _pUpFlagRC;
```

Variable for pile-up flagging in RC. 

### variable _RCCharge

```cpp
Float_t _RCCharge;
```

Variable for RC raw channel charge. 

### variable _RCTime

```cpp
Float_t _RCTime;
```

Variable for RC raw time readout. 

### variable _RCTotCharge

```cpp
Float_t _RCTotCharge;
```

Variable for RC raw total charge. 

### variable _SCchAmp

```cpp
Float_t _SCchAmp;
```

Variable for SC channel amplitude. 

### variable _SCTime

```cpp
Float_t _SCTime;
```

Variable for SC raw time readout. 

### variable _SCTotCharge

```cpp
Float_t _SCTotCharge;
```

Variable for SC raw total charge. 

### variable _TriggersToPlot

```cpp
std::map< TString, Int_t > _TriggersToPlot;
```

Map of trigger rates to monitor with WaveDAQ Id. 

### variable _TWampA

```cpp
Float_t _TWampA;
```

Variable for TW channel A amplitude. 

### variable _TWampB

```cpp
Float_t _TWampB;
```

Variable for TW channel B amplitude. 

### variable _TWCharge

```cpp
Float_t _TWCharge;
```

Variable for TW raw dE readout. 

### variable _TWTime

```cpp
Float_t _TWTime;
```

Variable for TW raw bar time readout. 

### variable _TWtof

```cpp
Float_t _TWtof;
```

Variable for TW raw TOF readout. 

### variable _WDChannelMap

```cpp
WDChannelMap _WDChannelMap;
```

Channel Map. 

### variable _WDtime

```cpp
UInt_t _WDtime;
```

variable for WaveDAQ acquisition time 

### variable _WDtriggerType

```cpp
Int_t _WDtriggerType;
```

variable for WaveDAQ trigger type 

### variable _WDtrigRates

```cpp
Float_t _WDtrigRates;
```

Variable for trigger rates. 

### variable _xPileUpRC

```cpp
std::vector< Int_t > _xPileUpRC;
```

x-values of RC Pile-Up plot 

### variable _yPileUpRC

```cpp
std::vector< Float_t > _yPileUpRC;
```

y-values of RC Pile-Up plot 

-------------------------------

Updated on 2025-01-27 at 17:57:12 +0000