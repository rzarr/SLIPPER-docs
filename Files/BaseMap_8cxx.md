---
title: src/ChannelMap/BaseMap.cxx
summary: File containing the base class for detector Channel Map. 

---

# src/ChannelMap/BaseMap.cxx

File containing the base class for detector Channel Map.  [More...](#detailed-description)

## Detailed Description

File containing the base class for detector Channel Map. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "BaseMap.h"

BaseMap::BaseMap()
{
    _IsMapLoaded = false;
    Clear();
}

BaseMap::~BaseMap()
{
    Clear();
}

std::vector<UShort_t>* BaseMap::GetListOfBoards() { return &_ListOfBoards; }

Bool_t BaseMap::IsBoardLoaded(UShort_t BoardId)
{
    if( _ListOfBoards.size() == 0 || std::find(_ListOfBoards.begin(), _ListOfBoards.end(), BoardId) == _ListOfBoards.end() )
        return false;
    else
        return true;
}


Bool_t BaseMap::IsLoaded() { return _IsMapLoaded; }


void BaseMap::Clear() { _ListOfBoards.clear(); }
```


-------------------------------

Updated on 2021-12-30 at 11:00:09 +0000
