---
title: NeutronChannelMap
summary: Class that handles all the WaveDREAM boards-channels connected to Neutron detectors. 

---

# NeutronChannelMap



Class that handles all the WaveDREAM boards-channels connected to Neutron detectors.  [More...](#detailed-description)

Inherits from [BaseMap](/Classes/classBaseMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[NeutronChannelMap](/Classes/classNeutronChannelMap.md#function-neutronchannelmap)**()<br>Default constructor.  |
| virtual | **[~NeutronChannelMap](/Classes/classNeutronChannelMap.md#function-~neutronchannelmap)**()<br>Default destructor.  |
| virtual void | **[Clear](/Classes/classNeutronChannelMap.md#function-clear)**()<br>Clear the Neutron Channel Map.  |
| UShort_t | **[GetBoardFast](/Classes/classNeutronChannelMap.md#function-getboardfast)**()<br>Get the Fast board Id.  |
| UShort_t | **[GetBoardSlow](/Classes/classNeutronChannelMap.md#function-getboardslow)**()<br>Get the Slow board Id.  |
| std::vector< Int_t > * | **[GetChFast](/Classes/classNeutronChannelMap.md#function-getchfast)**()<br>Get the Fast channels of the Neutron detectors.  |
| std::vector< Int_t > * | **[GetChSlow](/Classes/classNeutronChannelMap.md#function-getchslow)**()<br>Get the Slow channels of the Neutron detectors.  |
| std::string | **[GetDetFromBoardCh](/Classes/classNeutronChannelMap.md#function-getdetfromboardch)**(std::pair< UShort_t, Int_t > BoardChPair)<br>Get the neutron detector name from board-chanel pair.  |
| Bool_t | **[GetGlobFromBoardCh](/Classes/classNeutronChannelMap.md#function-getglobfromboardch)**(std::pair< UShort_t, Int_t > BoardChPair, Int_t * globCh)<br>Get the global channel Id from board-chanel pair.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classNeutronChannelMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classNeutronChannelMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classNeutronChannelMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |
| virtual Bool_t | **[LoadMap](/Classes/classNeutronChannelMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x)<br>Load the Neutron detector in the channel Map.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddDetector](/Classes/classNeutronChannelMap.md#function-adddetector)**(std::string DetName, UShort_t BoardSlow, std::vector< Int_t > ChSlow, std::vector< Int_t > GlobSlow, UShort_t BoardFast, std::vector< Int_t > ChFast, std::vector< Int_t > GlobFast)<br>Add a Neutron detector to the channel map.  |
| virtual Bool_t | **[CheckMapConsistency](/Classes/classNeutronChannelMap.md#function-checkmapconsistency)**()<br>Check the consistency of the Neutrons channel map.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< std::pair< UShort_t, Int_t >, std::string > | **[_BoardChToDetMap](/Classes/classNeutronChannelMap.md#variable--boardchtodetmap)** <br>Map linking board-channel pairs to the corresponding detector name.  |
| std::map< std::pair< UShort_t, Int_t >, Int_t > | **[_BoardChToGlobMap](/Classes/classNeutronChannelMap.md#variable--boardchtoglobmap)** <br>Map linking board-channel pairs to the corresponding global neutron channel index.  |
| UShort_t | **[_BoardFast](/Classes/classNeutronChannelMap.md#variable--boardfast)** <br>WaveDREAM board of neutron fast channels.  |
| UShort_t | **[_BoardSlow](/Classes/classNeutronChannelMap.md#variable--boardslow)** <br>WaveDREAM board of neutron slow channels.  |
| std::vector< Int_t > | **[_FastCh](/Classes/classNeutronChannelMap.md#variable--fastch)** <br>List of channels used in the fast board.  |
| Bool_t | **[_IsMapLoaded](/Classes/classNeutronChannelMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classNeutronChannelMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |
| std::vector< Int_t > | **[_SlowCh](/Classes/classNeutronChannelMap.md#variable--slowch)** <br>List of channels used in the slow board.  |

## Additional inherited members

**Public Functions inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |


## Detailed Description

```cpp
class NeutronChannelMap;
```

Class that handles all the WaveDREAM boards-channels connected to Neutron detectors. 

This map supports different Neutron detectors with channels in two WaveDREAM boards. In particular, the class expects a series of detectors with channels in exactly one FAST and one SLOW WaveDREAM board 

## Public Functions Documentation

### function NeutronChannelMap

```cpp
NeutronChannelMap()
```

Default constructor. 

### function ~NeutronChannelMap

```cpp
virtual ~NeutronChannelMap()
```

Default destructor. 

### function Clear

```cpp
virtual void Clear()
```

Clear the Neutron Channel Map. 

Clear all vectors of the Channel Map 


### function GetBoardFast

```cpp
UShort_t GetBoardFast()
```

Get the Fast board Id. 

**Return**: Serial number of the Neutron Fast Board 

### function GetBoardSlow

```cpp
UShort_t GetBoardSlow()
```

Get the Slow board Id. 

**Return**: Serial number of the Neutron Slow Board 

### function GetChFast

```cpp
std::vector< Int_t > * GetChFast()
```

Get the Fast channels of the Neutron detectors. 

**Return**: Pointer to the vector of Fast channels 

### function GetChSlow

```cpp
std::vector< Int_t > * GetChSlow()
```

Get the Slow channels of the Neutron detectors. 

**Return**: Pointer to the vector of Slow channels 

### function GetDetFromBoardCh

```cpp
std::string GetDetFromBoardCh(
    std::pair< UShort_t, Int_t > BoardChPair
)
```

Get the neutron detector name from board-chanel pair. 

**Parameters**: 

  * **BoardChPair** Pair containing the board serial number and channel 


**Return**: Name of the associated detector as std::string 

### function GetGlobFromBoardCh

```cpp
Bool_t GetGlobFromBoardCh(
    std::pair< UShort_t, Int_t > BoardChPair,
    Int_t * globCh
)
```

Get the global channel Id from board-chanel pair. 

**Parameters**: 

  * **BoardChPair** Pair containing the board serial number and channel 
  * **globCh** Pointer to variable that will contain the global channel Id 


**Return**: True if the board-channel pair exists in the neutron map, false otherwise 

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

### function LoadMap

```cpp
virtual Bool_t LoadMap(
    XmlParser * x
)
```

Load the Neutron detector in the channel Map. 

**Parameters**: 

  * **x** Pointer to [XmlParser](/Classes/classXmlParser.md) object 


**Return**: True if the CALO ChannelMap was loaded correctly, False otherwise 

## Protected Functions Documentation

### function AddDetector

```cpp
void AddDetector(
    std::string DetName,
    UShort_t BoardSlow,
    std::vector< Int_t > ChSlow,
    std::vector< Int_t > GlobSlow,
    UShort_t BoardFast,
    std::vector< Int_t > ChFast,
    std::vector< Int_t > GlobFast
)
```

Add a Neutron detector to the channel map. 

**Parameters**: 

  * **DetName** Name of the detector 
  * **BoardSlow** Serial number of the board for slow signals 
  * **ChSlow** Vector of slow channel Ids 
  * **GlobSlow** Vector of slow global channel Ids 
  * **BoardFast** Serial number of the board for fast signals 
  * **ChFast** Vector of fast channel Ids 
  * **GlobFast** Vector of fast global channel Ids 


### function CheckMapConsistency

```cpp
virtual Bool_t CheckMapConsistency()
```

Check the consistency of the Neutrons channel map. 

**Return**: True if the map is formed as expected, False otherwise 

This functions checks that the Neutron detectors are connected to exactly one Slow and one Fast WaveDREAM board. Moreover, it checks that both slow and fast channels have been loaded and are exactly in the expected number (check [Parameters.h]) 


## Protected Attributes Documentation

### variable _BoardChToDetMap

```cpp
std::map< std::pair< UShort_t, Int_t >, std::string > _BoardChToDetMap;
```

Map linking board-channel pairs to the corresponding detector name. 

### variable _BoardChToGlobMap

```cpp
std::map< std::pair< UShort_t, Int_t >, Int_t > _BoardChToGlobMap;
```

Map linking board-channel pairs to the corresponding global neutron channel index. 

### variable _BoardFast

```cpp
UShort_t _BoardFast = 0;
```

WaveDREAM board of neutron fast channels. 

### variable _BoardSlow

```cpp
UShort_t _BoardSlow = 0;
```

WaveDREAM board of neutron slow channels. 

### variable _FastCh

```cpp
std::vector< Int_t > _FastCh;
```

List of channels used in the fast board. 

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

### variable _SlowCh

```cpp
std::vector< Int_t > _SlowCh;
```

List of channels used in the slow board. 

-------------------------------

Updated on 2022-11-07 at 18:21:11 +0000