---
title: LivePlots
summary: Class containing all the methods used in the LivePlotter executable. 

---

# LivePlots



Class containing all the methods used in the LivePlotter executable. 

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[LivePlots](/Classes/classLivePlots.md#function-liveplots)**()<br>Default constructor.  |
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
| virtual void | **[UpdateCanvas](/Classes/classLivePlots.md#function-updatecanvas)**()<br>Update all the Canvas objects in the class.  |
| virtual Bool_t | **[UpdateFileList](/Classes/classLivePlots.md#function-updatefilelist)**()<br>Update the list of files in the directory.  |
| virtual void | **[UpdatePlots](/Classes/classLivePlots.md#function-updateplots)**()<br>Update the booked plots.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_CALOAmp](/Classes/classLivePlots.md#variable--caloamp)** <br>Variable for CALO amplitude reading.  |
| Float_t | **[_CALOEnergy](/Classes/classLivePlots.md#variable--caloenergy)** <br>Variable for CALO energy reading.  |
| std::map< Int_t, TCanvas * > | **[_cCALOAmp](/Classes/classLivePlots.md#variable--ccaloamp)** <br>Canvas for CALO Amplitude.  |
| TCanvas * | **[_cCALOenCorr](/Classes/classLivePlots.md#variable--ccaloencorr)** <br>Canvas for CALO enegry correlation plots.  |
| TCanvas * | **[_cCALOenTOF](/Classes/classLivePlots.md#variable--ccaloentof)** <br>Canvas for CALO energy vs TOF plots.  |
| TCanvas * | **[_cCALOhitmap](/Classes/classLivePlots.md#variable--ccalohitmap)** <br>Canvas for CALO hitmap.  |
| TCanvas * | **[_cDeltaEvsE](/Classes/classLivePlots.md#variable--cdeltaevse)** <br>Canvas for dE vs E plot.  |
| TCanvas * | **[_cDeltaEvsE_angle](/Classes/classLivePlots.md#variable--cdeltaevse-angle)** <br>Canvas for dE vs E plot.  |
| TCanvas * | **[_cDeltaT_FR](/Classes/classLivePlots.md#variable--cdeltat-fr)** <br>Canvas for DeltaT Front-Rear at TW center.  |
| TCanvas * | **[_cdEvsTOFcenter](/Classes/classLivePlots.md#variable--cdevstofcenter)** <br>Canvas for front/rear layer raw dEvsTOF.  |
| std::map< Int_t, TCanvas * > | **[_cFragCharge](/Classes/classLivePlots.md#variable--cfragcharge)** <br>Canvas of Fragmentation Trigger charge spectra.  |
| TCanvas * | **[_cHitmapFrag](/Classes/classLivePlots.md#variable--chitmapfrag)** <br>Canvas for TW hitmap w/ fragmentation trigger.  |
| TCanvas * | **[_cHitmapFragSW](/Classes/classLivePlots.md#variable--chitmapfragsw)** <br>Canvas for TW hitmap w/ fragmentation trigger.  |
| TCanvas * | **[_cHitmapMB](/Classes/classLivePlots.md#variable--chitmapmb)** <br>Canvas for TW hitmap w/ MB trigger.  |
| std::map< Int_t, TCanvas * > | **[_cMBCharge](/Classes/classLivePlots.md#variable--cmbcharge)** <br>Canvas of MB charge spectra.  |
| TCanvas * | **[_cMultiplicity](/Classes/classLivePlots.md#variable--cmultiplicity)** <br>Canvas for TW-CALO multiplivity plot.  |
| TCanvas * | **[_cPileUp](/Classes/classLivePlots.md#variable--cpileup)** <br>Canvas for Pile-Up monitoring.  |
| TCanvas * | **[_cPileUpRC](/Classes/classLivePlots.md#variable--cpileuprc)** <br>Canvas for RC Pile-Up monitoring.  |
| TCanvas * | **[_cRC_SC_TOF](/Classes/classLivePlots.md#variable--crc-sc-tof)** <br>Canvas for RC-SC TOF plots.  |
| TCanvas * | **[_cRC_TW_TOF](/Classes/classLivePlots.md#variable--crc-tw-tof)** <br>Canvas for RC-TW TOF plots.  |
| TCanvas * | **[_cRCcharge](/Classes/classLivePlots.md#variable--crccharge)** <br>Canvas for RC charge plots.  |
| TCanvas * | **[_cTWchCounts](/Classes/classLivePlots.md#variable--ctwchcounts)** <br>Canvas for TW channel counts monitoring.  |
| TCanvas * | **[_cTWchSat](/Classes/classLivePlots.md#variable--ctwchsat)** <br>Canvas for TW channel saturation monitoring.  |
| UInt_t | **[_FileCount](/Classes/classLivePlots.md#variable--filecount)** <br>Counter for number of files found.  |
| TGraph * | **[_gPileUp](/Classes/classLivePlots.md#variable--gpileup)** <br>Graph for Pile-Up monitoring.  |
| TGraph * | **[_gPileUpRC](/Classes/classLivePlots.md#variable--gpileuprc)** <br>Graph for RC Pile-Up monitoring.  |
| std::map< Int_t, TH1F * > | **[_hCALOAmp](/Classes/classLivePlots.md#variable--hcaloamp)** <br>Histograms for CALO amplitude.  |
| TH2F * | **[_hCALOenCorr](/Classes/classLivePlots.md#variable--hcaloencorr)** <br>Histogram for CALO energy correlation plots in events with multiplicity = 2.  |
| TH2F * | **[_hCALOenTOF](/Classes/classLivePlots.md#variable--hcaloentof)** <br>Histogram for CALO energy vs TOF plots.  |
| TH2D * | **[_hCALOhitmap](/Classes/classLivePlots.md#variable--hcalohitmap)** <br>2D histogram for CALO hitmap  |
| TH2D * | **[_hDeltaEvsE](/Classes/classLivePlots.md#variable--hdeltaevse)** <br>Histogram for dE vs E plot.  |
| TH2D * | **[_hDeltaEvsE_angle](/Classes/classLivePlots.md#variable--hdeltaevse-angle)** <br>Histogram for dE vs E plot.  |
| TH1F * | **[_hDeltaT_FR](/Classes/classLivePlots.md#variable--hdeltat-fr)** <br>Histogram for DeltaT Front-Rear at TW center.  |
| TH2F * | **[_hdEvsTOFcenter](/Classes/classLivePlots.md#variable--hdevstofcenter)** <br>histogram for front/rear layer raw dEvsTOF  |
| std::map< Int_t, TH1F * > | **[_hFragCharge](/Classes/classLivePlots.md#variable--hfragcharge)** <br>Histograms of Fragmentation Trigger charge spectra.  |
| TH2F * | **[_hHitmapFrag](/Classes/classLivePlots.md#variable--hhitmapfrag)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hHitmapFragSW](/Classes/classLivePlots.md#variable--hhitmapfragsw)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hHitmapMB](/Classes/classLivePlots.md#variable--hhitmapmb)** <br>Histogram for TW hitmap w/ MB trigger.  |
| std::map< Int_t, TH1F * > | **[_hMBCharge](/Classes/classLivePlots.md#variable--hmbcharge)** <br>Histograms of MBB charge spectra.  |
| std::map< Int_t, TH1F * > | **[_hRC_SC_TOF](/Classes/classLivePlots.md#variable--hrc-sc-tof)** <br>Histograms for RC-SC TOF plots.  |
| std::map< Int_t, TH1F * > | **[_hRC_TW_TOF](/Classes/classLivePlots.md#variable--hrc-tw-tof)** <br>Histograms for RC-TW TOF plots.  |
| std::map< Int_t, TH1F * > | **[_hRCcharge](/Classes/classLivePlots.md#variable--hrccharge)** <br>Histograms for RC charge plots.  |
| TH1I * | **[_hTWchCounts](/Classes/classLivePlots.md#variable--htwchcounts)** <br>Histograms for TW channel counts monitoring.  |
| TH1I * | **[_hTWchSat](/Classes/classLivePlots.md#variable--htwchsat)** <br>Histograms for TW channel saturation monitoring.  |
| TH2I * | **[_hTWmultiVsCALOmulti](/Classes/classLivePlots.md#variable--htwmultivscalomulti)** <br>2D histogram for TW-CALO multiplivity  |
| Bool_t | **[_IsFragTriggerSWOn](/Classes/classLivePlots.md#variable--isfragtriggerswon)**  |
| std::map< Int_t, TLegend * > | **[_lCALOAmp](/Classes/classLivePlots.md#variable--lcaloamp)** <br>Legend for CALO amplitude plots.  |
| std::map< Int_t, TLegend * > | **[_lFragCharge](/Classes/classLivePlots.md#variable--lfragcharge)** <br>Legend of Fragmentation Trigger charge spectra.  |
| std::vector< TCanvas * > | **[_ListOfCanvas](/Classes/classLivePlots.md#variable--listofcanvas)** <br>List of Canvas to update.  |
| std::vector< TString > | **[_ListOfFiles](/Classes/classLivePlots.md#variable--listoffiles)** <br>List of the .root files in the wanted directory.  |
| std::map< Int_t, TLegend * > | **[_lMBCharge](/Classes/classLivePlots.md#variable--lmbcharge)** <br>Legend of MB charge spectra.  |
| TLegend * | **[_lRC_SC_TOF](/Classes/classLivePlots.md#variable--lrc-sc-tof)** <br>Legend for RC-SC TOF plots.  |
| TLegend * | **[_lRC_TW_TOF](/Classes/classLivePlots.md#variable--lrc-tw-tof)** <br>Legend for RC-TW TOF plots.  |
| TLegend * | **[_lRCcharge](/Classes/classLivePlots.md#variable--lrccharge)** <br>Legend for RC charge plots.  |
| TLegend * | **[_lTWchCounts](/Classes/classLivePlots.md#variable--ltwchcounts)** <br>Legend for TW channel counts monitoring.  |
| TLegend * | **[_lTWchSat](/Classes/classLivePlots.md#variable--ltwchsat)** <br>Legend for TW channel saturation monitoring.  |
| std::map< Int_t, Double_t > | **[_maxFragCharge](/Classes/classLivePlots.md#variable--maxfragcharge)** <br>Maximum of charge plots for axis rescaling.  |
| std::map< Int_t, Double_t > | **[_maxMBCharge](/Classes/classLivePlots.md#variable--maxmbcharge)** <br>Maximum of charge plots for axis rescaling.  |
| TSystemDirectory * | **[_OutDir](/Classes/classLivePlots.md#variable--outdir)** <br>Output directory of the reconstruction executable.  |
| Bool_t | **[_pUpFlag](/Classes/classLivePlots.md#variable--pupflag)** <br>Variable for pile-up flagging in SC.  |
| Bool_t | **[_pUpFlagRC](/Classes/classLivePlots.md#variable--pupflagrc)** <br>Variable for pile-up flagging in RC.  |
| Float_t | **[_RCCharge](/Classes/classLivePlots.md#variable--rccharge)** <br>Variable for RC raw channel charge.  |
| Float_t | **[_RCTime](/Classes/classLivePlots.md#variable--rctime)** <br>Variable for RC raw time readout.  |
| Float_t | **[_RCTotCharge](/Classes/classLivePlots.md#variable--rctotcharge)** <br>Variable for RC raw total charge.  |
| Float_t | **[_SCTime](/Classes/classLivePlots.md#variable--sctime)** <br>Variable for SC raw time readout.  |
| Float_t | **[_SCTotCharge](/Classes/classLivePlots.md#variable--sctotcharge)** <br>Variable for SC raw total charge.  |
| Float_t | **[_TWampA](/Classes/classLivePlots.md#variable--twampa)** <br>Variable for TW channel A amplitude.  |
| Float_t | **[_TWampB](/Classes/classLivePlots.md#variable--twampb)** <br>Variable for TW channel B amplitude.  |
| Float_t | **[_TWCharge](/Classes/classLivePlots.md#variable--twcharge)** <br>Variable for TW raw dE readout.  |
| Float_t | **[_TWTime](/Classes/classLivePlots.md#variable--twtime)** <br>Variable for TW raw bar time readout.  |
| Float_t | **[_TWtof](/Classes/classLivePlots.md#variable--twtof)** <br>Variable for TW raw TOF readout.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classLivePlots.md#variable--wdchannelmap)** <br>Channel Map.  |
| std::vector< Int_t > | **[_xPileUp](/Classes/classLivePlots.md#variable--xpileup)** <br>x-values of Pile-Up plot  |
| std::vector< Int_t > | **[_xPileUpRC](/Classes/classLivePlots.md#variable--xpileuprc)** <br>x-values of RC Pile-Up plot  |
| std::vector< Float_t > | **[_yPileUp](/Classes/classLivePlots.md#variable--ypileup)** <br>y-values of Pile-Up plot  |
| std::vector< Float_t > | **[_yPileUpRC](/Classes/classLivePlots.md#variable--ypileuprc)** <br>y-values of RC Pile-Up plot  |

## Public Functions Documentation

### function LivePlots

```cpp
LivePlots()
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

### function UpdateCanvas

```cpp
virtual void UpdateCanvas()
```

Update all the Canvas objects in the class. 

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

### variable _cCALOAmp

```cpp
std::map< Int_t, TCanvas * > _cCALOAmp;
```

Canvas for CALO Amplitude. 

### variable _cCALOenCorr

```cpp
TCanvas * _cCALOenCorr;
```

Canvas for CALO enegry correlation plots. 

### variable _cCALOenTOF

```cpp
TCanvas * _cCALOenTOF;
```

Canvas for CALO energy vs TOF plots. 

### variable _cCALOhitmap

```cpp
TCanvas * _cCALOhitmap;
```

Canvas for CALO hitmap. 

### variable _cDeltaEvsE

```cpp
TCanvas * _cDeltaEvsE;
```

Canvas for dE vs E plot. 

### variable _cDeltaEvsE_angle

```cpp
TCanvas * _cDeltaEvsE_angle;
```

Canvas for dE vs E plot. 

### variable _cDeltaT_FR

```cpp
TCanvas * _cDeltaT_FR;
```

Canvas for DeltaT Front-Rear at TW center. 

### variable _cdEvsTOFcenter

```cpp
TCanvas * _cdEvsTOFcenter;
```

Canvas for front/rear layer raw dEvsTOF. 

### variable _cFragCharge

```cpp
std::map< Int_t, TCanvas * > _cFragCharge;
```

Canvas of Fragmentation Trigger charge spectra. 

### variable _cHitmapFrag

```cpp
TCanvas * _cHitmapFrag;
```

Canvas for TW hitmap w/ fragmentation trigger. 

### variable _cHitmapFragSW

```cpp
TCanvas * _cHitmapFragSW;
```

Canvas for TW hitmap w/ fragmentation trigger. 

### variable _cHitmapMB

```cpp
TCanvas * _cHitmapMB;
```

Canvas for TW hitmap w/ MB trigger. 

### variable _cMBCharge

```cpp
std::map< Int_t, TCanvas * > _cMBCharge;
```

Canvas of MB charge spectra. 

### variable _cMultiplicity

```cpp
TCanvas * _cMultiplicity;
```

Canvas for TW-CALO multiplivity plot. 

### variable _cPileUp

```cpp
TCanvas * _cPileUp;
```

Canvas for Pile-Up monitoring. 

### variable _cPileUpRC

```cpp
TCanvas * _cPileUpRC;
```

Canvas for RC Pile-Up monitoring. 

### variable _cRC_SC_TOF

```cpp
TCanvas * _cRC_SC_TOF;
```

Canvas for RC-SC TOF plots. 

### variable _cRC_TW_TOF

```cpp
TCanvas * _cRC_TW_TOF;
```

Canvas for RC-TW TOF plots. 

### variable _cRCcharge

```cpp
TCanvas * _cRCcharge;
```

Canvas for RC charge plots. 

### variable _cTWchCounts

```cpp
TCanvas * _cTWchCounts;
```

Canvas for TW channel counts monitoring. 

### variable _cTWchSat

```cpp
TCanvas * _cTWchSat;
```

Canvas for TW channel saturation monitoring. 

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

### variable _hCALOAmp

```cpp
std::map< Int_t, TH1F * > _hCALOAmp;
```

Histograms for CALO amplitude. 

### variable _hCALOenCorr

```cpp
TH2F * _hCALOenCorr;
```

Histogram for CALO energy correlation plots in events with multiplicity = 2. 

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

### variable _hDeltaEvsE

```cpp
TH2D * _hDeltaEvsE;
```

Histogram for dE vs E plot. 

### variable _hDeltaEvsE_angle

```cpp
TH2D * _hDeltaEvsE_angle;
```

Histogram for dE vs E plot. 

### variable _hDeltaT_FR

```cpp
TH1F * _hDeltaT_FR;
```

Histogram for DeltaT Front-Rear at TW center. 

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

### variable _hHitmapFrag

```cpp
TH2F * _hHitmapFrag;
```

Histogram for TW hitmap w/ fragmentation trigger. 

### variable _hHitmapFragSW

```cpp
TH2F * _hHitmapFragSW;
```

Histogram for TW hitmap w/ fragmentation trigger. 

### variable _hHitmapMB

```cpp
TH2F * _hHitmapMB;
```

Histogram for TW hitmap w/ MB trigger. 

### variable _hMBCharge

```cpp
std::map< Int_t, TH1F * > _hMBCharge;
```

Histograms of MBB charge spectra. 

### variable _hRC_SC_TOF

```cpp
std::map< Int_t, TH1F * > _hRC_SC_TOF;
```

Histograms for RC-SC TOF plots. 

### variable _hRC_TW_TOF

```cpp
std::map< Int_t, TH1F * > _hRC_TW_TOF;
```

Histograms for RC-TW TOF plots. 

### variable _hRCcharge

```cpp
std::map< Int_t, TH1F * > _hRCcharge;
```

Histograms for RC charge plots. 

### variable _hTWchCounts

```cpp
TH1I * _hTWchCounts;
```

Histograms for TW channel counts monitoring. 

### variable _hTWchSat

```cpp
TH1I * _hTWchSat;
```

Histograms for TW channel saturation monitoring. 

### variable _hTWmultiVsCALOmulti

```cpp
TH2I * _hTWmultiVsCALOmulti;
```

2D histogram for TW-CALO multiplivity 

### variable _IsFragTriggerSWOn

```cpp
Bool_t _IsFragTriggerSWOn;
```


### variable _lCALOAmp

```cpp
std::map< Int_t, TLegend * > _lCALOAmp;
```

Legend for CALO amplitude plots. 

### variable _lFragCharge

```cpp
std::map< Int_t, TLegend * > _lFragCharge;
```

Legend of Fragmentation Trigger charge spectra. 

### variable _ListOfCanvas

```cpp
std::vector< TCanvas * > _ListOfCanvas;
```

List of Canvas to update. 

### variable _ListOfFiles

```cpp
std::vector< TString > _ListOfFiles;
```

List of the .root files in the wanted directory. 

### variable _lMBCharge

```cpp
std::map< Int_t, TLegend * > _lMBCharge;
```

Legend of MB charge spectra. 

### variable _lRC_SC_TOF

```cpp
TLegend * _lRC_SC_TOF;
```

Legend for RC-SC TOF plots. 

### variable _lRC_TW_TOF

```cpp
TLegend * _lRC_TW_TOF;
```

Legend for RC-TW TOF plots. 

### variable _lRCcharge

```cpp
TLegend * _lRCcharge;
```

Legend for RC charge plots. 

### variable _lTWchCounts

```cpp
TLegend * _lTWchCounts;
```

Legend for TW channel counts monitoring. 

### variable _lTWchSat

```cpp
TLegend * _lTWchSat;
```

Legend for TW channel saturation monitoring. 

### variable _maxFragCharge

```cpp
std::map< Int_t, Double_t > _maxFragCharge;
```

Maximum of charge plots for axis rescaling. 

### variable _maxMBCharge

```cpp
std::map< Int_t, Double_t > _maxMBCharge;
```

Maximum of charge plots for axis rescaling. 

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

### variable _xPileUp

```cpp
std::vector< Int_t > _xPileUp;
```

x-values of Pile-Up plot 

### variable _xPileUpRC

```cpp
std::vector< Int_t > _xPileUpRC;
```

x-values of RC Pile-Up plot 

### variable _yPileUp

```cpp
std::vector< Float_t > _yPileUp;
```

y-values of Pile-Up plot 

### variable _yPileUpRC

```cpp
std::vector< Float_t > _yPileUpRC;
```

y-values of RC Pile-Up plot 

-------------------------------

Updated on 2022-11-07 at 18:21:11 +0000