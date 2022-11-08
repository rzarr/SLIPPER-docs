---
title: WDChannelMap
summary: Main class that handles the WaveDAQ Channel Map. 

---

# WDChannelMap



Main class that handles the WaveDAQ Channel Map.  [More...](#detailed-description)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[WDChannelMap](/Classes/classWDChannelMap.md#function-wdchannelmap)**()<br>Default constructor for global channel map.  |
| [CALOChannelMap](/Classes/classCALOChannelMap.md) * | **[GetCALOChannelMap](/Classes/classWDChannelMap.md#function-getcalochannelmap)**()<br>Get the Calorimeter Channel Map.  |
| [NeutronChannelMap](/Classes/classNeutronChannelMap.md) * | **[GetNeutronChannelMap](/Classes/classWDChannelMap.md#function-getneutronchannelmap)**()<br>Get the Neutron detectors Channel Map.  |
| [RCChannelMap](/Classes/classRCChannelMap.md) * | **[GetRCChannelMap](/Classes/classWDChannelMap.md#function-getrcchannelmap)**()<br>Get the Rome Counter Channel Map.  |
| [SCChannelMap](/Classes/classSCChannelMap.md) * | **[GetSCChannelMap](/Classes/classWDChannelMap.md#function-getscchannelmap)**()<br>Get the Start Counter Channel Map.  |
| [TWChannelMap](/Classes/classTWChannelMap.md) * | **[GetTWChannelMap](/Classes/classWDChannelMap.md#function-gettwchannelmap)**()<br>Get the TOF-Wall Channel Map.  |
| Bool_t | **[IsCALOMapLoaded](/Classes/classWDChannelMap.md#function-iscalomaploaded)**()<br>Check if the CALO Channel Map has been loaded.  |
| Bool_t | **[IsNeutronMapLoaded](/Classes/classWDChannelMap.md#function-isneutronmaploaded)**()<br>Check if the Neutron Channel Map has been loaded.  |
| Bool_t | **[IsRCMapLoaded](/Classes/classWDChannelMap.md#function-isrcmaploaded)**()<br>Check if the RC Channel Map has been loaded.  |
| Bool_t | **[IsSCMapLoaded](/Classes/classWDChannelMap.md#function-isscmaploaded)**()<br>Check if the SC Channel Map has been loaded.  |
| Bool_t | **[IsTWMapLoaded](/Classes/classWDChannelMap.md#function-istwmaploaded)**()<br>Check if the TW Channel Map has been loaded.  |
| Bool_t | **[LoadMap](/Classes/classWDChannelMap.md#function-loadmap)**(std::string Filename)<br>Load the WaveDAQ channel map.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[CheckMapConsistency](/Classes/classWDChannelMap.md#function-checkmapconsistency)**()<br>Check consistency of the detector maps between them.  |
| void | **[ClearChannelMap](/Classes/classWDChannelMap.md#function-clearchannelmap)**()<br>Clear the WaveDAQ channel map.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| [CALOChannelMap](/Classes/classCALOChannelMap.md) | **[_CALOChannelMap](/Classes/classWDChannelMap.md#variable--calochannelmap)** <br>Calorimeter Channel Map.  |
| Bool_t | **[_ChannelMapIsOk](/Classes/classWDChannelMap.md#variable--channelmapisok)** <br>Boolean flag for WaveDAQ Channel Map status.  |
| [NeutronChannelMap](/Classes/classNeutronChannelMap.md) | **[_NeutronChannelMap](/Classes/classWDChannelMap.md#variable--neutronchannelmap)** <br>Neutron detectors Channel Map.  |
| [RCChannelMap](/Classes/classRCChannelMap.md) | **[_RCChannelMap](/Classes/classWDChannelMap.md#variable--rcchannelmap)** <br>Rome Counter Channel Map.  |
| [SCChannelMap](/Classes/classSCChannelMap.md) | **[_SCChannelMap](/Classes/classWDChannelMap.md#variable--scchannelmap)** <br>Start Counter Channel Map.  |
| [TWChannelMap](/Classes/classTWChannelMap.md) | **[_TWChannelMap](/Classes/classWDChannelMap.md#variable--twchannelmap)** <br>TOF-Wall Channel Map.  |

## Detailed Description

```cpp
class WDChannelMap;
```

Main class that handles the WaveDAQ Channel Map. 

This class contains the single detectors Channel Maps and handles thier loading and reading throughout event reconstruction. At this stage, the maps contained in this class are:

* Start Counter (SC) Channel Map
* TOF-Wall (TW) Channel Map
* Calorimeter (CALO) Channel Map
* Neutron detetctors Channel Map 

## Public Functions Documentation

### function WDChannelMap

```cpp
WDChannelMap()
```

Default constructor for global channel map. 

Set global control flags to false 


### function GetCALOChannelMap

```cpp
CALOChannelMap * GetCALOChannelMap()
```

Get the Calorimeter Channel Map. 

**Return**: Pointer to CALO Channel Map 

### function GetNeutronChannelMap

```cpp
NeutronChannelMap * GetNeutronChannelMap()
```

Get the Neutron detectors Channel Map. 

**Return**: Pointer to Neutron Channel Map 

### function GetRCChannelMap

```cpp
RCChannelMap * GetRCChannelMap()
```

Get the Rome Counter Channel Map. 

**Return**: Pointer to RC Channel Map 

### function GetSCChannelMap

```cpp
SCChannelMap * GetSCChannelMap()
```

Get the Start Counter Channel Map. 

**Return**: Pointer to SC Channel Map 

### function GetTWChannelMap

```cpp
TWChannelMap * GetTWChannelMap()
```

Get the TOF-Wall Channel Map. 

**Return**: Pointer to TW Channel Map 

### function IsCALOMapLoaded

```cpp
Bool_t IsCALOMapLoaded()
```

Check if the CALO Channel Map has been loaded. 

**Return**: True if the map is loaded, False otherwise 

### function IsNeutronMapLoaded

```cpp
Bool_t IsNeutronMapLoaded()
```

Check if the Neutron Channel Map has been loaded. 

**Return**: True if the map is loaded, False otherwise 

### function IsRCMapLoaded

```cpp
Bool_t IsRCMapLoaded()
```

Check if the RC Channel Map has been loaded. 

**Return**: True if the map is loaded, False otherwise 

### function IsSCMapLoaded

```cpp
Bool_t IsSCMapLoaded()
```

Check if the SC Channel Map has been loaded. 

**Return**: True if the map is loaded, False otherwise 

### function IsTWMapLoaded

```cpp
Bool_t IsTWMapLoaded()
```

Check if the TW Channel Map has been loaded. 

**Return**: True if the map is loaded, False otherwise 

### function LoadMap

```cpp
Bool_t LoadMap(
    std::string Filename
)
```

Load the WaveDAQ channel map. 

**Parameters**: 

  * **FileName** ChannelMap file name 


**Return**: True if ChannelMap was loaded correctly 

Loads all the single detectors' Channel Maps 


## Protected Functions Documentation

### function CheckMapConsistency

```cpp
Bool_t CheckMapConsistency()
```

Check consistency of the detector maps between them. 

**Return**: True if the channel maps of all detectors are fine 

### function ClearChannelMap

```cpp
void ClearChannelMap()
```

Clear the WaveDAQ channel map. 

All single detector maps are deleted 


## Protected Attributes Documentation

### variable _CALOChannelMap

```cpp
CALOChannelMap _CALOChannelMap;
```

Calorimeter Channel Map. 

### variable _ChannelMapIsOk

```cpp
Bool_t _ChannelMapIsOk;
```

Boolean flag for WaveDAQ Channel Map status. 

### variable _NeutronChannelMap

```cpp
NeutronChannelMap _NeutronChannelMap;
```

Neutron detectors Channel Map. 

### variable _RCChannelMap

```cpp
RCChannelMap _RCChannelMap;
```

Rome Counter Channel Map. 

### variable _SCChannelMap

```cpp
SCChannelMap _SCChannelMap;
```

Start Counter Channel Map. 

### variable _TWChannelMap

```cpp
TWChannelMap _TWChannelMap;
```

TOF-Wall Channel Map. 

-------------------------------

Updated on 2022-11-08 at 13:56:41 +0000