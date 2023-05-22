---
title: WaveFormContainer
summary: Class that handles all the processing of raw WaveDAQ waveforms. 

---

# WaveFormContainer



Class that handles all the processing of raw WaveDAQ waveforms.  [More...](#detailed-description)

Inherited by [CALOWaveFormContainer](/Classes/classCALOWaveFormContainer.md), [SCWaveFormContainer](/Classes/classSCWaveFormContainer.md), [TWWaveFormContainer](/Classes/classTWWaveFormContainer.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**() |
| virtual void | **[CheckRangeOverflow](/Classes/classWaveFormContainer.md#function-checkrangeoverflow)**(Float_t * w_ptr)<br>Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary.  |
| virtual void | **[ClearData](/Classes/classWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual void | **[CopyWaveform](/Classes/classWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual Float_t | **[GetAmplitude](/Classes/classWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual UShort_t | **[GetBoardSerialNumber](/Classes/classWaveFormContainer.md#function-getboardserialnumber)**()<br>Get the serial number of the WDB board.  |
| virtual Float_t | **[GetCharge](/Classes/classWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN)<br>Find the integral charge of the waveform.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classWaveFormContainer.md#function-getpedestal)**(Int_t channel)<br>Find pedestal of the waveform.  |
| virtual Float_t | **[GetRiseTime](/Classes/classWaveFormContainer.md#function-getrisetime)**(Int_t channel)<br>Calucalte the 10% - 90% rise time of the waveform.  |
| virtual Float_t | **[GetTimeCFD](/Classes/classWaveFormContainer.md#function-gettimecfd)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with the CFD method.  |
| virtual Bool_t | **[IsEmpty](/Classes/classWaveFormContainer.md#function-isempty)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual Bool_t | **[IsEmptyTest](/Classes/classWaveFormContainer.md#function-isemptytest)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual void | **[SetBoardSerialNumber](/Classes/classWaveFormContainer.md#function-setboardserialnumber)**(UShort_t bsn)<br>Set the serial number of the WDB board.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[MedianFilter](/Classes/classWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[RescaleTime](/Classes/classWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[SaveWF](/Classes/classWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Amp](/Classes/classWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| UShort_t | **[_BoardSerialNumber](/Classes/classWaveFormContainer.md#variable--boardserialnumber)** <br>Serial number of the associated WaveDREAM board.  |
| Float_t | **[_Charge](/Classes/classWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| Float_t | **[_Ped](/Classes/classWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_RiseTime](/Classes/classWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |
| Float_t | **[_Time](/Classes/classWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |

## Detailed Description

```cpp
class WaveFormContainer;
```

Class that handles all the processing of raw WaveDAQ waveforms. 

The class contains the signals acquired by one WaveDREAM board and all the methods used for waveform processing 

## Public Functions Documentation

### function WaveFormContainer

```cpp
WaveFormContainer()
```

Default constructor. 

### function ~WaveFormContainer

```cpp
virtual ~WaveFormContainer()
```


### function CheckRangeOverflow

```cpp
virtual void CheckRangeOverflow(
    Float_t * w_ptr
)
```

Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary. 

**Parameters**: 

  * **w_ptr** Pointer to element 1 (not 0) of the WF amplitude vector 


### function ClearData

```cpp
virtual void ClearData()
```

Clear data for new cycle. 

**Reimplemented by**: [SCWaveFormContainer::ClearData](/Classes/classSCWaveFormContainer.md#function-cleardata)


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

### function GetBoardSerialNumber

```cpp
virtual UShort_t GetBoardSerialNumber()
```

Get the serial number of the WDB board. 

**Return**: Board Serial Number 

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

**Reimplemented by**: [CALOWaveFormContainer::GetCharge](/Classes/classCALOWaveFormContainer.md#function-getcharge)


The boundaries of the integral are useful when performing Pulse Shape Analysis 


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

**Reimplemented by**: [CALOWaveFormContainer::GetPedestal](/Classes/classCALOWaveFormContainer.md#function-getpedestal)


The value is computed as the median of the points from PEDESTALSTARTBIN to PEDESTALSTOPBIN (left-right) in [Parameters.h]


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


### function SetBoardSerialNumber

```cpp
virtual void SetBoardSerialNumber(
    UShort_t bsn
)
```

Set the serial number of the WDB board. 

**Parameters**: 

  * **bsn** BoardSerialNumber 


## Protected Functions Documentation

### function MedianFilter

```cpp
virtual void MedianFilter(
    Int_t channel
)
```

Apply a 7-point median filter to the WF if needed. 

**Parameters**: 

  * **channel** Channel Id 


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

### variable _Amp

```cpp
Float_t _Amp;
```

Amplitude of the signals (<0) [V]. 

### variable _BoardSerialNumber

```cpp
UShort_t _BoardSerialNumber;
```

Serial number of the associated WaveDREAM board. 

### variable _Charge

```cpp
Float_t _Charge;
```

Integral charge of the signals [V*ns]. 

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

### variable _RiseTime

```cpp
Float_t _RiseTime;
```

Rise Time of the signals [ns]. 

### variable _Time

```cpp
Float_t _Time;
```

Raw Time of the signals [ns]. 

-------------------------------

Updated on 2023-05-22 at 10:49:05 +0000