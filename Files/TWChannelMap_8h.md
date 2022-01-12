---
title: src/ChannelMap/TWChannelMap.h
summary: Header of TWChannelMap.cxx. 

---

# src/ChannelMap/TWChannelMap.h

Header of [TWChannelMap.cxx](/Files/TWChannelMap_8cxx.md#file-twchannelmap.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[TWChannelMap](/Classes/classTWChannelMap.md)** <br>Class that handles the TOF-Wall Channel Map.  |

## Types

|                | Name           |
| -------------- | -------------- |
| typedef std::map< Int_t, [TLayer](/Files/Parameters_8h.md#enum-tlayer) > | **[TMapBarIdLayerId](/Files/TWChannelMap_8h.md#typedef-tmapbaridlayerid)**  |
| typedef std::map< std::pair< UShort_t, Int_t >, Int_t > | **[TBoardChannelToGlobalMap](/Files/TWChannelMap_8h.md#typedef-tboardchanneltoglobalmap)**  |
| typedef std::map< Int_t, std::pair< Int_t, Char_t > > | **[TGlobalToBarChIDpairMap](/Files/TWChannelMap_8h.md#typedef-tglobaltobarchidpairmap)**  |

## Detailed Description

Header of [TWChannelMap.cxx](/Files/TWChannelMap_8cxx.md#file-twchannelmap.cxx). 

**Author**: R. Zarrella 
## Types Documentation

### typedef TMapBarIdLayerId

```cpp
typedef std::map<Int_t,TLayer> TMapBarIdLayerId;
```


### typedef TBoardChannelToGlobalMap

```cpp
typedef std::map<std::pair<UShort_t, Int_t>, Int_t> TBoardChannelToGlobalMap;
```


### typedef TGlobalToBarChIDpairMap

```cpp
typedef std::map<Int_t, std::pair<Int_t, Char_t> > TGlobalToBarChIDpairMap;
```





## Source code

```cpp

#ifndef TWCHANNELMAP_H
#define TWCHANNELMAP_H

#include "BaseMap.h"

typedef std::map<Int_t,TLayer> TMapBarIdLayerId;
typedef std::map<std::pair<UShort_t, Int_t>, Int_t> TBoardChannelToGlobalMap;
typedef std::map<Int_t, std::pair<Int_t, Char_t>> TGlobalToBarChIDpairMap;


// Channel Map of the TW detector
class TWChannelMap : public BaseMap
{
protected:
    TMapBarIdLayerId _BarLayerMap;                      
    TBoardChannelToGlobalMap _BoardChannelToGlobalMap;  
    TGlobalToBarChIDpairMap _GlobalToBarChIDpairMap;    

    void    AddBar(Int_t BarId, TLayer Layer, UShort_t BoardId, Int_t ChannelA, Int_t ChannelB, Int_t GlobalChannelA, Int_t GlobalChannelB);
    virtual Bool_t  CheckMapConsistency();

public:
    TWChannelMap();
    virtual ~TWChannelMap();
    TBoardChannelToGlobalMap    GetBoardChannelToGlobalMap();
    TGlobalToBarChIDpairMap GetGlobalToBarChIDpairMap();
    TMapBarIdLayerId    GetBarLayerMap();
    Int_t   GetGlobalFromBoardChannelPair(std::pair<UShort_t, Int_t> p);
    Int_t   GetNumberOfTWBars();
    virtual Bool_t  LoadMap(XmlParser* x);
    virtual void    Clear();
};


#endif
```


-------------------------------

Updated on 2022-01-12 at 16:47:44 +0000
