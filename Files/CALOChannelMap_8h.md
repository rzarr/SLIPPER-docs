---
title: src/ChannelMap/CALOChannelMap.h
summary: Header of CALOChannelMap.cxx. 

---

# src/ChannelMap/CALOChannelMap.h

Header of [CALOChannelMap.cxx](/Files/CALOChannelMap_8cxx.md#file-calochannelmap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CALOChannelMap](/Classes/classCALOChannelMap.md)** <br>Class that handles the Calorimeter Channel Map.  |

## Detailed Description

Header of [CALOChannelMap.cxx](/Files/CALOChannelMap_8cxx.md#file-calochannelmap.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef CALOCHANNELMAP_H
#define CALOCHANNELMAP_H

#include "BaseMap.h"

// Channel Map of the CALO
class CALOChannelMap : public BaseMap
{
protected:
    std::map<Int_t, std::vector<std::pair<UShort_t, Int_t>> > _ModToBoardChMap; 
    std::map<std::pair<UShort_t, Int_t>, Int_t> _BoardChToCrysMap;              
    
    void            AddModule(Int_t ModuleId, std::vector<UShort_t> Boards, std::vector<Int_t> Channels, std::vector<Int_t> Crystals);
    virtual Bool_t  CheckMapConsistency();
    
public:
    CALOChannelMap();
    virtual ~CALOChannelMap();
    Int_t                                   GetNumberOfCALOModules();
    Int_t                                   GetModuleFromCrys(Int_t CrysId);
    std::pair<UShort_t, Int_t>              GetBoardChFromCrys(Int_t CrysId);
    std::vector<std::pair<UShort_t, Int_t>> GetBoardChVec(Int_t ModuleId);
    Bool_t                                  GetCrystalId(UShort_t board, Int_t channel, Int_t* CrysId);
    
    virtual Bool_t  LoadMap(XmlParser* x);
    virtual void    Clear();
};


#endif
```


-------------------------------

Updated on 2022-02-10 at 11:57:30 +0000
