---
title: CALOChannelMap
summary: Class that handles the Calorimeter Channel Map. 

---

# CALOChannelMap



Class that handles the Calorimeter Channel Map.  [More...](#detailed-description)

Inherits from [BaseMap](/Classes/classBaseMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CALOChannelMap](/Classes/classCALOChannelMap.md#function-calochannelmap)**()<br>Default constructor.  |
| virtual | **[~CALOChannelMap](/Classes/classCALOChannelMap.md#function-~calochannelmap)**()<br>Default destructor.  |
| virtual void | **[Clear](/Classes/classCALOChannelMap.md#function-clear)**() |
| Bool_t | **[CrystalHasPosition](/Classes/classCALOChannelMap.md#function-crystalhasposition)**(Int_t CrysId)<br>Check if a CALO crystal has position information in the ChannelMap.  |
| std::pair< UShort_t, Int_t > | **[GetBoardChFromCrys](/Classes/classCALOChannelMap.md#function-getboardchfromcrys)**(Int_t CrysId)<br>Get the <board, channel> pair from the Id of the crystal.  |
| std::vector< std::pair< UShort_t, Int_t > > | **[GetBoardChVec](/Classes/classCALOChannelMap.md#function-getboardchvec)**(Int_t ModuleId)<br>Get the <board, channel> vector of all the crystals in a CALO module.  |
| Bool_t | **[GetCrystalId](/Classes/classCALOChannelMap.md#function-getcrystalid)**(UShort_t board, Int_t channel, Int_t * CrysId)<br>Get the Id of a crystal from its board and channel.  |
| Int_t | **[GetCrystalIdFromIndex](/Classes/classCALOChannelMap.md#function-getcrystalidfromindex)**(Int_t CrysIndex)<br>Get the Id of a crystal from its board and channel.  |
| Int_t | **[GetCrystalIndexFromId](/Classes/classCALOChannelMap.md#function-getcrystalindexfromid)**(Int_t CrysId)<br>Get the index of a CALO crystal from its Id.  |
| const TVector2 | **[GetCrystalPosition](/Classes/classCALOChannelMap.md#function-getcrystalposition)**(Int_t CrysId)<br>Get the X-Y position of a CALO crystal.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classCALOChannelMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| std::vector< Int_t > | **[GetListOfCrysIndex](/Classes/classCALOChannelMap.md#function-getlistofcrysindex)**(Int_t ModuleId)<br>Get the vector of crystal indices associated to a CALO module.  |
| Int_t | **[GetModuleFromCrys](/Classes/classCALOChannelMap.md#function-getmodulefromcrys)**(Int_t CrysId) |
| Int_t | **[GetNumberOfCALOModules](/Classes/classCALOChannelMap.md#function-getnumberofcalomodules)**()<br>Get the number of Calorimeter Modules.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classCALOChannelMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classCALOChannelMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |
| virtual Bool_t | **[LoadMap](/Classes/classCALOChannelMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x) |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddModule](/Classes/classCALOChannelMap.md#function-addmodule)**(Int_t ModuleId, std::vector< UShort_t > Boards, std::vector< Int_t > Channels, std::vector< Int_t > Crystals)<br>Add a CALO module to the channel map.  |
| void | **[AddPositions](/Classes/classCALOChannelMap.md#function-addpositions)**([XmlParser](/Classes/classXmlParser.md) * x, XMLNodePointer_t x_child) |
| virtual Bool_t | **[CheckMapConsistency](/Classes/classCALOChannelMap.md#function-checkmapconsistency)**()<br>Check the consistency of the CALO channel map.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< std::pair< UShort_t, Int_t >, Int_t > | **[_BoardChToCrysMap](/Classes/classCALOChannelMap.md#variable--boardchtocrysmap)** <br>Map that links the WaveDREAM board-channel pair to the corresponding CALO Crystal.  |
| std::map< Int_t, Int_t > | **[_CrysIndexToId](/Classes/classCALOChannelMap.md#variable--crysindextoid)** <br>Map that links a CALO crystal index to its Id in the ChannelMap.  |
| std::map< Int_t, TVector2 > | **[_CrysToPosMap](/Classes/classCALOChannelMap.md#variable--crystoposmap)** <br>Map that links the CALO crystal to its X-Y position.  |
| Bool_t | **[_IsMapLoaded](/Classes/classCALOChannelMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classCALOChannelMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |
| std::map< Int_t, std::vector< std::pair< UShort_t, Int_t > > > | **[_ModToBoardChMap](/Classes/classCALOChannelMap.md#variable--modtoboardchmap)** <br>Map that links a Calorimeter module with all the WaveDREAM board-channel pairs of the corresponding Crystals.  |
| std::map< Int_t, std::vector< Int_t > > | **[_ModToCrysIndex](/Classes/classCALOChannelMap.md#variable--modtocrysindex)** <br>Map that links a CALO module to the vector of crystal indices.  |

## Additional inherited members

**Public Functions inherited from [BaseMap](/Classes/classBaseMap.md)**

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |


## Detailed Description

```cpp
class CALOChannelMap;
```

Class that handles the Calorimeter Channel Map. 

This class contains all the needed information to link each Calorimeter Crystal/Module with the corresponding WaveDREAM board-channel 

## Public Functions Documentation

### function CALOChannelMap

```cpp
CALOChannelMap()
```

Default constructor. 

### function ~CALOChannelMap

```cpp
virtual ~CALOChannelMap()
```

Default destructor. 

### function Clear

```cpp
virtual void Clear()
```


Clear the CALO channel map 


### function CrystalHasPosition

```cpp
Bool_t CrystalHasPosition(
    Int_t CrysId
)
```

Check if a CALO crystal has position information in the ChannelMap. 

**Parameters**: 

  * **CrysId** Index of the CALO crystal 


**Return**: True if the crystal has position information; false otherwise 

### function GetBoardChFromCrys

```cpp
std::pair< UShort_t, Int_t > GetBoardChFromCrys(
    Int_t CrysId
)
```

Get the <board, channel> pair from the Id of the crystal. 

**Parameters**: 

  * **CrysId** Id of the CALO crystal 


**Return**: Pair containing the corresponding board serial number and channel Id 

### function GetBoardChVec

```cpp
std::vector< std::pair< UShort_t, Int_t > > GetBoardChVec(
    Int_t ModuleId
)
```

Get the <board, channel> vector of all the crystals in a CALO module. 

**Parameters**: 

  * **ModuleId** Id of the module 


**Return**: Pair containing the corresponding board serial number and channel Id 

### function GetCrystalId

```cpp
Bool_t GetCrystalId(
    UShort_t board,
    Int_t channel,
    Int_t * CrysId
)
```

Get the Id of a crystal from its board and channel. 

**Parameters**: 

  * **board** Board serial number 
  * **channel** Channel Id 
  * **CrysId** Pointer to variable to write the crystal Id 


**Return**: True if the crystal was found in the CALO channel map, False otherwise 

### function GetCrystalIdFromIndex

```cpp
Int_t GetCrystalIdFromIndex(
    Int_t CrysIndex
)
```

Get the Id of a crystal from its board and channel. 

**Parameters**: 

  * **CrysIndexd** Pointer to variable to write the crystal Id 


**Return**: True if the crystal was found in the CALO channel map, False otherwise 

### function GetCrystalIndexFromId

```cpp
Int_t GetCrystalIndexFromId(
    Int_t CrysId
)
```

Get the index of a CALO crystal from its Id. 

**Parameters**: 

  * **CrysId** Id of the CALO crystal 


**Return**: Index of the crystal 

### function GetCrystalPosition

```cpp
const TVector2 GetCrystalPosition(
    Int_t CrysId
)
```

Get the X-Y position of a CALO crystal. 

**Parameters**: 

  * **CrysId** Index of the CALO crystal 


**Return**: Vector of the X-Y position of the crystal 

### function GetListOfBoards

```cpp
virtual std::vector< UShort_t > * GetListOfBoards()
```

Get the list of boards loaded in the Channel Map. 

**Return**: Pointer to the vector of loaded boards 

### function GetListOfCrysIndex

```cpp
std::vector< Int_t > GetListOfCrysIndex(
    Int_t ModuleId
)
```

Get the vector of crystal indices associated to a CALO module. 

**Parameters**: 

  * **ModuleId** Id of the module 


**Return**: Vector of crystal indices of that CALO module 

### function GetModuleFromCrys

```cpp
Int_t GetModuleFromCrys(
    Int_t CrysId
)
```


**Parameters**: 

  * **CrysId** Crystal Id 


**Return**: Id of the corresponding module 

Get the Id of a CALO module from its crystal 


### function GetNumberOfCALOModules

```cpp
Int_t GetNumberOfCALOModules()
```

Get the number of Calorimeter Modules. 

**Return**: Total number of CALO modules 

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


**Parameters**: 

  * **x** Pointer to [XmlParser](/Classes/classXmlParser.md) object 


**Return**: True if the CALO ChannelMap was loaded correctly 

Load the CALO channel Map 


## Protected Functions Documentation

### function AddModule

```cpp
void AddModule(
    Int_t ModuleId,
    std::vector< UShort_t > Boards,
    std::vector< Int_t > Channels,
    std::vector< Int_t > Crystals
)
```

Add a CALO module to the channel map. 

**Parameters**: 

  * **ModuleId** Id of the module read from the XML file 
  * **Boards** Vector of the boards' serial numbers read from the XML file 
  * **Channels** Vector of channels Ids read from the XML file 
  * **Crystals** Vector of crystal Ids read from the XML file 


### function AddPositions

```cpp
void AddPositions(
    XmlParser * x,
    XMLNodePointer_t x_child
)
```


### function CheckMapConsistency

```cpp
virtual Bool_t CheckMapConsistency()
```

Check the consistency of the CALO channel map. 

**Return**: True if the map is formed as expected, False otherwise 

This function checks that the map has been loaded correctly, without repeated/double indices, and with the expected number of CALO modules/crystals (check [Parameters.h]) 


## Protected Attributes Documentation

### variable _BoardChToCrysMap

```cpp
std::map< std::pair< UShort_t, Int_t >, Int_t > _BoardChToCrysMap;
```

Map that links the WaveDREAM board-channel pair to the corresponding CALO Crystal. 

### variable _CrysIndexToId

```cpp
std::map< Int_t, Int_t > _CrysIndexToId;
```

Map that links a CALO crystal index to its Id in the ChannelMap. 

### variable _CrysToPosMap

```cpp
std::map< Int_t, TVector2 > _CrysToPosMap;
```

Map that links the CALO crystal to its X-Y position. 

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

### variable _ModToBoardChMap

```cpp
std::map< Int_t, std::vector< std::pair< UShort_t, Int_t > > > _ModToBoardChMap;
```

Map that links a Calorimeter module with all the WaveDREAM board-channel pairs of the corresponding Crystals. 

### variable _ModToCrysIndex

```cpp
std::map< Int_t, std::vector< Int_t > > _ModToCrysIndex;
```

Map that links a CALO module to the vector of crystal indices. 

-------------------------------

Updated on 2022-11-07 at 18:21:11 +0000