---
title: CWaveFormContainer
summary: Class that handles all the processing of raw WaveDAQ waveforms. 

---

# CWaveFormContainer



Class that handles all the processing of raw WaveDAQ waveforms.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CWaveFormContainer](/Classes/classCWaveFormContainer.md#function-cwaveformcontainer)**()<br>Default constructor.  |
| virtual Bool_t | **[IsEmpty](/Classes/classCWaveFormContainer.md#function-isempty)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual Bool_t | **[IsEmptyTest](/Classes/classCWaveFormContainer.md#function-isemptytest)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual void | **[CopyWaveform](/Classes/classCWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual void | **[ClearData](/Classes/classCWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classCWaveFormContainer.md#function-getpedestal)**(Int_t channel)<br>Find pedestal of the waveform.  |
| virtual Float_t | **[GetAmplitude](/Classes/classCWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual Float_t | **[GetCharge](/Classes/classCWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =[CHARGESTARTBIN](/Files/Parameters_8h.md#define-chargestartbin), Int_t stop_bin =[CHARGESTOPBIN](/Files/Parameters_8h.md#define-chargestopbin))<br>Find the integral charge of the waveform.  |
| virtual Float_t | **[GetRiseTime](/Classes/classCWaveFormContainer.md#function-getrisetime)**(Int_t channel)<br>Calucalte the 10% - 90% rise time of the waveform.  |
| virtual Float_t | **[GetSCTotalCharge](/Classes/classCWaveFormContainer.md#function-getsctotalcharge)**(std::vector< Int_t > * Channels)<br>Compute and get the total raw energy loss in the SC.  |
| virtual Float_t | **[GetTimeSC](/Classes/classCWaveFormContainer.md#function-gettimesc)**(std::vector< Int_t > * Channels, UShort_t BoardId =0, Int_t event =-1, TFile * fOut =nullptr)<br>Analyze SC waveforms to extract its timestamp.  |
| virtual Float_t | **[GetTimeSC_Linear](/Classes/classCWaveFormContainer.md#function-gettimesc-linear)**(std::vector< Int_t > * Channels)<br>Analyze SC waveforms and extract the SC time with a linear extrapolation to the baseline.  |
| virtual Bool_t | **[CheckForPileUp](/Classes/classCWaveFormContainer.md#function-checkforpileup)**(std::vector< Float_t > * w_ptr, std::vector< Float_t > * t_ptr, Int_t event =-1, TFile * fOut =nullptr)<br>Check for PileUp in the Start Counter signal.  |
| virtual Float_t | **[GetTimeCFD](/Classes/classCWaveFormContainer.md#function-gettimecfd)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with the CFD method.  |
| virtual Float_t | **[GetTimeLinear](/Classes/classCWaveFormContainer.md#function-gettimelinear)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with a linear extrapolation.  |
| virtual Float_t | **[GetChargeCALO](/Classes/classCWaveFormContainer.md#function-getchargecalo)**(Int_t channel)<br>Find the integral charge of a Calorimeter waveform.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classCWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[RescaleTime](/Classes/classCWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[MedianFilter](/Classes/classCWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[SumSCWavefoms](/Classes/classCWaveFormContainer.md#function-sumscwavefoms)**(std::vector< Int_t > * Channels, std::vector< Float_t > * SC_Sum_W, std::vector< Float_t > * SC_Sum_T)<br>Function that performs the sum of the SC waveforms.  |
| virtual void | **[SaveWF](/Classes/classCWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classCWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Ped](/Classes/classCWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classCWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_Amp](/Classes/classCWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| Float_t | **[_Charge](/Classes/classCWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| Float_t | **[_Time](/Classes/classCWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |
| Float_t | **[_RiseTime](/Classes/classCWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |

## Detailed Description

```cpp
class CWaveFormContainer;
```

Class that handles all the processing of raw WaveDAQ waveforms. 

The class contains the signals acquired by one WaveDREAM board and all the methods used for waveform processing 

## Public Functions Documentation

### function CWaveFormContainer

```cpp
CWaveFormContainer()
```

Default constructor. 

### function IsEmpty

```cpp
virtual Bool_t IsEmpty(
    Int_t channel
)
```

Check if a WaveDREAM channel is empty. 

**Parameters**: 

  * **channel** Channel Id 


**Return**: True if the channel is empty, False otherwise 

Find min and max of WF and see if there is actually a signal The function also corrects range overflow errors for TW signals 


### function IsEmptyTest

```cpp
virtual Bool_t IsEmptyTest(
    Int_t channel
)
```

Check if a WaveDREAM channel is empty. 

**Parameters**: 

  * **channel** Channel Id 


**Return**: True if the channel is empty, false otherwise 

AUX function 


### function CopyWaveform

```cpp
virtual void CopyWaveform(
    NeutronWF * nWF,
    int channel
)
```

Copy a decoded waveform in the output container of neutrons. 

**Parameters**: 

  * **nWF** Pointer to output neutron waveform container 
  * **channel** WaveDREAM channel to be copied 


### function ClearData

```cpp
virtual void ClearData()
```

Clear data for new cycle. 

### function GetPedestal

```cpp
virtual std::pair< Float_t, Float_t > GetPedestal(
    Int_t channel
)
```

Find pedestal of the waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 


**Return**: Pair containing the value of the pedestal and its RMS [V] 

The value is computed as the median of the points from PEDESTALSTARTBIN to PEDESTALSTOPBIN in [Parameters.h](/Files/Parameters_8h.md#file-parameters.h)


### function GetAmplitude

```cpp
virtual Float_t GetAmplitude(
    Int_t channel
)
```

Find the max amplitude of the waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 


**Return**: Amplitude of the WF (<0) [V] 

### function GetCharge

```cpp
virtual Float_t GetCharge(
    Int_t channel,
    Int_t start_bin =CHARGESTARTBIN,
    Int_t stop_bin =CHARGESTOPBIN
)
```

Find the integral charge of the waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **start_bin** Start bin (optional, default=CHARGESTARTBIN) 
  * **stop_bin** Stop bin (optional, default=CHARGESTOPBIN) 


**Return**: Total charge (integral) of the WF [V*ns] 

The boundaries of the integral are useful when performing Pulse Shape Analysis 


### function GetRiseTime

```cpp
virtual Float_t GetRiseTime(
    Int_t channel
)
```

Calucalte the 10% - 90% rise time of the waveform. 

**Parameters**: 

  * **channel** Channel Id 


**Return**: Rise time of the signal [ns] 

### function GetSCTotalCharge

```cpp
virtual Float_t GetSCTotalCharge(
    std::vector< Int_t > * Channels
)
```

Compute and get the total raw energy loss in the SC. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channel 


**Return**: SC total raw energy loss 

The energy loss of single SC channels is computed as the integral of the WaveForms and then all the values are added together 


### function GetTimeSC

```cpp
virtual Float_t GetTimeSC(
    std::vector< Int_t > * Channels,
    UShort_t BoardId =0,
    Int_t event =-1,
    TFile * fOut =nullptr
)
```

Analyze SC waveforms to extract its timestamp. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channel 
  * **BoardId** SC board serial number (optional, default = 0) 
  * **event** Event number (optional, default = -1) 
  * **fOut** Pointer to output file (optional, default = nullptr) 


**Return**: Time calculated for the SC [ns] 

This method saves WFs to output if the optional paramaters are set 


### function GetTimeSC_Linear

```cpp
virtual Float_t GetTimeSC_Linear(
    std::vector< Int_t > * Channels
)
```

Analyze SC waveforms and extract the SC time with a linear extrapolation to the baseline. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channels 


**Return**: Time calculated for the SC [ns] 

This function is the new template one for linear extrapolation to the baseline. CURRENTLY NOT USED 


### function CheckForPileUp

```cpp
virtual Bool_t CheckForPileUp(
    std::vector< Float_t > * w_ptr,
    std::vector< Float_t > * t_ptr,
    Int_t event =-1,
    TFile * fOut =nullptr
)
```

Check for PileUp in the Start Counter signal. 

**Return**: True if there is PileUp in the event, false otherwise 

### function GetTimeCFD

```cpp
virtual Float_t GetTimeCFD(
    Int_t channel,
    UShort_t board =0,
    Int_t event =-1,
    TFile * fOut =nullptr,
    TString detector =""
)
```

Calculate the timestamp of the waveform with the CFD method. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **board** Board serial number (optional, default = 0) 
  * **event** Event number (optional, default = -1) 
  * **fOut** Pointer to output file (optional, default = nullptr) 
  * **detector** Name of the analyzed detector (optional, default = "") 


**Return**: Time calculated with the CFD method [ns] 

The default CFD threshold is set in [Parameters.h](/Files/Parameters_8h.md#file-parameters.h). If the optional parameters are used, the function also saves the WF 


### function GetTimeLinear

```cpp
virtual Float_t GetTimeLinear(
    Int_t channel,
    UShort_t board =0,
    Int_t event =-1,
    TFile * fOut =nullptr,
    TString detector =""
)
```

Calculate the timestamp of the waveform with a linear extrapolation. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **board** Board serial number (optional, default = 0) 
  * **event** Event number (optional, default = -1) 
  * **fOut** Pointer to output file (optional, default = nullptr) 
  * **detector** Name of the analyzed detector (optional, default = "") 


**Return**: Time calculated with a linear extrapolation to the baseline [ns] 

The slope is calculated at CFD threshold and the time is found at the crossing with the pedestal. If the optional parameters are used, the function also saves the WF 


### function GetChargeCALO

```cpp
virtual Float_t GetChargeCALO(
    Int_t channel
)
```

Find the integral charge of a Calorimeter waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 


**Return**: Total charge (integral) of the WF [V*ns] 

The integral is stopped when the WF crosses the baseline 


### function GetCLKPhase

```cpp
virtual Float_t GetCLKPhase(
    Int_t channel,
    UShort_t board =0,
    Int_t event =-1,
    TFile * fOut =nullptr
)
```

Get the phase of a CLK signal. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **board** Board serial number 
  * **event** Event number 
  * **fOut** Pointer to output file 


**Return**: Phase of the CLK signal [ns] 

This function analyzes the clock waveform and returns its phase.

* Each rising edge of the waveform is analyzed -> the zero-crossing points are found using linear interpolation
* These timestamps are then plotted versus the number of clock cycles elapsed
* This graph is linearly fitted -> the clock phase is the intercept of the fit


## Protected Functions Documentation

### function RescaleTime

```cpp
virtual void RescaleTime(
    std::vector< Float_t > * tmp_time
)
```

Rescale channel time from s to ns. 

**Parameters**: 

  * **t** Pointer to vector of time values 


Function called only by SaveWF at the moment 


### function MedianFilter

```cpp
virtual void MedianFilter(
    Int_t channel
)
```

Apply a 7-point median filter to the WF if needed. 

**Parameters**: 

  * **channel** Channel Id 


### function SumSCWavefoms

```cpp
virtual void SumSCWavefoms(
    std::vector< Int_t > * Channels,
    std::vector< Float_t > * SC_Sum_W,
    std::vector< Float_t > * SC_Sum_T
)
```

Function that performs the sum of the SC waveforms. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channels 
  * **SC_Sum_W** Pointer to vector for the Width values of the summed WF [V] 
  * **SC_Sum_T** Pointer to vector for the Time values of the summed WF [s] 


### function SaveWF

```cpp
virtual void SaveWF(
    Int_t board,
    Int_t channel,
    Int_t event,
    TFile * fOut,
    TString detector,
    TString tag =""
)
```

Save the waveform to a folder in the output file. 

**Parameters**: 

  * **board** Board serial number 
  * **channel** Channel Id 
  * **event** Event number 
  * **fOut** Pointer to output file 
  * **detector** Detector name 
  * **tag** Additional tags (optional) 


## Public Attributes Documentation

### variable data

```cpp
WDBDATA data;
```

Object containing the raw Waveforms of a single WaveDREAM board. 

## Protected Attributes Documentation

### variable _Ped

```cpp
Float_t _Ped;
```

Pedestal of the WFs [V]. 

### variable _PedRMS

```cpp
Float_t _PedRMS;
```

Pedestal Root Mean Square [V]. 

### variable _Amp

```cpp
Float_t _Amp;
```

Amplitude of the signals (<0) [V]. 

### variable _Charge

```cpp
Float_t _Charge;
```

Integral charge of the signals [V*ns]. 

### variable _Time

```cpp
Float_t _Time;
```

Raw Time of the signals [ns]. 

### variable _RiseTime

```cpp
Float_t _RiseTime;
```

Rise Time of the signals [ns]. 

-------------------------------

Updated on 2022-02-10 at 11:12:25 +0000