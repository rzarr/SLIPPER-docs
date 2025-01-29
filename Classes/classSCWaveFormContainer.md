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
| virtual void | **[ClearData](/Classes/classSCWaveFormContainer.md#function-cleardata)**() override<br>Clear data for new cycle.  |
| virtual void | **[ClearOutputData](/Classes/classSCWaveFormContainer.md#function-clearoutputdata)**()<br>Clear output data for new cycle.  |
| virtual Float_t | **[GetChargeSC](/Classes/classSCWaveFormContainer.md#function-getchargesc)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN)<br>Find the integral charge of the single channel SC waveform.  |
| virtual Float_t | **[GetSCTotalCharge](/Classes/classSCWaveFormContainer.md#function-getsctotalcharge)**(std::vector< Int_t > * Channels)<br>Compute and get the total raw energy loss in the SC.  |
| virtual Float_t | **[GetTimeSC](/Classes/classSCWaveFormContainer.md#function-gettimesc)**(Bool_t * IsPossiblePileUp, std::vector< Int_t > * Channels, UShort_t BoardId =0, Int_t event =-1, TFile * fOut =nullptr, TString detector ="SC")<br>Analyze SC waveforms to extract its timestamp.  |
| virtual Float_t | **[GetTimeSC_Linear](/Classes/classSCWaveFormContainer.md#function-gettimesc-linear)**(std::vector< Int_t > * Channels)<br>Analyze SC waveforms and extract the SC time with a linear extrapolation to the baseline.  |
| virtual void | **[SumSCWaveforms](/Classes/classSCWaveFormContainer.md#function-sumscwaveforms)**(std::vector< Int_t > * Channels)<br>Function that performs the sum of the SC waveforms and computes the baseline of the total waveform.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual Bool_t | **[CheckForPileUp](/Classes/classSCWaveFormContainer.md#function-checkforpileup)**(std::vector< Float_t > * w_ptr, std::vector< Float_t > * t_ptr, Int_t event =-1, TFile * fOut =nullptr, TString detector ="SC")<br>Check for PileUp in the Start Counter total signal.  |
| virtual void | **[CheckSignals](/Classes/classSCWaveFormContainer.md#function-checksignals)**(std::vector< Int_t > * Channels)<br>Function that checks if any SC channel has undergone dynamic range bit overflow and corrects it.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::vector< Float_t > | **[_SC_Sum_T](/Classes/classSCWaveFormContainer.md#variable--sc-sum-t)** <br>Time vector for SC total signal.  |
| std::vector< Float_t > | **[_SC_Sum_W](/Classes/classSCWaveFormContainer.md#variable--sc-sum-w)** <br>Amplitude vector for SC total signal.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::vector< Float_t > | **[_DerT](/Classes/classSCWaveFormContainer.md#variable--dert)** <br>Time vector for SC total signal derivative.  |
| std::vector< Float_t > | **[_DerW](/Classes/classSCWaveFormContainer.md#variable--derw)** <br>Amplitude vector for SC total signal derivative.  |
| Float_t | **[_SCped](/Classes/classSCWaveFormContainer.md#variable--scped)** <br>Pedestal of the SC total signal.  |
| Float_t | **[_SCpedRMS](/Classes/classSCWaveFormContainer.md#variable--scpedrms)** <br>Pedestal of the SC total signal.  |
| Bool_t | **[_SignalsChecked](/Classes/classSCWaveFormContainer.md#variable--signalschecked)** <br>Boolean flag that signals if SC channels have been checked for dynamic range overflow.  |

## Additional inherited members

**Public Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**()<br>Default destructor.  |
| virtual void | **[CheckRangeOverflow](/Classes/classWaveFormContainer.md#function-checkrangeoverflow)**(Float_t * w_ptr)<br>Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary.  |
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

**Protected Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| virtual void | **[MedianFilter](/Classes/classWaveFormContainer.md#function-medianfilter)**(Int_t channel)<br>Apply a 7-point median filter to the WF if needed.  |
| virtual void | **[RescaleTime](/Classes/classWaveFormContainer.md#function-rescaletime)**(std::vector< Float_t > * tmp_time)<br>Rescale channel time from s to ns.  |
| virtual void | **[SaveWF](/Classes/classWaveFormContainer.md#function-savewf)**(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag ="")<br>Save the waveform to a folder in the output file.  |

**Public Attributes inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| [WDBDATA](/Classes/classWDBDATA.md) | **[data](/Classes/classWaveFormContainer.md#variable-data)** <br>Object containing the raw Waveforms of a single WaveDREAM board.  |

**Protected Attributes inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| Float_t | **[_Amp](/Classes/classWaveFormContainer.md#variable--amp)** <br>Amplitude of the signals (<0) [V].  |
| UShort_t | **[_BoardSerialNumber](/Classes/classWaveFormContainer.md#variable--boardserialnumber)** <br>Serial number of the associated WaveDREAM board.  |
| Float_t | **[_Charge](/Classes/classWaveFormContainer.md#variable--charge)** <br>Integral charge of the signals [V*ns].  |
| Float_t | **[_Ped](/Classes/classWaveFormContainer.md#variable--ped)** <br>Pedestal of the WFs [V].  |
| Float_t | **[_PedRMS](/Classes/classWaveFormContainer.md#variable--pedrms)** <br>Pedestal Root Mean Square [V].  |
| Float_t | **[_RiseTime](/Classes/classWaveFormContainer.md#variable--risetime)** <br>Rise Time of the signals [ns].  |
| Float_t | **[_Time](/Classes/classWaveFormContainer.md#variable--time)** <br>Raw Time of the signals [ns].  |


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

### function ClearData

```cpp
virtual void ClearData() override
```

Clear data for new cycle. 

**Reimplements**: [WaveFormContainer::ClearData](/Classes/classWaveFormContainer.md#function-cleardata)


### function ClearOutputData

```cpp
virtual void ClearOutputData()
```

Clear output data for new cycle. 

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


## Protected Functions Documentation

### function CheckForPileUp

```cpp
virtual Bool_t CheckForPileUp(
    std::vector< Float_t > * w_ptr,
    std::vector< Float_t > * t_ptr,
    Int_t event =-1,
    TFile * fOut =nullptr,
    TString detector ="SC"
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


## Public Attributes Documentation

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

## Protected Attributes Documentation

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

-------------------------------

Updated on 2025-01-29 at 16:16:32 +0000