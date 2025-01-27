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
| virtual Float_t | **[GetCharge](/Classes/classCALOWaveFormContainer.md#function-getcharge)**(Int_t channel, Int_t start_bin =CHARGESTARTBIN, Int_t stop_bin =CHARGESTOPBIN) override<br>Find the integral charge of a Calorimeter waveform [OVERLOADED].  |
| virtual std::pair< Float_t, Float_t > | **[GetPedestal](/Classes/classCALOWaveFormContainer.md#function-getpedestal)**(Int_t channel) override<br>Find pedestal of a CALO waveform.  |

## Additional inherited members

**Public Functions inherited from [WaveFormContainer](/Classes/classWaveFormContainer.md)**

|                | Name           |
| -------------- | -------------- |
| | **[WaveFormContainer](/Classes/classWaveFormContainer.md#function-waveformcontainer)**()<br>Default constructor.  |
| virtual | **[~WaveFormContainer](/Classes/classWaveFormContainer.md#function-~waveformcontainer)**()<br>Default destructor.  |
| virtual void | **[CheckRangeOverflow](/Classes/classWaveFormContainer.md#function-checkrangeoverflow)**(Float_t * w_ptr)<br>Check if the Waveform read from WDB overflows the WDAQ dynamic range and correct if necessary.  |
| virtual void | **[ClearData](/Classes/classWaveFormContainer.md#function-cleardata)**()<br>Clear data for new cycle.  |
| virtual void | **[CopyWaveform](/Classes/classWaveFormContainer.md#function-copywaveform)**([NeutronWF](/Classes/classNeutronWF.md) * nWF, int channel)<br>Copy a decoded waveform in the output container of neutrons.  |
| virtual Float_t | **[GetAmplitude](/Classes/classWaveFormContainer.md#function-getamplitude)**(Int_t channel)<br>Find the max amplitude of the waveform.  |
| virtual UShort_t | **[GetBoardSerialNumber](/Classes/classWaveFormContainer.md#function-getboardserialnumber)**()<br>Get the serial number of the WDB board.  |
| virtual Float_t | **[GetCLKPhase](/Classes/classWaveFormContainer.md#function-getclkphase)**(Int_t channel, UShort_t board =0, Int_t event =-1, TFile * fOut =nullptr)<br>Get the phase of a CLK signal.  |
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

### function CALOWaveFormContainer

```cpp
CALOWaveFormContainer()
```

Default constructor. 

### function GetCharge

```cpp
virtual Float_t GetCharge(
    Int_t channel,
    Int_t start_bin =CHARGESTARTBIN,
    Int_t stop_bin =CHARGESTOPBIN
) override
```

Find the integral charge of a Calorimeter waveform [OVERLOADED]. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 
  * **start_bin** Start bin (optional, default=CHARGESTARTBIN) 
  * **stop_bin** Stop bin (optional, default=CHARGESTOPBIN) 


**Return**: Total charge (integral) of the WF [V*ns] 

**Reimplements**: [WaveFormContainer::GetCharge](/Classes/classWaveFormContainer.md#function-getcharge)


The integral is stopped when the WF crosses the baseline 


### function GetPedestal

```cpp
virtual std::pair< Float_t, Float_t > GetPedestal(
    Int_t channel
) override
```

Find pedestal of a CALO waveform. 

**Parameters**: 

  * **channel** WaveDREAM channel Id 


**Return**: Pair containing the value of the pedestal and its RMS [V] 

**Reimplements**: [WaveFormContainer::GetPedestal](/Classes/classWaveFormContainer.md#function-getpedestal)


The value is computed as the median of the points from PEDESTALSTARTBIN to PEDESTALSTOPBIN in [Parameters.h] --> For CALO, only the first points are considered 


-------------------------------

Updated on 2025-01-27 at 17:57:12 +0000