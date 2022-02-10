---
title: src/ChannelMap/SCChannelMap.cxx
summary: File with methods of Start Counter Channel Map. 

---

# src/ChannelMap/SCChannelMap.cxx

File with methods of Start Counter Channel Map.  [More...](#detailed-description)

## Detailed Description

File with methods of Start Counter Channel Map. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "SCChannelMap.h"

SCChannelMap::SCChannelMap()
{
    BaseMap();
}

SCChannelMap::~SCChannelMap()
{
    Clear();
}



Bool_t SCChannelMap::LoadMap(XmlParser* x)
{
    _IsMapLoaded = false;
    std::vector<XMLNodePointer_t> SCVector = x->GetChildNodesByName(x->GetMainNode(),"SC");
    if(SCVector.size() > 1)
    {
        Error("LoadMap()", "SC channel map is malformed! Expected max 1 board, found %zu!", SCVector.size());
        throw -1;
    }
    else if(SCVector.size() == 1)
    {
        UShort_t BoardId = (UShort_t)x->GetContentAsInt("BOARD_ID", SCVector.at(0));
        std::vector<Int_t> Channels = x->GetContentAsIntVec("CHANNELS", SCVector.at(0));
        AddSCBoard(BoardId, &Channels);
    }

    if(CheckMapConsistency())
        _IsMapLoaded = true;
    
    return _IsMapLoaded;
}


void SCChannelMap::AddSCBoard(UShort_t BoardId, std::vector<Int_t>* Channels)
{
    _ListOfBoards.push_back(BoardId);
    for(Int_t i=0; i<Channels->size(); ++i)
    {
        _Channels.push_back(Channels->at(i));
        Message::DisplayMessage(Form("SC => BOARD %hu CHANNEL %d", BoardId, _Channels.at(i)));
    }
    return;
}


Bool_t SCChannelMap::CheckMapConsistency()
{
    if(_ListOfBoards.size() == 0)
    {
        if(_Channels.size() == 0)
        {
            Message::DisplayWarning("CheckMapConsistency() --> SC not loaded in Channel Map!");
            Clear();
            return false;
        }
        else
        {
            Error("CheckMapConsistency()", "SC channel map is malformed! Found channels, but BoardId not set!");
            throw -1;
        }
    }
    else if(_ListOfBoards.size() > 1)
    {
        Error("CheckMapConsistency()", "SC channel map has more than one board!");
        throw -1;
    }
    else
    {
        if(_Channels.size() == NUMBEROFSCCHANNELS)
            return true;
        else
        {
            Error("CheckMapConsistency()", "SC channel map is malformed! Found %zu channels, expected %d!", _Channels.size(), NUMBEROFSCCHANNELS);
            throw -1;
        }
    }
}



UShort_t SCChannelMap::GetSCBoard() { return _ListOfBoards[0]; }


Int_t SCChannelMap::GetNumberOfChannels() { return _Channels.size(); }


std::vector<Int_t> SCChannelMap::GetSCChannels() { return _Channels; }


void SCChannelMap::Clear()
{
    BaseMap::Clear();
    _Channels.clear();
}
```


-------------------------------

Updated on 2022-02-10 at 11:57:30 +0000
