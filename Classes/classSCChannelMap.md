---
title: SCChannelMap
summary: Class that handles the Start Counter Channel Map. 

---

# SCChannelMap



Class that handles the Start Counter Channel Map.  [More...](#detailed-description)

Inherits from [BaseMap](/Classes/classBaseMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SCChannelMap](/Classes/classSCChannelMap.md#function-scchannelmap)**()<br>Default constructor.  |
| virtual | **[~SCChannelMap](/Classes/classSCChannelMap.md#function-~scchannelmap)**()<br>Default destructor.  |
| UShort_t | **[GetSCBoard](/Classes/classSCChannelMap.md#function-getscboard)**()<br>Get the WaveDREAM board used for SC readout.  |
| Int_t | **[GetNumberOfChannels](/Classes/classSCChannelMap.md#function-getnumberofchannels)**()<br>Get the number of SC channels.  |
| std::vector< Int_t > | **[GetSCChannels](/Classes/classSCChannelMap.md#function-getscchannels)**()<br>Get the vector of SC channels.  |
| void | **[AddSCBoard](/Classes/classSCChannelMap.md#function-addscboard)**(UShort_t BoardId, std::vector< Int_t > * Channels)<br>Add board to the SC channel map w/ the associated channels.  |
| virtual Bool_t | **[LoadMap](/Classes/classSCChannelMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x)<br>Load channel map for the SC.  |
| virtual void | **[Clear](/Classes/classSCChannelMap.md#function-clear)**()<br>Clear SC Map.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classSCChannelMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classSCChannelMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classSCChannelMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual Bool_t | **[CheckMapConsistency](/Classes/classSCChannelMap.md#function-checkmapconsistency)**()<br>Check that the SC map has been loaded without errors.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::vector< Int_t > | **[_Channels](/Classes/classSCChannelMap.md#variable--channels)** <br>Vector of the SC channels.  |
| Bool_t | **[_IsMapLoaded](/Classes/classSCChannelMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classSCChannelMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |

## Additional inherited members

**Public Functions inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |


## Detailed Description

```cpp
class SCChannelMap;
```

Class that handles the Start Counter Channel Map. 

This class contains all the needed information for the handling of WaveDAQ channels connected to the Start Counter 

## Public Functions Documentation

### function SCChannelMap

```cpp
SCChannelMap()
```

Default constructor. 

### function ~SCChannelMap

```cpp
virtual ~SCChannelMap()
```

Default destructor. 

### function GetSCBoard

```cpp
UShort_t GetSCBoard()
```

Get the WaveDREAM board used for SC readout. 

**Return**: Serial number of the SC board 

### function GetNumberOfChannels

```cpp
Int_t GetNumberOfChannels()
```

Get the number of SC channels. 

**Return**: Number of SC channels loaded in the Map 

### function GetSCChannels

```cpp
std::vector< Int_t > GetSCChannels()
```

Get the vector of SC channels. 

**Return**: Pointer to _Channels (vector of SC channels) 

### function AddSCBoard

```cpp
void AddSCBoard(
    UShort_t BoardId,
    std::vector< Int_t > * Channels
)
```

Add board to the SC channel map w/ the associated channels. 

**Parameters**: 

  * **BoardId** Serial number of the SC WaveDREAM board read from XML 
  * **Channels** Pointer to vector of WDB channels of the SC read from the XML file 


### function LoadMap

```cpp
virtual Bool_t LoadMap(
    XmlParser * x
)
```

Load channel map for the SC. 

**Parameters**: 

  * **x** Pointer to [XmlParser](/Classes/classXmlParser.md) object 


**Return**: True if the SC ChannelMap was loaded correctly, False otherwise 

### function Clear

```cpp
virtual void Clear()
```

Clear SC Map. 

### function GetListOfBoards

```cpp
virtual std::vector< UShort_t > * GetListOfBoards()
```

Get the list of boards loaded in the Channel Map. 

**Return**: Pointer to the vector of loaded boards 

### function IsBoardLoaded

```cpp
virtual Bool_t IsBoardLoaded(
    UShort_t BoardId
)
```

Check if the board has been loaded in the Channel Map. 

**Parameters**: 

  * **BoardId** Board serial number 


**Return**: True if the board is has been loaded in the corresponding Channel Map 

### function IsLoaded

```cpp
Bool_t IsLoaded()
```

Check if the Map has been loaded. 

**Return**: True if the Map is loaded, False otherwise 

## Protected Functions Documentation

### function CheckMapConsistency

```cpp
virtual Bool_t CheckMapConsistency()
```

Check that the SC map has been loaded without errors. 

**Return**: True if the SC channel map is formed as expected, False otherwise 

This function makes sure that there is only one WaveDREAM board in the Channel Map that is connected to the Start Counter and checks that the number of channels is the one expected from [Parameters.h]


## Protected Attributes Documentation

### variable _Channels

```cpp
std::vector< Int_t > _Channels;
```

Vector of the SC channels. 

### variable _IsMapLoaded

```cpp
Bool_t _IsMapLoaded;
```

Boolean flag that checks if the map has been loaded. 

### variable _ListOfBoards

```cpp
std::vector< UShort_t > _ListOfBoards;
```

List of the WaveDREAM boards in the Channel Map. 

-------------------------------

Updated on 2022-07-12 at 15:22:20 +0000