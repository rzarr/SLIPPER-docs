---
title: WDBDATA
summary: Class for WaveDREAM board data container. 

---

# WDBDATA



Class for WaveDREAM board data container.  [More...](#detailed-description)


`#include <CUtils.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[clear](/Classes/classWDBDATA.md#function-clear)**()<br>Clear all the data of a WaveDREAM.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| Float_t | **[w](/Classes/classWDBDATA.md#variable-w)** <br>Amplitude values of the waveforms for each channel of the board.  |
| Float_t | **[t](/Classes/classWDBDATA.md#variable-t)** <br>Time values of the waveforms for each channel of the board.  |
| Bool_t | **[ch_on](/Classes/classWDBDATA.md#variable-ch-on)** <br>Boolean flag that signals if a channel has exceeded the zero-suppression threshold.  |
| UShort_t | **[trigcell](/Classes/classWDBDATA.md#variable-trigcell)** <br>Trigger Cell of the channel.  |
| UShort_t | **[adc_waveform](/Classes/classWDBDATA.md#variable-adc-waveform)** <br>ADC waveform.  |
| UChar_t | **[tdc_waveform](/Classes/classWDBDATA.md#variable-tdc-waveform)** <br>TDC waveform.  |
| ULong_t | **[trigger_data](/Classes/classWDBDATA.md#variable-trigger-data)** <br>Data on the trigger of the event.  |
| Float_t | **[scaler](/Classes/classWDBDATA.md#variable-scaler)** <br>Waveform scaler.  |

## Detailed Description

```cpp
class WDBDATA;
```

Class for WaveDREAM board data container. 

The class contains all the information that can be extracted from the decoding of WaveDREAM board events 

## Public Functions Documentation

### function clear

```cpp
inline void clear()
```

Clear all the data of a WaveDREAM. 

## Public Attributes Documentation

### variable w

```cpp
Float_t w;
```

Amplitude values of the waveforms for each channel of the board. 

### variable t

```cpp
Float_t t;
```

Time values of the waveforms for each channel of the board. 

### variable ch_on

```cpp
Bool_t ch_on;
```

Boolean flag that signals if a channel has exceeded the zero-suppression threshold. 

### variable trigcell

```cpp
UShort_t trigcell;
```

Trigger Cell of the channel. 

### variable adc_waveform

```cpp
UShort_t adc_waveform;
```

ADC waveform. 

### variable tdc_waveform

```cpp
UChar_t tdc_waveform;
```

TDC waveform. 

### variable trigger_data

```cpp
ULong_t trigger_data;
```

Data on the trigger of the event. 

### variable scaler

```cpp
Float_t scaler;
```

Waveform scaler. 

-------------------------------

Updated on 2022-03-07 at 17:54:19 +0000