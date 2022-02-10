---
title: src/ChannelMap/NeutronChannelMap.h
summary: Header of NeutronChannelMap.cxx. 

---

# src/ChannelMap/NeutronChannelMap.h

Header of [NeutronChannelMap.cxx](/Files/NeutronChannelMap_8cxx.md#file-neutronchannelmap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[NeutronChannelMap](/Classes/classNeutronChannelMap.md)** <br>Class that handles all the WaveDREAM boards-channels connected to Neutron detectors.  |

## Detailed Description

Header of [NeutronChannelMap.cxx](/Files/NeutronChannelMap_8cxx.md#file-neutronchannelmap.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef NEUTRONCHANNELMAP_H
#define NEUTRONCHANNELMAP_H

#include "BaseMap.h"

// Channel Map of the Neutron detectors
class NeutronChannelMap : public BaseMap
{
protected:
    UShort_t _BoardSlow = 0;                                                
    UShort_t _BoardFast = 0;                                                
    std::vector<Int_t> _SlowCh;                                             
    std::vector<Int_t> _FastCh;                                             
    std::map<std::pair<UShort_t, Int_t>, std::string> _BoardChToDetMap;     
    std::map<std::pair<UShort_t, Int_t>, Int_t> _BoardChToGlobMap;          
    
    void    AddDetector(std::string DetName, UShort_t BoardSlow, std::vector<Int_t> ChSlow, std::vector<Int_t> GlobSlow, UShort_t BoardFast, std::vector<Int_t> ChFast, std::vector<Int_t> GlobFast);
    virtual Bool_t  CheckMapConsistency();
    
public:
    NeutronChannelMap();
    virtual ~NeutronChannelMap();
    std::vector<Int_t>* GetChSlow();
    std::vector<Int_t>* GetChFast();
    UShort_t    GetBoardSlow();
    UShort_t    GetBoardFast();

    std::string GetDetFromBoardCh(std::pair<UShort_t, Int_t> BoardChPair);
    Bool_t      GetGlobFromBoardCh(std::pair<UShort_t, Int_t> BoardChPair, Int_t* globCh);

    virtual Bool_t  LoadMap(XmlParser* x);
    virtual void    Clear();
};

#endif
```


-------------------------------

Updated on 2022-02-10 at 12:05:07 +0000
