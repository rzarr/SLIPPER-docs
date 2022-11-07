---
title: SCWaveFormContainer
summary: Class that handles all the processing of raw WaveDAQ waveforms for the Start Counter detector. 

---

# SCWaveFormContainer



Class that handles all the processing of raw WaveDAQ waveforms for the Start Counter detector. 

Inherits from [WaveFormContainer](/Classes/classWaveFormContainer.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SCWaveFormContainer](/Classes/classSCWaveFormContainer.md#function-scwaveformcontainer)**()<br>Default constructor.  |
| virtual | **[~SCWaveFormContainer](/Classes/classSCWaveFormContainer.md#function-~scwaveformcontainer)**()<br>Default destructor.  |
| virtual void | **[CheckRangeOverflow](/Classes/classSCWaveFormContainer.md#function-checkrangeoverflow)**(Float_t * w_ptr)<br>Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary.  |
| virtual void | **[ClearData](/Classes/classSCWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual void | **[ClearOutputData](/Classes/classSCWaveFormContainer.md#function-clearoutputdata)**()<br>Clear output data for new cycle.  |
| virtual void | **[CopyWaveform](/Classes/classSCWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual Float_t | **[GetAmplitude](/Classes/classSCWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual UShort_t | **[GetBoardSerialNumber](/Classes/classSCWaveFormContainer.md#function-getboardserialnumber)**()<br>Get the serial number of the WDB board.  |
| virtual Float_t | **[GetCharge](/Classes/classSCWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN)<br>Find the integral charge of the waveform.  |
| virtual Float_t | **[GetChargeSC](/Classes/classSCWaveFormContainer.md#function-getchargesc)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN)<br>Find the integral charge of the single channel SC waveform.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classSCWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classSCWaveFormContainer.md#function-getpedestal)**(Int_t channel)<br>Find pedestal of the waveform.  |
| virtual Float_t | **[GetRiseTime](/Classes/classSCWaveFormContainer.md#function-getrisetime)**(Int_t channel)<br>Calucalte the 10% - 90% rise time of the waveform.  |
| virtual Float_t | **[GetSCTotalCharge](/Classes/classSCWaveFormContainer.md#function-getsctotalcharge)**(std::vector< Int_t > * Channels)<br>Compute and get the total raw energy loss in the SC.  |
| virtual Float_t | **[GetTimeCFD](/Classes/classSCWaveFormContainer.md#function-gettimecfd)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="")<br>Calculate the timestamp of the waveform with the CFD method.  |
| virtual Float_t | **[GetTimeSC](/Classes/classSCWaveFormContainer.md#function-gettimesc)**(Bool_t * IsPossiblePileUp, std::vector< Int_t > * Channels, UShort_t BoardId =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="SC")<br>Analyze SC waveforms to extract its timestamp.  |
| virtual Float_t | **[GetTimeSC_Linear](/Classes/classSCWaveFormContainer.md#function-gettimesc-linear)**(std::vector< Int_t > * Channels)<br>Analyze SC waveforms and extract the SC time with a linear extrapolation to the baseline.  |
| virtual Bool_t | **[IsEmpty](/Classes/classSCWaveFormContainer.md#function-isempty)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual Bool_t | **[IsEmptyTest](/Classes/classSCWaveFormContainer.md#function-isemptytest)**(Int_t channel)<br>Check if a WaveDREAM channel is empty.  |
| virtual void | **[SetBoardSerialNumber](/Classes/classSCWaveFormContainer.md#function-setboardserialnumber)**(UShort_t bsn)<br>Set the serial number of the WDB board.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual Bool_t | **[CheckForPileUp](/Classes/classSCWaveFormContainer.md#function-checkforpileup)**(std::vector< Float_t > * w_ptr, std::vector< Float_t > * t_ptr, Int_t event =-1, TFile * fOut =nullptr)<br>Check for PileUp in the Start Counter total signal.  |
| virtual void | **[CheckSignals](/Classes/classSCWaveFormContainer.md#function-checksignals)**(std::vector< Int_t > * Channels)<br>Function that checks if any SC channel has undergone dynamic range bit overflow and corrects it.  |
| virtual void | **[MedianFilter](/Classes/classSCWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[RescaleTime](/Classes/classSCWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[SaveWF](/Classes/classSCWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |
| virtual void | **[SumSCWaveforms](/Classes/classSCWaveFormContainer.md#function-sumscwaveforms)**(std::vector< Int_t > * Channels)<br>Function that performs the sum of the SC waveforms and computes the baseline of the total waveform.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classSCWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Amp](/Classes/classSCWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| UShort_t | **[_BoardSerialNumber](/Classes/classSCWaveFormContainer.md#variable--boardserialnumber)** <br>Serial number of the associated WaveDREAM board.  |
| Float_t | **[_Charge](/Classes/classSCWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| std::vector< Float_t > | **[_DerT](/Classes/classSCWaveFormContainer.md#variable--dert)** <br>Time vector for SC total signal derivative.  |
| std::vector< Float_t > | **[_DerW](/Classes/classSCWaveFormContainer.md#variable--derw)** <br>Amplitude vector for SC total signal derivative.  |
| Float_t | **[_Ped](/Classes/classSCWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classSCWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_RiseTime](/Classes/classSCWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |
| std::vector< Float_t > | **[_SC_Sum_T](/Classes/classSCWaveFormContainer.md#variable--sc-sum-t)** <br>Time vector for SC total signal.  |
| std::vector< Float_t > | **[_SC_Sum_W](/Classes/classSCWaveFormContainer.md#variable--sc-sum-w)** <br>Amplitude vector for SC total signal.  |
| Float_t | **[_SCped](/Classes/classSCWaveFormContainer.md#variable--scped)** <br>Pedestal of the SC total signal.  |
| Float_t | **[_SCpedRMS](/Classes/classSCWaveFormContainer.md#variable--scpedrms)** <br>Pedestal of the SC total signal.  |
| Bool_t | **[_SignalsChecked](/Classes/classSCWaveFormContainer.md#variable--signalschecked)** <br>Boolean flag that signals if SC channels have been checked for dynamic range overflow.  |
| Float_t | **[_Time](/Classes/classSCWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |

## Additional inherited members

**Public Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**() |


## Public Functions Documentation

### function SCWaveFormContainer

```cpp
SCWaveFormContainer()
```

Default constructor. 

### function ~SCWaveFormContainer

```cpp
virtual ~SCWaveFormContainer()
```

Default destructor. 

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

**Reimplements**: [WaveFormContainer::ClearData](/Classes/classWaveFormContainer.md#function-cleardata)


### function ClearOutputData

```cpp
virtual void ClearOutputData()
```

Clear output data for new cycle. 

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


### function GetChargeSC

```cpp
virtual Float_t GetChargeSC(
    Int_t channel,
    Int_t start_bin =CHARGESTARTBIN,
    Int_t stop_bin =CHARGESTOPBIN
)
```

Find the integral charge of the single channel SC waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **start_bin** Start bin (optional, default=CHARGESTARTBIN) 
  * **stop_bin** Stop bin (optional, default=CHARGESTOPBIN) 


**Return**: Total charge (integral) of the WF [V*ns] 

The integral is performed only in the region where the waveform is less than the baseline + 2*PedRMS 


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

### function GetSCTotalCharge

```cpp
virtual Float_t GetSCTotalCharge(
    std::vector< Int_t > * Channels
)
```

Compute and get the total raw energy loss in the SC. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channel 


**Return**: Integral charge of the total SC Waveform 

The energy loss of single SC channels is computed as the integral of the total SC WaveForm, i.e. the sum of all the 8 channels waveforms 


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


### function GetTimeSC

```cpp
virtual Float_t GetTimeSC(
    Bool_t * IsPossiblePileUp,
    std::vector< Int_t > * Channels,
    UShort_t BoardId =0,
    Int_t event =-1,
    TFile * fOut =nullptr,
    TString detector ="SC"
)
```

Analyze SC waveforms to extract its timestamp. 

**Parameters**: 

  * **IsPossiblePileUp** Pointer to boolean variable that flags the event as possible Pile-Up 
  * **Channels** Pointer to vector of SC channel 
  * **BoardId** SC board serial number (optional, default = 0) 
  * **event** Event number (optional, default = -1) 
  * **fOut** Pointer to output file (optional, default = nullptr) 
  * **detector** Name of the detecor (optional, default = "SC"), added for the new SC version inclusion 


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


**Return**: Time calculated for the SC with linear extrapolation [ns] 

This function is the new template one for linear extrapolation to the baseline. CURRENTLY NOT USED 


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

### function CheckForPileUp

```cpp
virtual Bool_t CheckForPileUp(
    std::vector< Float_t > * w_ptr,
    std::vector< Float_t > * t_ptr,
    Int_t event =-1,
    TFile * fOut =nullptr
)
```

Check for PileUp in the Start Counter total signal. 

**Parameters**: 

  * **w_ptr** Pointer to first element of amplitude vector 
  * **t_ptr** Pointer to first element of time vector 
  * **event** Event number (optional, default=-1) 
  * **fOut** Pointer to output file (optional, default=nullptr) 


**Return**: True if there is possible PileUp in the event, false otherwise 

The implemented algorithm is dervied from the n_TOF collaboration and exploits the derivative of the signal. If the derivative crosses a certain threshold exactly 4 times, then there is a single signal. Otherwise, the event is flagged as a possible pile-up. 


### function CheckSignals

```cpp
virtual void CheckSignals(
    std::vector< Int_t > * Channels
)
```

Function that checks if any SC channel has undergone dynamic range bit overflow and corrects it. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channels 


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


### function SumSCWaveforms

```cpp
virtual void SumSCWaveforms(
    std::vector< Int_t > * Channels
)
```

Function that performs the sum of the SC waveforms and computes the baseline of the total waveform. 

**Parameters**: 

  * **Channels** Pointer to vector of SC channels 


Both the amplitude-time values of the total signal and its baseline are stored in private variables of the CWaveformContainer class 


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

### variable _DerT

```cpp
std::vector< Float_t > _DerT;
```

Time vector for SC total signal derivative. 

### variable _DerW

```cpp
std::vector< Float_t > _DerW;
```

Amplitude vector for SC total signal derivative. 

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

### variable _SC_Sum_T

```cpp
std::vector< Float_t > _SC_Sum_T;
```

Time vector for SC total signal. 

### variable _SC_Sum_W

```cpp
std::vector< Float_t > _SC_Sum_W;
```

Amplitude vector for SC total signal. 

### variable _SCped

```cpp
Float_t _SCped;
```

Pedestal of the SC total signal. 

### variable _SCpedRMS

```cpp
Float_t _SCpedRMS;
```

Pedestal of the SC total signal. 

### variable _SignalsChecked

```cpp
Bool_t _SignalsChecked;
```

Boolean flag that signals if SC channels have been checked for dynamic range overflow. 

### variable _Time

```cpp
Float_t _Time;
```

Raw Time of the signals [ns]. 

-------------------------------

Updated on 2022-11-07 at 19:12:57 +0000