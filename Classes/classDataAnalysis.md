---
title: DataAnalysis
summary: Main class used by the Analysis executable. 

---

# DataAnalysis



Main class used by the Analysis executable.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[DataAnalysis](/Classes/classDataAnalysis.md#function-dataanalysis)**()<br>Default constructor.  |
| void | **[DoAll](/Classes/classDataAnalysis.md#function-doall)**(TString InputFileName, TString OutputFileName)<br>Perform the whole analysis.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AnalyzeDeltaT](/Classes/classDataAnalysis.md#function-analyzedeltat)**()<br>Analyze the time difference histograms.  |
| bool | **[CheckTriggeredBars](/Classes/classDataAnalysis.md#function-checktriggeredbars)**()<br>Check the number of trigerred bars in the event.  |
| void | **[FillHistograms](/Classes/classDataAnalysis.md#function-fillhistograms)**()<br>Fill the histograms.  |
| TF1 * | **[FitGauss](/Classes/classDataAnalysis.md#function-fitgauss)**(TH1F * hist)<br>Fit an histogram with a Gaussian Function.  |
| void | **[InitHistos](/Classes/classDataAnalysis.md#function-inithistos)**()<br>Initialize all histograms.  |
| void | **[SetOutputStructures](/Classes/classDataAnalysis.md#function-setoutputstructures)**(TTree * t)<br>Set the branches of the output treee.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Ampl_A](/Classes/classDataAnalysis.md#variable--ampl-a)** <br>TW bar amplitude of channel A.  |
| Float_t | **[_Ampl_B](/Classes/classDataAnalysis.md#variable--ampl-b)** <br>TW bar amplitude of channel B.  |
| Float_t | **[_Charge](/Classes/classDataAnalysis.md#variable--charge)** <br>TW bar total charge.  |
| Float_t | **[_Charge_A](/Classes/classDataAnalysis.md#variable--charge-a)** <br>TW bar charge of channel A.  |
| Float_t | **[_Charge_B](/Classes/classDataAnalysis.md#variable--charge-b)** <br>TW bar charge of channel B.  |
| Float_t | **[_DeltaT_AB](/Classes/classDataAnalysis.md#variable--deltat-ab)** <br>TW bar time difference between channels A and B.  |
| TGraphErrors * | **[_DeltaT_AB_Bar](/Classes/classDataAnalysis.md#variable--deltat-ab-bar)** <br>Graph of Time difference vs Postion for each TW Bar.  |
| TH1F * | **[_hist_Ampl_A_Front](/Classes/classDataAnalysis.md#variable--hist-ampl-a-front)** <br>Histograms of the channel A amplitude in a position of Front TW Layer.  |
| TH1F * | **[_hist_Ampl_A_Rear](/Classes/classDataAnalysis.md#variable--hist-ampl-a-rear)** <br>Histograms of the channel A amplitude in a position of Rear TW Layer.  |
| TH1F * | **[_hist_Ampl_B_Front](/Classes/classDataAnalysis.md#variable--hist-ampl-b-front)** <br>Histograms of the channel B amplitude in a position of Front TW Layer.  |
| TH1F * | **[_hist_Ampl_B_Rear](/Classes/classDataAnalysis.md#variable--hist-ampl-b-rear)** <br>Histograms of the channel B amplitude in a position of Rear TW Layer.  |
| TH1F * | **[_hist_Charge_Front](/Classes/classDataAnalysis.md#variable--hist-charge-front)** <br>Histograms of total charge in a position of the Front TW layer.  |
| TH1F * | **[_hist_Charge_Rear](/Classes/classDataAnalysis.md#variable--hist-charge-rear)** <br>Histograms of total charge in a position of the Rear TW layer.  |
| TH1F * | **[_hist_DeltaT_AB_Front](/Classes/classDataAnalysis.md#variable--hist-deltat-ab-front)** <br>Histograms of A-B time difference in a position of Front TW Layer.  |
| TH1F * | **[_hist_DeltaT_AB_Rear](/Classes/classDataAnalysis.md#variable--hist-deltat-ab-rear)** <br>Histograms of A-B time difference in a position of Rear TW Layer.  |
| TH1F * | **[_hitmap_Channels_A](/Classes/classDataAnalysis.md#variable--hitmap-channels-a)** <br>1D channel A hitmap  |
| TH1F * | **[_hitmap_Channels_B](/Classes/classDataAnalysis.md#variable--hitmap-channels-b)** <br>1D channel B hitmap  |
| TH2F * | **[_hitmap_DeltaT_Front](/Classes/classDataAnalysis.md#variable--hitmap-deltat-front)** <br>Histogram for dT resolution in a position of the Front TW Layer.  |
| TH2F * | **[_hitmap_DeltaT_Rear](/Classes/classDataAnalysis.md#variable--hitmap-deltat-rear)** <br>Histogram for dT resolution in a position of the Rear TW Layer.  |
| Int_t | **[_NumberOfGhosts](/Classes/classDataAnalysis.md#variable--numberofghosts)** <br>Number of ghost hits found in an event.  |
| TFile * | **[fOut](/Classes/classDataAnalysis.md#variable-fout)** <br>Output file pointer.  |
| Int_t | **[FrontBar](/Classes/classDataAnalysis.md#variable-frontbar)** <br>TW Front Bar.  |
| Int_t | **[RearBar](/Classes/classDataAnalysis.md#variable-rearbar)** <br>TW Rear Bar.  |

## Detailed Description

```cpp
class DataAnalysis;
```

Main class used by the Analysis executable. 

Currently this class contains some simple functions for plotting 

## Public Functions Documentation

### function DataAnalysis

```cpp
DataAnalysis()
```

Default constructor. 

### function DoAll

```cpp
void DoAll(
    TString InputFileName,
    TString OutputFileName
)
```

Perform the whole analysis. 

**Parameters**: 

  * **InputFileName** Name of the input file 
  * **OutputFileName** Name of the output file 


## Protected Functions Documentation

### function AnalyzeDeltaT

```cpp
void AnalyzeDeltaT()
```

Analyze the time difference histograms. 

Extract the resolution on time difference distributions and plot the deltaT vs Pos of each TW bar 


### function CheckTriggeredBars

```cpp
bool CheckTriggeredBars()
```

Check the number of trigerred bars in the event. 

**Return**: true if only two bars where fired, false otherwise 

### function FillHistograms

```cpp
void FillHistograms()
```

Fill the histograms. 

### function FitGauss

```cpp
TF1 * FitGauss(
    TH1F * hist
)
```

Fit an histogram with a Gaussian Function. 

**Parameters**: 

  * **hist** Pointer to the histogram 


**Return**: Pointer to the fitted Gaussian function 

### function InitHistos

```cpp
void InitHistos()
```

Initialize all histograms. 

### function SetOutputStructures

```cpp
void SetOutputStructures(
    TTree * t
)
```

Set the branches of the output treee. 

**Parameters**: 

  * **t** Pointer to the output tree 


## Protected Attributes Documentation

### variable _Ampl_A

```cpp
Float_t _Ampl_A;
```

TW bar amplitude of channel A. 

### variable _Ampl_B

```cpp
Float_t _Ampl_B;
```

TW bar amplitude of channel B. 

### variable _Charge

```cpp
Float_t _Charge;
```

TW bar total charge. 

### variable _Charge_A

```cpp
Float_t _Charge_A;
```

TW bar charge of channel A. 

### variable _Charge_B

```cpp
Float_t _Charge_B;
```

TW bar charge of channel B. 

### variable _DeltaT_AB

```cpp
Float_t _DeltaT_AB;
```

TW bar time difference between channels A and B. 

### variable _DeltaT_AB_Bar

```cpp
TGraphErrors * _DeltaT_AB_Bar;
```

Graph of Time difference vs Postion for each TW Bar. 

### variable _hist_Ampl_A_Front

```cpp
TH1F * _hist_Ampl_A_Front;
```

Histograms of the channel A amplitude in a position of Front TW Layer. 

### variable _hist_Ampl_A_Rear

```cpp
TH1F * _hist_Ampl_A_Rear;
```

Histograms of the channel A amplitude in a position of Rear TW Layer. 

### variable _hist_Ampl_B_Front

```cpp
TH1F * _hist_Ampl_B_Front;
```

Histograms of the channel B amplitude in a position of Front TW Layer. 

### variable _hist_Ampl_B_Rear

```cpp
TH1F * _hist_Ampl_B_Rear;
```

Histograms of the channel B amplitude in a position of Rear TW Layer. 

### variable _hist_Charge_Front

```cpp
TH1F * _hist_Charge_Front;
```

Histograms of total charge in a position of the Front TW layer. 

### variable _hist_Charge_Rear

```cpp
TH1F * _hist_Charge_Rear;
```

Histograms of total charge in a position of the Rear TW layer. 

### variable _hist_DeltaT_AB_Front

```cpp
TH1F * _hist_DeltaT_AB_Front;
```

Histograms of A-B time difference in a position of Front TW Layer. 

### variable _hist_DeltaT_AB_Rear

```cpp
TH1F * _hist_DeltaT_AB_Rear;
```

Histograms of A-B time difference in a position of Rear TW Layer. 

### variable _hitmap_Channels_A

```cpp
TH1F * _hitmap_Channels_A;
```

1D channel A hitmap 

### variable _hitmap_Channels_B

```cpp
TH1F * _hitmap_Channels_B;
```

1D channel B hitmap 

### variable _hitmap_DeltaT_Front

```cpp
TH2F * _hitmap_DeltaT_Front;
```

Histogram for dT resolution in a position of the Front TW Layer. 

### variable _hitmap_DeltaT_Rear

```cpp
TH2F * _hitmap_DeltaT_Rear;
```

Histogram for dT resolution in a position of the Rear TW Layer. 

### variable _NumberOfGhosts

```cpp
Int_t _NumberOfGhosts;
```

Number of ghost hits found in an event. 

### variable fOut

```cpp
TFile * fOut;
```

Output file pointer. 

### variable FrontBar

```cpp
Int_t FrontBar;
```

TW Front Bar. 

### variable RearBar

```cpp
Int_t RearBar;
```

TW Rear Bar. 

-------------------------------

Updated on 2025-02-26 at 13:36:50 +0000