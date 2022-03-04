---
title: src/ChannelMap/CALOChannelMap.cxx
summary: File containing all methods of the Calorimeter Channel Map. 

---

# src/ChannelMap/CALOChannelMap.cxx

File containing all methods of the Calorimeter Channel Map.  [More...](#detailed-description)

## Detailed Description

File containing all methods of the Calorimeter Channel Map. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "CALOChannelMap.h"

CALOChannelMap::CALOChannelMap()
{
    BaseMap();
}

CALOChannelMap::~CALOChannelMap()
{
    Clear();
}


Bool_t CALOChannelMap::LoadMap(XmlParser* x)
{
    Bool_t MapLoaded = false;

    std::vector<XMLNodePointer_t> ModuleVector = x->GetChildNodesByName(x->GetMainNode(),"MODULE");
    for(std::vector<XMLNodePointer_t>::iterator it = ModuleVector.begin(); it != ModuleVector.end(); ++it)
    {
        Int_t ModuleId = x->GetContentAsInt("MODULE_ID", *it);
        std::vector<UShort_t> Boards = x->GetContentAsShortVec("BOARD_ID", *it);
        std::vector<Int_t> Channels = x->GetContentAsIntVec("CHANNELS", *it);
        std::vector<Int_t> Crystals = x->GetContentAsIntVec("CRYSTAL_ID", *it);

        if(Crystals.size() != Channels.size())
        {
            Error("LoadChannelMap()", "CALO Channel Map is malformed! In module %d, found %zu channels and %zu crystals!", ModuleId, Channels.size(), Crystals.size());
            throw -1;
        }

        AddModule(ModuleId, Boards, Channels, Crystals);

        for(int i = 0; i < Boards.size(); ++i )
        {
            if( std::find(_ListOfBoards.begin(), _ListOfBoards.end(), Boards[i]) == _ListOfBoards.end() )
                _ListOfBoards.push_back(Boards[i]);
        }
    }

    if(_ListOfBoards.size() > 0 && CheckMapConsistency())
        MapLoaded = true;

    return MapLoaded;
}


void CALOChannelMap::AddModule(Int_t ModuleId, std::vector<UShort_t> Boards, std::vector<Int_t> Channels, std::vector<Int_t> Crystals)
{
    if(_ModToBoardChMap.find(ModuleId) != _ModToBoardChMap.end())
    {
        Error("AddModule()", "Module %d already found in CALO Channel Map!", ModuleId);
        throw -1;
    }

    UShort_t board1, board2;
    board1 = Boards.at(0);

    if( Boards.size() == 2 )
        board2 = Boards.at(1);
    else
        board2 = board1;

    std::vector<Int_t>::iterator itCh, itCrys;
    UShort_t board = board1;
    for(itCh = Channels.begin(), itCrys = Crystals.begin(); itCh != Channels.end() && itCrys != Crystals.end(); itCh++, itCrys++)
    {
        std::pair<UShort_t, Int_t> BoardCh(board, *itCh);
        if( _BoardChToCrysMap.find(BoardCh) != _BoardChToCrysMap.end() )
        {
            Error("AddModule()", "Board-channel pair (%hu, %d) already loaded in CALO Channel Map!", board, *itCh);
            throw -1;
        }
        _ModToBoardChMap[ModuleId].push_back( BoardCh );
        _BoardChToCrysMap[BoardCh] = *itCrys;

        Message::DisplayMessage(Form("CALO => MODULE_ID %d BOARD ID %hu Channel %d Crystal %d ", ModuleId, board, *itCh, *itCrys));

        if( *itCh == 15 )
            board = board2;
    }

    return;
}


Int_t CALOChannelMap::GetModuleFromCrys(Int_t CrysId)
{
    bool found = false;
    Int_t ModId;
    std::pair<UShort_t, Int_t> BoardChPair = GetBoardChFromCrys(CrysId);
    
    std::map<Int_t, std::vector<std::pair<UShort_t, Int_t>> >::iterator it;
    for(it = _ModToBoardChMap.begin(); it != _ModToBoardChMap.end(); ++it)
    {
        if(std::find(it->second.begin(), it->second.end(), BoardChPair) != it->second.end())
        {
            ModId = it->first;
            found = true;
            break;
        }
    }

    if(!found)
    {
        Error("GetModuleFromCrys()", "Board-channel pair (%hu, %d) not found in Channel Map!", BoardChPair.first, BoardChPair.second);
        throw -1;
    }
    else
        return ModId;
}


std::vector<std::pair<UShort_t, Int_t>> CALOChannelMap::GetBoardChVec(Int_t ModuleId)
{
    if( _ModToBoardChMap.find(ModuleId) == _ModToBoardChMap.end() )
    {
        Error("GetBoardChVec()", "Requested a CALO module (%d) not found in ChannelMap!", ModuleId);
        throw -1;
    }
    else
        return _ModToBoardChMap.at( ModuleId );
}


Bool_t CALOChannelMap::GetCrystalId(UShort_t board, Int_t channel, Int_t* CrysId)
{
    if( _BoardChToCrysMap.find( std::make_pair(board, channel) ) != _BoardChToCrysMap.end() )
    {
        *CrysId = _BoardChToCrysMap.at( std::make_pair(board, channel) );
        return true;
    }
    else
    {
        Warning("GetCrystalId()", "Requested CALO Crystal in board %d, channel %d not found in ChannelMap! => Skipping...", board, channel);
        return false;
    }
}


std::pair<UShort_t, Int_t> CALOChannelMap::GetBoardChFromCrys(Int_t CrysId)
{
    bool found = false;
    std::pair<UShort_t, Int_t> BoardChPair;
    if(CrysId > NUMBEROFCRYSTALS)
    {
        Error("GetBoardChFromCrys()", "CrystalId %d exceeds max number of crystals!", CrysId);
        throw -1;
    }

    std::map<std::pair<UShort_t, Int_t>, Int_t>::iterator it;
    for(it = _BoardChToCrysMap.begin(); it != _BoardChToCrysMap.end(); ++it)
    {
        if(it->second == CrysId)
        {
            BoardChPair = it->first;
            found = true;
            break;
        }
    }

    if(!found)
    {
        Error("GetBoardChFromCrys()", "Crystal %d not found in Channel Map!", CrysId);
        throw -1;
    }
    else
        return BoardChPair;
}


Bool_t CALOChannelMap::CheckMapConsistency()
{
    if(_ModToBoardChMap.size() == 0)
    {
        Message::DisplayWarning("CheckMapConsistency() --> No CALO Module Loaded!!");
        Clear();
        return false;
    }

    if(_ListOfBoards.size() == 0)
    {
        Message::DisplayWarning("CheckMapConsistency() --> No CALO Board loaded!!");
        Clear();
        return false;
    }

    if(_BoardChToCrysMap.size() == 0)
    {
        Message::DisplayWarning("CheckMapConsistency() --> No CALO Board-Channel pair loaded!!");
        Clear();
        return false;
    }

    // check if the same combination board,channel appears twice in the map
    std::map<std::pair<UShort_t,Int_t>, Int_t> ChannelOccurrenceMap;
    for (auto it = _BoardChToCrysMap.begin(); it != _BoardChToCrysMap.end(); ++it)
    {
        if (ChannelOccurrenceMap.count(it->first)!=0)
        {
            Error("CheckMapConsistency()", "Combination Board %hu Channel %d appears twice in the CALO channel map", (it->first).first, (it->first).second);
            throw -1;
        }
        ChannelOccurrenceMap[it->first] = 1;
    }

    // check if the number of bar found is bigger than NUMBEROFTWBARS found in Parameters.h
    if (_ModToBoardChMap.size() > NUMBEROFCALOMODULES)
    {
        Error("CheckMapConsistency()", "Wrong number of CALO modules in channel map. Found %zu expected %d", _ModToBoardChMap.size(), NUMBEROFCALOMODULES);
        throw -1;
    }

    return true;
}


Int_t CALOChannelMap::GetNumberOfCALOModules() { return _ModToBoardChMap.size(); }


void CALOChannelMap::Clear()
{
    BaseMap::Clear();
    _ModToBoardChMap.clear();
    _BoardChToCrysMap.clear();
}
```


-------------------------------

Updated on 2022-03-04 at 14:25:58 +0000
