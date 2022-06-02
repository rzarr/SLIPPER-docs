---
title: TWWaveFormContainer
summary: Class that handles all the processing of raw WaveDAQ waveforms for the TOF-Wall detector. 

---

# TWWaveFormContainer



Class that handles all the processing of raw WaveDAQ waveforms for the TOF-Wall detector. 

Inherits from [WaveFormContainer](/Classes/classWaveFormContainer.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TWWaveFormContainer](/Classes/classTWWaveFormContainer.md#function-twwaveformcontainer)**()<br>Default constructor.  |
| virtual Float_t | **[GetTimeLinear](/Classes/classTWWaveFormContainer.md#function-gettimelinear)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with a linear extrapolation.  |
| virtual Bool_t | **[IsEmpty](/Classes/classTWWaveFormContainer.md#function-isempty)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual Bool_t | **[IsEmptyTest](/Classes/classTWWaveFormContainer.md#function-isemptytest)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual void | **[CopyWaveform](/Classes/classTWWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual void | **[SetBoardSerialNumber](/Classes/classTWWaveFormContainer.md#function-setboardserialnumber)**(UShort_t bsn)<br>Set the serial number of the WDB board.  |
| virtual UShort_t | **[GetBoardSerialNumber](/Classes/classTWWaveFormContainer.md#function-getboardserialnumber)**()<br>Get the serial number of the WDB board.  |
| virtual void | **[ClearData](/Classes/classTWWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classTWWaveFormContainer.md#function-getpedestal)**(Int_t channel)<br>Find pedestal of the waveform.  |
| virtual Float_t | **[GetAmplitude](/Classes/classTWWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual Float_t | **[GetCharge](/Classes/classTWWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN)<br>Find the integral charge of the waveform.  |
| virtual Float_t | **[GetRiseTime](/Classes/classTWWaveFormContainer.md#function-getrisetime)**(Int_t channel)<br>Calucalte the 10% - 90% rise time of the waveform.  |
| virtual Float_t | **[GetTimeCFD](/Classes/classTWWaveFormContainer.md#function-gettimecfd)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with the CFD method.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classTWWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[RescaleTime](/Classes/classTWWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[MedianFilter](/Classes/classTWWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[SaveWF](/Classes/classTWWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classTWWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Ped](/Classes/classTWWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classTWWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_Amp](/Classes/classTWWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| Float_t | **[_Charge](/Classes/classTWWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| Float_t | **[_Time](/Classes/classTWWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |
| Float_t | **[_RiseTime](/Classes/classTWWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |
| UShort_t | **[_BoardSerialNumber](/Classes/classTWWaveFormContainer.md#variable--boardserialnumber)**  |

## Additional inherited members

**Public Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**() |


## Public Functions Documentation

### function TWWaveFormContainer

```cpp
TWWaveFormContainer()
```

Default constructor. 

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


### function SetBoardSerialNumber

```cpp
virtual void SetBoardSerialNumber(
    UShort_t bsn
)
```

Set the serial number of the WDB board. 

**Parameters**: 

  * **bsn** BoardSerialNumber 


### function GetBoardSerialNumber

```cpp
virtual UShort_t GetBoardSerialNumber()
```

Get the serial number of the WDB board. 

**Return**: Board Serial Number 

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

The value is computed as the median of the points from PEDESTALSTARTBIN to PEDESTALSTOPBIN in [Parameters.h]


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

The default CFD threshold is set in [Parameters.h]. If the optional parameters are used, the function also saves the WF 


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

### variable _BoardSerialNumber

```cpp
UShort_t _BoardSerialNumber;
```


-------------------------------

Updated on 2022-06-02 at 14:53:40 +0200