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


-------------------------------

Updated on 2024-02-14 at 13:20:17 +0000