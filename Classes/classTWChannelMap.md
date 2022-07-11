---
title: TWChannelMap
summary: Class that handles the TOF-Wall Channel Map. 

---

# TWChannelMap



Class that handles the TOF-Wall Channel Map.  [More...](#detailed-description)

Inherits from [BaseMap](/Classes/classBaseMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TWChannelMap](/Classes/classTWChannelMap.md#function-twchannelmap)**()<br>Default constructor.  |
| virtual | **[~TWChannelMap](/Classes/classTWChannelMap.md#function-~twchannelmap)**()<br>Default destructor.  |
| TBoardChannelToGlobalMap | **[GetBoardChannelToGlobalMap](/Classes/classTWChannelMap.md#function-getboardchanneltoglobalmap)**()<br>Get the WaveDREAM board-channel to TW global channel map.  |
| TGlobalToBarChIDpairMap | **[GetGlobalToBarChIDpairMap](/Classes/classTWChannelMap.md#function-getglobaltobarchidpairmap)**()<br>Get the TW global channel to bar number-channel Id ("A"/"B") map.  |
| TMapBarIdLayerId | **[GetBarLayerMap](/Classes/classTWChannelMap.md#function-getbarlayermap)**()<br>Get the TW bar to layer map.  |
| TLayer | **[GetLayer](/Classes/classTWChannelMap.md#function-getlayer)**(Int_t bar)<br>Get the layer of a TW bar.  |
| Int_t | **[GetGlobalFromBoardChannelPair](/Classes/classTWChannelMap.md#function-getglobalfromboardchannelpair)**(std::pair< UShort_t, Int_t > p)<br>Get the WaveDREAM board-channel pair connected to a TW global channel.  |
| Int_t | **[GetNumberOfTWBars](/Classes/classTWChannelMap.md#function-getnumberoftwbars)**()<br>Get the total number of TW bars loaded in the map.  |
| std::pair< Int_t, Int_t > | **[GetBoardChsFromFragBar](/Classes/classTWChannelMap.md#function-getboardchsfromfragbar)**(Int_t barId)<br>Get the global channels connected to a bar involved in the fragmentation trigger logic.  |
| virtual Bool_t | **[LoadMap](/Classes/classTWChannelMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x)<br>Load the TW channel map.  |
| virtual void | **[Clear](/Classes/classTWChannelMap.md#function-clear)**()<br>Clear data of TW map.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classTWChannelMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classTWChannelMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classTWChannelMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddBar](/Classes/classTWChannelMap.md#function-addbar)**(Int_t BarId, TLayer Layer, UShort_t BoardId, Int_t ChannelA, Int_t ChannelB, Int_t GlobalChannelA, Int_t GlobalChannelB)<br>Load the information of a single TW bar in the map.  |
| virtual Bool_t | **[CheckMapConsistency](/Classes/classTWChannelMap.md#function-checkmapconsistency)**()<br>Check TW map consistency.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| TMapBarIdLayerId | **[_BarLayerMap](/Classes/classTWChannelMap.md#variable--barlayermap)** <br>Map that links the TW bar to its layer.  |
| TBoardChannelToGlobalMap | **[_BoardChannelToGlobalMap](/Classes/classTWChannelMap.md#variable--boardchanneltoglobalmap)** <br>Map that links the WaveDREAM board-channel pair to the TW global channel.  |
| TGlobalToBarChIDpairMap | **[_GlobalToBarChIDpairMap](/Classes/classTWChannelMap.md#variable--globaltobarchidpairmap)** <br>Map that links the TW global channel with the Bar number-channel id ("A"/"B") pair.  |
| std::map< Int_t, std::pair< Int_t, Int_t > > | **[_FragBarToChPair](/Classes/classTWChannelMap.md#variable--fragbartochpair)** <br>Map that links fragmentation bars to their two global channels.  |
| Bool_t | **[_IsMapLoaded](/Classes/classTWChannelMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classTWChannelMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |

## Additional inherited members

**Public Functions inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |


## Detailed Description

```cpp
class TWChannelMap;
```

Class that handles the TOF-Wall Channel Map. 

This class contains all the information about the connections between WaveDAQ and the TOF-Wall detector. 

## Public Functions Documentation

### function TWChannelMap

```cpp
TWChannelMap()
```

Default constructor. 

### function ~TWChannelMap

```cpp
virtual ~TWChannelMap()
```

Default destructor. 

### function GetBoardChannelToGlobalMap

```cpp
TBoardChannelToGlobalMap GetBoardChannelToGlobalMap()
```

Get the WaveDREAM board-channel to TW global channel map. 

**Return**: Map object 

### function GetGlobalToBarChIDpairMap

```cpp
TGlobalToBarChIDpairMap GetGlobalToBarChIDpairMap()
```

Get the TW global channel to bar number-channel Id ("A"/"B") map. 

**Return**: Map object 

### function GetBarLayerMap

```cpp
TMapBarIdLayerId GetBarLayerMap()
```

Get the TW bar to layer map. 

**Return**: Map object 

### function GetLayer

```cpp
TLayer GetLayer(
    Int_t bar
)
```

Get the layer of a TW bar. 

**Parameters**: 

  * **barId** TW bar number 


**Return**: Layer of the TW bar 

### function GetGlobalFromBoardChannelPair

```cpp
Int_t GetGlobalFromBoardChannelPair(
    std::pair< UShort_t, Int_t > p
)
```

Get the WaveDREAM board-channel pair connected to a TW global channel. 

**Parameters**: 

  * **p** Pair with WaveDREAM board serial number and channel index 


**Return**: 

### function GetNumberOfTWBars

```cpp
Int_t GetNumberOfTWBars()
```

Get the total number of TW bars loaded in the map. 

**Return**: Number of TW bars loaded 

### function GetBoardChsFromFragBar

```cpp
std::pair< Int_t, Int_t > GetBoardChsFromFragBar(
    Int_t barId
)
```

Get the global channels connected to a bar involved in the fragmentation trigger logic. 

**Parameters**: 

  * **barId** Number of the TW bar 


**Return**: Pair of the two global channels connected to the bar 

### function LoadMap

```cpp
virtual Bool_t LoadMap(
    XmlParser * x
)
```

Load the TW channel map. 

**Parameters**: 

  * **x** Pointer to [XmlParser](/Classes/classXmlParser.md) object 


**Return**: True if the TW channel map was loaded correctly, False otherwise 

### function Clear

```cpp
virtual void Clear()
```

Clear data of TW map. 

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

### function AddBar

```cpp
void AddBar(
    Int_t BarId,
    TLayer Layer,
    UShort_t BoardId,
    Int_t ChannelA,
    Int_t ChannelB,
    Int_t GlobalChannelA,
    Int_t GlobalChannelB
)
```

Load the information of a single TW bar in the map. 

**Parameters**: 

  * **BarId** Id of the bar 
  * **Layer** TW layer 
  * **BoardId** Id of the WaveDREAM board 
  * **ChannelA** Id of the channel A (WDB) 
  * **ChannelB** Id of the channel B (WDB) 
  * **GlobalChannelA** Global Id of channel A 
  * **GlobalChannelB** Global Id of channel B 


### function CheckMapConsistency

```cpp
virtual Bool_t CheckMapConsistency()
```

Check TW map consistency. 

**Return**: True if the TW channel map is formed as expected, False otherwise 

This function makes sure that there are no repeated/doubled indices and that the number of TW bars loaded is equal to the expected one (check [Parameters.h]) 


## Protected Attributes Documentation

### variable _BarLayerMap

```cpp
TMapBarIdLayerId _BarLayerMap;
```

Map that links the TW bar to its layer. 

### variable _BoardChannelToGlobalMap

```cpp
TBoardChannelToGlobalMap _BoardChannelToGlobalMap;
```

Map that links the WaveDREAM board-channel pair to the TW global channel. 

### variable _GlobalToBarChIDpairMap

```cpp
TGlobalToBarChIDpairMap _GlobalToBarChIDpairMap;
```

Map that links the TW global channel with the Bar number-channel id ("A"/"B") pair. 

### variable _FragBarToChPair

```cpp
std::map< Int_t, std::pair< Int_t, Int_t > > _FragBarToChPair;
```

Map that links fragmentation bars to their two global channels. 

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

Updated on 2022-07-11 at 18:28:26 +0000