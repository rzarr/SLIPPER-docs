---
title: src/ChannelMap/TWChannelMap.cxx
summary: File containing all methods of TOF-Wall Channel Map. 

---

# src/ChannelMap/TWChannelMap.cxx

File containing all methods of TOF-Wall Channel Map.  [More...](#detailed-description)

## Detailed Description

File containing all methods of TOF-Wall Channel Map. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "TWChannelMap.h"

TWChannelMap::TWChannelMap()
{
    BaseMap();
}

TWChannelMap::~TWChannelMap()
{
    Clear();
}


Bool_t TWChannelMap::LoadMap(XmlParser* x)
{
    _IsMapLoaded = false;

    //Create a vector with "BAR" entries
    std::vector<XMLNodePointer_t> BarVector=x->GetChildNodesByName(x->GetMainNode(),"BAR");

    //Load TW Bars
    Int_t BarId, ChannelA, ChannelB,  GlobalChannelA, GlobalChannelB;
    UShort_t BoardId;
    TLayer Layer;
    for (std::vector<XMLNodePointer_t>::iterator it=BarVector.begin();it!=BarVector.end();++it)
    {
        BarId = x->GetContentAsInt("BAR_ID",*it);
        Layer = (TLayer)x->GetContentAsInt("LAYER",*it);
        BoardId = (UShort_t)x->GetContentAsInt("BOARD_ID",*it);
        ChannelA = x->GetContentAsInt("CHANNEL_A",*it);
        ChannelB = x->GetContentAsInt("CHANNEL_B",*it);
        GlobalChannelA = x->GetContentAsInt("GLOBAL_CHANNEL_IDA", *it);
        GlobalChannelB = x->GetContentAsInt("GLOBAL_CHANNEL_IDB", *it);

        AddBar(BarId, Layer, BoardId, ChannelA, ChannelB, GlobalChannelA, GlobalChannelB);

        if(std::find(_ListOfBoards.begin(), _ListOfBoards.end(), BoardId) == _ListOfBoards.end())
            _ListOfBoards.push_back(BoardId);
    }
    //Check if boards where found and the map is consistent
    if(_ListOfBoards.size() > 0 && CheckMapConsistency())
        _IsMapLoaded = true;

    return _IsMapLoaded;
}


void TWChannelMap::AddBar(Int_t BarId, TLayer Layer, UShort_t BoardId, Int_t ChannelA, Int_t ChannelB, Int_t GlobalChannelA, Int_t GlobalChannelB)
{
    // the same bar should not appear twice
    if (_BarLayerMap.count(BarId)!=0)
    {
        Error("LoadChannelMap()", "Channel Map is malformed: BAR %d appears twice", BarId);
    }
    
    std::pair<Int_t, Int_t> GlobalPair;
    std::pair<UShort_t, Int_t> BoardChannelAPair, BoardChannelBPair;
    
    BoardChannelAPair = std::make_pair(BoardId, ChannelA);
    BoardChannelBPair = std::make_pair(BoardId, ChannelB);
    GlobalPair = std::make_pair(GlobalChannelA, GlobalChannelB);

    _BoardChannelToGlobalMap[BoardChannelAPair] = GlobalChannelA;
    _BoardChannelToGlobalMap[BoardChannelBPair] = GlobalChannelB;
    _GlobalToBarChIDpairMap[GlobalChannelA] = std::make_pair(BarId, 'A');
    _GlobalToBarChIDpairMap[GlobalChannelB] = std::make_pair(BarId, 'B');
    _BarLayerMap[BarId]=Layer;
    Message::DisplayMessage(Form("TW => BAR_ID %d BOARD ID %d Channel A %d Channel B %d Layer Id %d Global A %d Global B %d", BarId, BoardId, ChannelA, ChannelB, Layer, GlobalChannelA, GlobalChannelB));
}


Bool_t TWChannelMap::CheckMapConsistency()
{
    if(_BarLayerMap.size() <= 0 || _BoardChannelToGlobalMap.size() <= 0 || _GlobalToBarChIDpairMap.size() <= 0)
    {
        Message::DisplayWarning("CheckMapConsistency() --> No TW Channel Map loaded!");
        Clear();
        return false;
    }

    // check if the same combination board,channel appears twice in the map
    std::map<std::pair<Int_t,Int_t>, Int_t> ChannelOccurrenceMap;
    for (auto it = _BoardChannelToGlobalMap.begin(); it != _BoardChannelToGlobalMap.end(); ++it)
    {
        if (ChannelOccurrenceMap.count(it->first) != 0)
        {
            Error("CheckMapConsistency()", "Combination Board %d Channel %d appears twice in the TW channel map", (it->first).first, (it->first).second);
            throw -1;
        }
        ChannelOccurrenceMap[it->first]=1;
    }

    // check if the number of bar found is bigger than NUMBEROFTWBARS found in Parameters.h
    if (_BarLayerMap.size() > NUMBEROFTWBARS)
    {
        Error("CheckMapConsistency()", "Too many bars in channel map. Found %lu expected %d", _BarLayerMap.size(), NUMBEROFTWBARS);
        throw -1;
    }

    return true;
}



TBoardChannelToGlobalMap TWChannelMap::GetBoardChannelToGlobalMap() { return _BoardChannelToGlobalMap; }

TGlobalToBarChIDpairMap TWChannelMap::GetGlobalToBarChIDpairMap() { return _GlobalToBarChIDpairMap; }

TMapBarIdLayerId TWChannelMap::GetBarLayerMap() { return _BarLayerMap; }

Int_t TWChannelMap::GetGlobalFromBoardChannelPair(std::pair<UShort_t, Int_t> p) { return _BoardChannelToGlobalMap[p];}

Int_t TWChannelMap::GetNumberOfTWBars() { return _BarLayerMap.size(); }


void TWChannelMap::Clear()
{
    BaseMap::Clear();
    _BarLayerMap.clear();
    _BoardChannelToGlobalMap.clear();
    _GlobalToBarChIDpairMap.clear();
}
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
