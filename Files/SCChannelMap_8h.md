---
title: src/ChannelMap/SCChannelMap.h
summary: Header of SCChannelMap.cxx. 

---

# src/ChannelMap/SCChannelMap.h

Header of [SCChannelMap.cxx](/Files/SCChannelMap_8cxx.md#file-scchannelmap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[SCChannelMap](/Classes/classSCChannelMap.md)** <br>Class that handles the Start Counter Channel Map.  |

## Detailed Description

Header of [SCChannelMap.cxx](/Files/SCChannelMap_8cxx.md#file-scchannelmap.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef SCCHANNELMAP_H
#define SCCHANNELMAP_H

#include "BaseMap.h"

//Channel Map of the SC detector
class SCChannelMap : public BaseMap
{
protected:
    std::vector<Int_t> _Channels;           
    virtual Bool_t  CheckMapConsistency();
    
public:
    SCChannelMap();
    virtual ~SCChannelMap();
    UShort_t            GetSCBoard();
    Int_t               GetNumberOfChannels();
    std::vector<Int_t>  GetSCChannels();
    void                AddSCBoard(UShort_t BoardId, std::vector<Int_t>* Channels);
    virtual Bool_t      LoadMap(XmlParser* x);
    virtual void        Clear();
};


#endif
```


-------------------------------

Updated on 2021-12-29 at 15:21:51 +0000
