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
| Bool_t | **[LoadMap](/Classes/classWDChannelMap.md#function-loadmap)**(std::string Filename)<br>Load the WaveDAQ channel map.  |
| [SCChannelMap](/Classes/classSCChannelMap.md) * | **[GetSCChannelMap](/Classes/classWDChannelMap.md#function-getscchannelmap)**()<br>Get the Start Counter Channel Map.  |
| [TWChannelMap](/Classes/classTWChannelMap.md) * | **[GetTWChannelMap](/Classes/classWDChannelMap.md#function-gettwchannelmap)**()<br>Get the TOF-Wall Channel Map.  |
| [CALOChannelMap](/Classes/classCALOChannelMap.md) * | **[GetCALOChannelMap](/Classes/classWDChannelMap.md#function-getcalochannelmap)**()<br>Get the Calorimeter Channel Map.  |
| [NeutronChannelMap](/Classes/classNeutronChannelMap.md) * | **[GetNeutronChannelMap](/Classes/classWDChannelMap.md#function-getneutronchannelmap)**()<br>Get the Neutron detectors Channel Map.  |
| Bool_t | **[IsSCMapLoaded](/Classes/classWDChannelMap.md#function-isscmaploaded)**()<br>Check if the SC Channel Map has been loaded.  |
| Bool_t | **[IsTWMapLoaded](/Classes/classWDChannelMap.md#function-istwmaploaded)**()<br>Check if the TW Channel Map has been loaded.  |
| Bool_t | **[IsCALOMapLoaded](/Classes/classWDChannelMap.md#function-iscalomaploaded)**()<br>Check if the CALO Channel Map has been loaded.  |
| Bool_t | **[IsNeutronMapLoaded](/Classes/classWDChannelMap.md#function-isneutronmaploaded)**()<br>Check if the Neutron Channel Map has been loaded.  |

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

-------------------------------

Updated on 2021-12-29 at 15:02:03 +0100