---
title: TCBDATA
summary: Class for Trigger Concentrator Board data container. 

---

# TCBDATA



Class for Trigger Concentrator Board data container.  [More...](#detailed-description)


`#include <CUtils.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TCBDATA](/Classes/classTCBDATA.md#function-tcbdata)**()<br>Default constructor.  |
| void | **[clear](/Classes/classTCBDATA.md#function-clear)**()<br>Clear all the data of a TCB.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| ULong_t | **[in_waveform](/Classes/classTCBDATA.md#variable-in-waveform)** <br>in_waveform  |
| ULong_t | **[out_waveform](/Classes/classTCBDATA.md#variable-out-waveform)** <br>out_waveform  |
| ULong_t | **[gent_waveform](/Classes/classTCBDATA.md#variable-gent-waveform)** <br>TGEN bank information.  |

## Detailed Description

```cpp
class TCBDATA;
```

Class for Trigger Concentrator Board data container. 

The class contains all the information that can be extracted from the decoding of TCB events 

## Public Functions Documentation

### function TCBDATA

```cpp
inline TCBDATA()
```

Default constructor. 

### function clear

```cpp
inline void clear()
```

Clear all the data of a TCB. 

## Public Attributes Documentation

### variable in_waveform

```cpp
ULong_t in_waveform;
```

in_waveform 

### variable out_waveform

```cpp
ULong_t out_waveform;
```

out_waveform 

### variable gent_waveform

```cpp
ULong_t gent_waveform;
```

TGEN bank information. 

-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100