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
| virtual void | **[Run](/Classes/classLivePlots.md#function-run)**()<br>Run the online plotting.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[BookPlots](/Classes/classLivePlots.md#function-bookplots)**()<br>Book the plots to be updated online.  |
| virtual Bool_t | **[UpdateFileList](/Classes/classLivePlots.md#function-updatefilelist)**()<br>Update the list of files in the directory.  |
| virtual void | **[UpdatePlots](/Classes/classLivePlots.md#function-updateplots)**()<br>Update the booked plots.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| TSystemDirectory * | **[_OutDir](/Classes/classLivePlots.md#variable--outdir)** <br>Output directory of the reconstruction executable.  |
| std::vector< TString > | **[_ListOfFiles](/Classes/classLivePlots.md#variable--listoffiles)** <br>List of the .root files in the wanted directory.  |
| Int_t | **[_FileCount](/Classes/classLivePlots.md#variable--filecount)** <br>Counter for number of files found.  |
| std::map< Int_t, TCanvas * > | **[_cFragCharge](/Classes/classLivePlots.md#variable--cfragcharge)**  |
| std::map< Int_t, TH1F * > | **[_hFragCharge](/Classes/classLivePlots.md#variable--hfragcharge)** <br>Histograms of Fragmentation Trigger charge spectra.  |
| TCanvas * | **[_cTrigAmp](/Classes/classLivePlots.md#variable--ctrigamp)** <br>Canvas for Trigger Amplitude of single channels.  |
| TH1F * | **[_hTrigAmp](/Classes/classLivePlots.md#variable--htrigamp)** <br>Histograms for Trigger Amplitude of single channels.  |
| TCanvas * | **[_cPileUp](/Classes/classLivePlots.md#variable--cpileup)** <br>Canvas for Pile-Up monitoring.  |
| TGraph * | **[_gPileUp](/Classes/classLivePlots.md#variable--gpileup)** <br>Graph for Pile-Up monitoring.  |
| std::vector< Float_t > | **[_yPileUp](/Classes/classLivePlots.md#variable--ypileup)** <br>y-values of Pile-Up plot  |
| std::vector< Int_t > | **[_xPileUp](/Classes/classLivePlots.md#variable--xpileup)** <br>x-values of Pile-Up plot  |
| TCanvas * | **[_cHitmapMB](/Classes/classLivePlots.md#variable--chitmapmb)** <br>Canvas for TW hitmap w/ MB trigger.  |
| TCanvas * | **[_cHitmapFrag](/Classes/classLivePlots.md#variable--chitmapfrag)** <br>Canvas for TW hitmap w/ fragmentation trigger.  |
| TH2F * | **[_hHitmapMB](/Classes/classLivePlots.md#variable--hhitmapmb)** <br>Histogram for TW hitmap w/ MB trigger.  |
| TH2F * | **[_hHitmapFrag](/Classes/classLivePlots.md#variable--hhitmapfrag)** <br>Histogram for TW hitmap w/ fragmentation trigger.  |

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


## Protected Attributes Documentation

### variable _OutDir

```cpp
TSystemDirectory * _OutDir;
```

Output directory of the reconstruction executable. 

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


### variable _hFragCharge

```cpp
std::map< Int_t, TH1F * > _hFragCharge;
```

Histograms of Fragmentation Trigger charge spectra. 

### variable _cTrigAmp

```cpp
TCanvas * _cTrigAmp;
```

Canvas for Trigger Amplitude of single channels. 

### variable _hTrigAmp

```cpp
TH1F * _hTrigAmp;
```

Histograms for Trigger Amplitude of single channels. 

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

-------------------------------

Updated on 2022-07-12 at 15:22:20 +0000