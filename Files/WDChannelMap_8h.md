---
title: src/ChannelMap/WDChannelMap.h
summary: Header of WDChannelMap.cxx. 

---

# src/ChannelMap/WDChannelMap.h

Header of [WDChannelMap.cxx](/Files/WDChannelMap_8cxx.md#file-wdchannelmap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[WDChannelMap](/Classes/classWDChannelMap.md)** <br>Main class that handles the WaveDAQ Channel Map.  |

## Detailed Description

Header of [WDChannelMap.cxx](/Files/WDChannelMap_8cxx.md#file-wdchannelmap.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef WDCHANNELMAP_H
#define WDCHANNELMAP_H

#include "SCChannelMap.h"
#include "TWChannelMap.h"
#include "CALOChannelMap.h"
#include "NeutronChannelMap.h"


// Overall WaveDAQ channel map that handles all the attached detectors
class WDChannelMap
{
protected:
    SCChannelMap _SCChannelMap;             
    TWChannelMap _TWChannelMap;             
    CALOChannelMap _CALOChannelMap;         
    NeutronChannelMap _NeutronChannelMap;   
    Bool_t _ChannelMapIsOk;                 
    void    ClearChannelMap();
    Bool_t  CheckMapConsistency();

public:
    WDChannelMap();
    Bool_t  LoadMap(std::string Filename);
    SCChannelMap*   GetSCChannelMap();
    TWChannelMap*   GetTWChannelMap();
    CALOChannelMap* GetCALOChannelMap();
    NeutronChannelMap*  GetNeutronChannelMap();
    Bool_t  IsSCMapLoaded();
    Bool_t  IsTWMapLoaded();
    Bool_t  IsCALOMapLoaded();
    Bool_t  IsNeutronMapLoaded();
};
#endif
```


-------------------------------

Updated on 2022-03-04 at 14:25:58 +0000
