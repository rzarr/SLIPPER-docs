---
title: RCChannelMap
summary: Class that handles the Rome Counter Channel Map. 

---

# RCChannelMap



Class that handles the Rome Counter Channel Map.  [More...](#detailed-description)

Inherits from [BaseMap](/Classes/classBaseMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[RCChannelMap](/Classes/classRCChannelMap.md#function-rcchannelmap)**()<br>Default constructor.  |
| virtual | **[~RCChannelMap](/Classes/classRCChannelMap.md#function-~rcchannelmap)**()<br>Default destructor.  |
| void | **[AddRCBoard](/Classes/classRCChannelMap.md#function-addrcboard)**(UShort_t BoardId, std::vector< Int_t > * Channels)<br>Add board to the RC channel map w/ the associated channels.  |
| virtual void | **[Clear](/Classes/classRCChannelMap.md#function-clear)**()<br>Clear RC Map.  |
| Int_t | **[GetNumberOfChannels](/Classes/classRCChannelMap.md#function-getnumberofchannels)**()<br>Get the number of RC channels.  |
| UShort_t | **[GetRCBoard](/Classes/classRCChannelMap.md#function-getrcboard)**()<br>Get the WaveDREAM board used for RC readout.  |
| std::vector< Int_t > | **[GetRCChannels](/Classes/classRCChannelMap.md#function-getrcchannels)**()<br>Get the vector of RC channels.  |
| virtual Bool_t | **[LoadMap](/Classes/classRCChannelMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x)<br>Load channel map for the RC.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual Bool_t | **[CheckMapConsistency](/Classes/classRCChannelMap.md#function-checkmapconsistency)**()<br>Check that the RC map has been loaded without errors.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::vector< Int_t > | **[_Channels](/Classes/classRCChannelMap.md#variable--channels)** <br>Vector of the RC channels.  |

## Additional inherited members

**Public Functions inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classBaseMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classBaseMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classBaseMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |

**Protected Attributes inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[_IsMapLoaded](/Classes/classBaseMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classBaseMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |


## Detailed Description

```cpp
class RCChannelMap;
```

Class that handles the Rome Counter Channel Map. 

This class contains all the needed information for the handling of WaveDAQ channels connected to the Rome Counter 

## Public Functions Documentation

### function RCChannelMap

```cpp
RCChannelMap()
```

Default constructor. 

### function ~RCChannelMap

```cpp
virtual ~RCChannelMap()
```

Default destructor. 

### function AddRCBoard

```cpp
void AddRCBoard(
    UShort_t BoardId,
    std::vector< Int_t > * Channels
)
```

Add board to the RC channel map w/ the associated channels. 

**Parameters**: 

  * **BoardId** Serial number of the RC WaveDREAM board read from XML 
  * **Channels** Pointer to vector of WDB channels of the RC read from the XML file 


### function Clear

```cpp
virtual void Clear()
```

Clear RC Map. 

### function GetNumberOfChannels

```cpp
Int_t GetNumberOfChannels()
```

Get the number of RC channels. 

**Return**: Number of RC channels loaded in the Map 

### function GetRCBoard

```cpp
UShort_t GetRCBoard()
```

Get the WaveDREAM board used for RC readout. 

**Return**: Serial number of the RC board 

### function GetRCChannels

```cpp
std::vector< Int_t > GetRCChannels()
```

Get the vector of RC channels. 

**Return**: Pointer to _Channels (vector of RC channels) 

### function LoadMap

```cpp
virtual Bool_t LoadMap(
    XmlParser * x
)
```

Load channel map for the RC. 

**Parameters**: 

  * **x** Pointer to [XmlParser](/Classes/classXmlParser.md) object 


**Return**: True if the RC ChannelMap was loaded correctly, False otherwise 

## Protected Functions Documentation

### function CheckMapConsistency

```cpp
virtual Bool_t CheckMapConsistency()
```

Check that the RC map has been loaded without errors. 

**Return**: True if the RC channel map is formed as expected, False otherwise 

This function makes sure that there is only one WaveDREAM board in the Channel Map that is connected to the Rome Counter and checks that the number of channels is the one expected from [Parameters.h]


## Protected Attributes Documentation

### variable _Channels

```cpp
std::vector< Int_t > _Channels;
```

Vector of the RC channels. 

-------------------------------

Updated on 2025-01-29 at 16:15:43 +0000