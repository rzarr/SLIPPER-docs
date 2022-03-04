---
title: CALOWaveFormContainer
summary: Class that handles all the processing of raw WaveDAQ waveforms for the Calorimeter. 

---

# CALOWaveFormContainer



Class that handles all the processing of raw WaveDAQ waveforms for the Calorimeter. 

Inherits from [WaveFormContainer](/Classes/classWaveFormContainer.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CALOWaveFormContainer](/Classes/classCALOWaveFormContainer.md#function-calowaveformcontainer)**()<br>Default constructor.  |
| virtual Float_t | **[GetChargeCALO](/Classes/classCALOWaveFormContainer.md#function-getchargecalo)**(Int_t channel, Int_t start_bin =[CHARGESTARTBIN](/Files/Parameters_8h.md#define-chargestartbin), Int_t stop_bin =[CHARGESTOPBIN](/Files/Parameters_8h.md#define-chargestopbin))<br>Find the integral charge of a Calorimeter waveform.  |
| virtual Bool_t | **[IsEmpty](/Classes/classCALOWaveFormContainer.md#function-isempty)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual Bool_t | **[IsEmptyTest](/Classes/classCALOWaveFormContainer.md#function-isemptytest)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual void | **[CopyWaveform](/Classes/classCALOWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual void | **[ClearData](/Classes/classCALOWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classCALOWaveFormContainer.md#function-getpedestal)**(Int_t channel)<br>Find pedestal of the waveform.  |
| virtual Float_t | **[GetAmplitude](/Classes/classCALOWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual Float_t | **[GetCharge](/Classes/classCALOWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =[CHARGESTARTBIN](/Files/Parameters_8h.md#define-chargestartbin), Int_t stop_bin =[CHARGESTOPBIN](/Files/Parameters_8h.md#define-chargestopbin))<br>Find the integral charge of the waveform.  |
| virtual Float_t | **[GetRiseTime](/Classes/classCALOWaveFormContainer.md#function-getrisetime)**(Int_t channel)<br>Calucalte the 10% - 90% rise time of the waveform.  |
| virtual Float_t | **[GetTimeCFD](/Classes/classCALOWaveFormContainer.md#function-gettimecfd)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with the CFD method.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classCALOWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[RescaleTime](/Classes/classCALOWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[MedianFilter](/Classes/classCALOWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[SaveWF](/Classes/classCALOWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classCALOWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Ped](/Classes/classCALOWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classCALOWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_Amp](/Classes/classCALOWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| Float_t | **[_Charge](/Classes/classCALOWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| Float_t | **[_Time](/Classes/classCALOWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |
| Float_t | **[_RiseTime](/Classes/classCALOWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |

## Additional inherited members

**Public Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**() |


## Public Functions Documentation

### function CALOWaveFormContainer

```cpp
CALOWaveFormContainer()
```

Default constructor. 

### function GetChargeCALO

```cpp
virtual Float_t GetChargeCALO(
    Int_t channel,
    Int_t start_bin =CHARGESTARTBIN,
    Int_t stop_bin =CHARGESTOPBIN
)
```

Find the integral charge of a Calorimeter waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **start_bin** Start bin (optional, default=CHARGESTARTBIN) 
  * **stop_bin** Stop bin (optional, default=CHARGESTOPBIN) 


**Return**: Total charge (integral) of the WF [V*ns] 

The integral is stopped when the WF crosses the baseline 


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

**Reimplemented by**: [SCWaveFormContainer::ClearData](/Classes/classSCWaveFormContainer.md#function-cleardata)


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

Updated on 2022-03-04 at 14:25:58 +0000