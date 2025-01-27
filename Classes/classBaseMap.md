---
title: BaseMap
summary: Base class for detector Channel Map. 

---

# BaseMap



Base class for detector Channel Map. 

Inherited by [CALOChannelMap](/Classes/classCALOChannelMap.md), [NeutronChannelMap](/Classes/classNeutronChannelMap.md), [RCChannelMap](/Classes/classRCChannelMap.md), [SCChannelMap](/Classes/classSCChannelMap.md), [TWChannelMap](/Classes/classTWChannelMap.md)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[BaseMap](/Classes/classBaseMap.md#function-basemap)**()<br>Default constructor.  |
| virtual | **[~BaseMap](/Classes/classBaseMap.md#function-~basemap)**()<br>Default destructor.  |
| void | **[Clear](/Classes/classBaseMap.md#function-clear)**()<br>Clear the list of boards loaded in the Channel Map.  |
| virtual std::vector< UShort_t > * | **[GetListOfBoards](/Classes/classBaseMap.md#function-getlistofboards)**()<br>Get the list of boards loaded in the Channel Map.  |
| virtual Bool_t | **[IsBoardLoaded](/Classes/classBaseMap.md#function-isboardloaded)**(UShort_t BoardId)<br>Check if the board has been loaded in the Channel Map.  |
| Bool_t | **[IsLoaded](/Classes/classBaseMap.md#function-isloaded)**()<br>Check if the Map has been loaded.  |
| Bool_t | **[LoadMap](/Classes/classBaseMap.md#function-loadmap)**([XmlParser](/Classes/classXmlParser.md) * x)<br>Base function for Channel Map loading.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[CheckMapConsistency](/Classes/classBaseMap.md#function-checkmapconsistency)**()<br>Base function for internal Channel Map checks.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| Bool_t | **[_IsMapLoaded](/Classes/classBaseMap.md#variable--ismaploaded)** <br>Boolean flag that checks if the map has been loaded.  |
| std::vector< UShort_t > | **[_ListOfBoards](/Classes/classBaseMap.md#variable--listofboards)** <br>List of the WaveDREAM boards in the Channel Map.  |

## Public Functions Documentation

### function BaseMap

```cpp
BaseMap()
```

Default constructor. 

### function ~BaseMap

```cpp
virtual ~BaseMap()
```

Default destructor. 

### function Clear

```cpp
void Clear()
```

Clear the list of boards loaded in the Channel Map. 

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
Bool_t LoadMap(
    XmlParser * x
)
```

Base function for Channel Map loading. 

## Protected Functions Documentation

### function CheckMapConsistency

```cpp
Bool_t CheckMapConsistency()
```

Base function for internal Channel Map checks. 

## Protected Attributes Documentation

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

Updated on 2025-01-27 at 18:20:31 +0000