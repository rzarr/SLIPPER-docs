---
title: src/ChannelMap/BaseMap.h
summary: Header of BaseMap.cxx. 

---

# src/ChannelMap/BaseMap.h

Header of [BaseMap.cxx](/Files/BaseMap_8cxx.md#file-basemap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[BaseMap](/Classes/classBaseMap.md)** <br>Base class for detector Channel Map.  |

## Detailed Description

Header of [BaseMap.cxx](/Files/BaseMap_8cxx.md#file-basemap.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef BASEMAP_H
#define BASEMAP_H

#include <string>
#include <TSystem.h>
#include "XmlParser.h"
#include "Parameters.h"

// Base class for the channel map of different detectors
class BaseMap
{
protected:
    Bool_t _IsMapLoaded;                    
    std::vector<UShort_t> _ListOfBoards;    
    Bool_t  CheckMapConsistency();

public:
    BaseMap();
    virtual ~BaseMap();
    virtual std::vector<UShort_t>*  GetListOfBoards();
    virtual Bool_t  IsBoardLoaded(UShort_t BoardId);
    Bool_t  LoadMap(XmlParser* x);
    Bool_t  IsLoaded();
    void    Clear();
};

#endif
```


-------------------------------

Updated on 2022-01-12 at 16:47:44 +0000
