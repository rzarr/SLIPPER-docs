---
title: NeutronWF
summary: Class for Neutron WaveForms storing. 

---

# NeutronWF



Class for Neutron WaveForms storing.  [More...](#detailed-description)


`#include <CUtils.h>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[NeutronWF](/Classes/classNeutronWF.md#function-neutronwf)**()<br>Default constructor.  |
| void | **[clear](/Classes/classNeutronWF.md#function-clear)**()<br>Clear all data in the container.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[IsOn](/Classes/classNeutronWF.md#variable-ison)** <br>Boolean flag for WaveDAQ zero-suppression.  |
| Float_t | **[T](/Classes/classNeutronWF.md#variable-t)** <br>Time values of the Waveforms.  |
| Float_t | **[V](/Classes/classNeutronWF.md#variable-v)** <br>Amplitude values of the Waveforms.  |

## Detailed Description

```cpp
class NeutronWF;
```

Class for Neutron WaveForms storing. 

This class is only used when the "save neutrons" flag is activated in the Reconstruction executable 

## Public Functions Documentation

### function NeutronWF

```cpp
inline NeutronWF()
```

Default constructor. 

### function clear

```cpp
inline void clear()
```

Clear all data in the container. 

## Public Attributes Documentation

### variable IsOn

```cpp
Bool_t IsOn;
```

Boolean flag for WaveDAQ zero-suppression. 

### variable T

```cpp
Float_t T;
```

Time values of the Waveforms. 

### variable V

```cpp
Float_t V;
```

Amplitude values of the Waveforms. 

-------------------------------

Updated on 2025-01-27 at 18:13:43 +0000