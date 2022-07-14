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
| virtual void | **[SetOutputDirectory](/Classes/classLivePlots.md#function-setoutputdirectory)**(std::string outputdir)<br>Set the name of the output directory of the Reconstruction executable.  |
| virtual void | **[LoadChannelMap](/Classes/classLivePlots.md#function-loadchannelmap)**(std::string channelmap)<br>Load the WaveDAQ channel map of the campaign.  |
| virtual void | **[Run](/Classes/classLivePlots.md#function-run)**()<br>Run the online plotting.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[BookPlots](/Classes/classLivePlots.md#function-bookplots)**()<br>Book the plots to be updated online.  |
| virtual Bool_t | **[UpdateFileList](/Classes/classLivePlots.md#function-updatefilelist)**()<br>Update the list of files in the directory.  |
| virtual void | **[UpdatePlots](/Classes/classLivePlots.md#function-updateplots)**()<br>Update the booked plots.  |
| virtual void | **[UpdateCanvas](/Classes/classLivePlots.md#function-updatecanvas)**()<br>Update all the Canvas objects in the class.  |
| virtual Float_t | **[GetGamma](/Classes/classLivePlots.md#function-getgamma)**(Float_t tof)<br>Return the Lorentz gamma factor for a specific TOF value.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| TSystemDirectory * | **[_OutDir](/Classes/classLivePlots.md#variable--outdir)** <br>Output directory of the reconstruction executable.  |
| [WDChannelMap](/Classes/classWDChannelMap.md) | **[_WDChannelMap](/Classes/classLivePlots.md#variable--wdchannelmap)** <br>Channel Map.  |
| std::vector< TString > | **[_ListOfFiles](/Classes/classLivePlots.md#variable--listoffiles)** <br>List of the .root files in the wanted directory.  |
| Int_t | **[_FileCount](/Classes/classLivePlots.md#variable--filecount)** <br>Counter for number of files found.  |
| std::map< Int_t, TCanvas * > | **[_cFragCharge](/Classes/classLivePlots.md#variable--cfragcharge)**  |
| std::map< Int_t, TLegend * > | **[_lFragCharge](/Classes/classLivePlots.md#variable--lfragcharge)**  |
| std::map< Int_t, TH1F * > | **[_hFragCharge](/Classes/classLivePlots.md#variable--hfragcharge)** <br>Histograms of Fragmentation Trigger charge spectra.  |
| std::map< Int_t, Double_t > | **[_maxFragCharge](/Classes/classLivePlots.md#variable--maxfragcharge)** <br>Maximum of charge plots for axis rescaling.  |
| Float_t | **[_TWampA](/Classes/classLivePlots.md#variable--twampa)** <br>Variable for TW channel A amplitude.  |
| Float_t | **[_TWampB](/Classes/classLivePlots.md#variable--twampb)** <br>Variable for TW channel B amplitude.  |
| TCanvas * | **[_cTWchCounts](/Classes/classLivePlots.md#variable--ctwchcounts)** <br>Canvas for TW channel counts monitoring.  |
| TLegend * | **[_lTWchCounts](/Classes/classLivePlots.md#variable--ltwchcounts)** <br>Legend for TW channel counts monitoring.  |
| TH1I * | **[_hTWchCounts](/Classes/classLivePlots.md#variable--htwchcounts)** <br>Histograms for TW channel counts monitoring.  |
| TCanvas * | **[_cTWchSat](/Classes/classLivePlots.md#variable--ctwchsat)** <br>Canvas for TW channel saturation monitoring.  |
| TLegend * | **[_lTWchSat](/Classes/classLivePlots.md#variable--ltwchsat)** <br>Legend for TW channel saturation monitoring.  |
| TH1I * | **[_hTWchSat](/Classes/classLivePlots.md#variable--htwchsat)** <br>Histograms for TW channel saturation monitoring.  |
| TCanvas * | **[_cPileUp](/Classes/classLivePlots.md#variable--cpileup)** <br>Canvas for Pile-Up monitoring.  |
| TGraph * | **[_gPileUp](/Classes/classLivePlots.md#variable--gpileup)** <br>Graph for Pile-Up monitoring.  |
| std::vector< Float_t > | **[_yPileUp](/Classes/classLivePlots.md#variable--ypileup)** <br>y-values of Pile-Up plot  |
| std::vector< Int_t > | **[_xPileUp](/Classes/classLivePlots.md#variable--xpileup)** <br>x-values of Pile-Up plot  |
| TCanvas * | **[_cHitmapMB](/Classes/classLivePlots.md#variable--chitmapmb)** <br>Canvas for TW hitmap w/ MB trigger.  |
| TCanvas * | **[_cHitmapFrag](/Classes/classLivePlots.md#variable--chitmapfrag)** <br>Canvas for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hHitmapMB](/Classes/classLivePlots.md#variable--hhitmapmb)** <br>Histogram for TW hitmap w/ MB trigger.  |
| TH2F * | **[_hHitmapFrag](/Classes/classLivePlots.md#variable--hhitmapfrag)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |
| TCanvas * | **[_cCALOEnergy](/Classes/classLivePlots.md#variable--ccaloenergy)** <br>Canvas for CALO energy release.  |
| TLegend * | **[_lCALOEnergy](/Classes/classLivePlots.md#variable--lcaloenergy)** <br>Legend for CALO plots.  |
| TH1F * | **[_hCALOEnergy](/Classes/classLivePlots.md#variable--hcaloenergy)** <br>Histograms for CALO energy release.  |
| Float_t | **[_CALOEnergy](/Classes/classLivePlots.md#variable--caloenergy)** <br>Variable for CALO energy reading.  |
| TCanvas * | **[_cDeltaEvsE](/Classes/classLivePlots.md#variable--cdeltaevse)** <br>Canvas for dE vs E plot.  |
| TH2D * | **[_hDeltaEvsE](/Classes/classLivePlots.md#variable--hdeltaevse)** <br>Histogram for dE vs E plot.  |
| Float_t | **[_TWCharge](/Classes/classLivePlots.md#variable--twcharge)** <br>Variable for TW raw dE readout.  |
| Float_t | **[_TWtof](/Classes/classLivePlots.md#variable--twtof)** <br>Variable for TW raw TOF readout.  |
| TCanvas * | **[_cdEvsTOFcenter](/Classes/classLivePlots.md#variable--cdevstofcenter)** <br>Canvas for front/rear layer raw dEvsTOF.  |
| TH2F * | **[_hdEvsTOFcenter](/Classes/classLivePlots.md#variable--hdevstofcenter)** <br>histogram for front/rear layer raw dEvsTOF  |
| TCanvas * | **[_cCALOhitmap](/Classes/classLivePlots.md#variable--ccalohitmap)** <br>Canvas for CALO hitmap.  |
| TH2D * | **[_hCALOhitmap](/Classes/classLivePlots.md#variable--hcalohitmap)** <br>2D histogram for CALO hitmap  |
| TCanvas * | **[_cMultiplicity](/Classes/classLivePlots.md#variable--cmultiplicity)** <br>Canvas for TW-CALO multiplivity plot.  |
| TH2I * | **[_hTWmultiVsCALOmulti](/Classes/classLivePlots.md#variable--htwmultivscalomulti)** <br>2D histogram for TW-CALO multiplivity  |
| std::vector< TCanvas * > | **[_ListOfCanvas](/Classes/classLivePlots.md#variable--listofcanvas)** <br>List of Canvas to update.  |

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


## Protected Functions Documentation

### function BookPlots

```cpp
virtual void BookPlots()
```

Book the plots to be updated online. 

Contains all the definitions of canvases and histograms/graphs 


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


### function UpdateCanvas

```cpp
virtual void UpdateCanvas()
```

Update all the Canvas objects in the class. 

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

## Protected Attributes Documentation

### variable _OutDir

```cpp
TSystemDirectory * _OutDir;
```

Output directory of the reconstruction executable. 

### variable _WDChannelMap

```cpp
WDChannelMap _WDChannelMap;
```

Channel Map. 

### variable _ListOfFiles

```cpp
std::vector< TString > _ListOfFiles;
```

List of the .root files in the wanted directory. 

### variable _FileCount

```cpp
Int_t _FileCount;
```

Counter for number of files found. 

### variable _cFragCharge

```cpp
std::map< Int_t, TCanvas * > _cFragCharge;
```


### variable _lFragCharge

```cpp
std::map< Int_t, TLegend * > _lFragCharge;
```


### variable _hFragCharge

```cpp
std::map< Int_t, TH1F * > _hFragCharge;
```

Histograms of Fragmentation Trigger charge spectra. 

### variable _maxFragCharge

```cpp
std::map< Int_t, Double_t > _maxFragCharge;
```

Maximum of charge plots for axis rescaling. 

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

### variable _cTWchCounts

```cpp
TCanvas * _cTWchCounts;
```

Canvas for TW channel counts monitoring. 

### variable _lTWchCounts

```cpp
TLegend * _lTWchCounts;
```

Legend for TW channel counts monitoring. 

### variable _hTWchCounts

```cpp
TH1I * _hTWchCounts;
```

Histograms for TW channel counts monitoring. 

### variable _cTWchSat

```cpp
TCanvas * _cTWchSat;
```

Canvas for TW channel saturation monitoring. 

### variable _lTWchSat

```cpp
TLegend * _lTWchSat;
```

Legend for TW channel saturation monitoring. 

### variable _hTWchSat

```cpp
TH1I * _hTWchSat;
```

Histograms for TW channel saturation monitoring. 

### variable _cPileUp

```cpp
TCanvas * _cPileUp;
```

Canvas for Pile-Up monitoring. 

### variable _gPileUp

```cpp
TGraph * _gPileUp;
```

Graph for Pile-Up monitoring. 

### variable _yPileUp

```cpp
std::vector< Float_t > _yPileUp;
```

y-values of Pile-Up plot 

### variable _xPileUp

```cpp
std::vector< Int_t > _xPileUp;
```

x-values of Pile-Up plot 

### variable _cHitmapMB

```cpp
TCanvas * _cHitmapMB;
```

Canvas for TW hitmap w/ MB trigger. 

### variable _cHitmapFrag

```cpp
TCanvas * _cHitmapFrag;
```

Canvas for TW hitmap w/ fragmentation trigger. 

### variable _hHitmapMB

```cpp
TH2F * _hHitmapMB;
```

Histogram for TW hitmap w/ MB trigger. 

### variable _hHitmapFrag

```cpp
TH2F * _hHitmapFrag;
```

Histogram for TW hitmap w/ fragmentation trigger. 

### variable _cCALOEnergy

```cpp
TCanvas * _cCALOEnergy;
```

Canvas for CALO energy release. 

### variable _lCALOEnergy

```cpp
TLegend * _lCALOEnergy;
```

Legend for CALO plots. 

### variable _hCALOEnergy

```cpp
TH1F * _hCALOEnergy;
```

Histograms for CALO energy release. 

### variable _CALOEnergy

```cpp
Float_t _CALOEnergy;
```

Variable for CALO energy reading. 

### variable _cDeltaEvsE

```cpp
TCanvas * _cDeltaEvsE;
```

Canvas for dE vs E plot. 

### variable _hDeltaEvsE

```cpp
TH2D * _hDeltaEvsE;
```

Histogram for dE vs E plot. 

### variable _TWCharge

```cpp
Float_t _TWCharge;
```

Variable for TW raw dE readout. 

### variable _TWtof

```cpp
Float_t _TWtof;
```

Variable for TW raw TOF readout. 

### variable _cdEvsTOFcenter

```cpp
TCanvas * _cdEvsTOFcenter;
```

Canvas for front/rear layer raw dEvsTOF. 

### variable _hdEvsTOFcenter

```cpp
TH2F * _hdEvsTOFcenter;
```

histogram for front/rear layer raw dEvsTOF 

### variable _cCALOhitmap

```cpp
TCanvas * _cCALOhitmap;
```

Canvas for CALO hitmap. 

### variable _hCALOhitmap

```cpp
TH2D * _hCALOhitmap;
```

2D histogram for CALO hitmap 

### variable _cMultiplicity

```cpp
TCanvas * _cMultiplicity;
```

Canvas for TW-CALO multiplivity plot. 

### variable _hTWmultiVsCALOmulti

```cpp
TH2I * _hTWmultiVsCALOmulti;
```

2D histogram for TW-CALO multiplivity 

### variable _ListOfCanvas

```cpp
std::vector< TCanvas * > _ListOfCanvas;
```

List of Canvas to update. 

-------------------------------

Updated on 2022-07-14 at 15:09:35 +0000