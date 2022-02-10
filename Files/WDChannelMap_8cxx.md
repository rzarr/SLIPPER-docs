---
title: src/ChannelMap/WDChannelMap.cxx
summary: File containing all methods of Channel Map classes. 

---

# src/ChannelMap/WDChannelMap.cxx

File containing all methods of Channel Map classes.  [More...](#detailed-description)

## Detailed Description

File containing all methods of Channel Map classes. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "WDChannelMap.h"

WDChannelMap::WDChannelMap():
    _ChannelMapIsOk(false)
{
}


Bool_t WDChannelMap::LoadMap(std::string FileName)
{
    if (gSystem->AccessPathName(FileName.c_str()))
    {
        Error("LoadChannelMap()", "File %s doesn't exist", FileName.c_str());
        throw -1;
    }
    // reset channel map
    ClearChannelMap();
    // parse xml
    XmlParser x;
    x.ReadFile(FileName);

    // print some info about the channel map
    Message::DisplayMessageWithEmphasys(" Channel map ");
    Message::DisplayMessage(" Description: "+x.GetContentAsString("DESCRIPTION",x.GetMainNode()));
    Message::DisplayMessage(" Creation date: "+x.GetContentAsString("DATE",x.GetMainNode()));

    //Load SC channels
    _SCChannelMap.LoadMap(&x);

    // Load TW Bars
    _TWChannelMap.LoadMap(&x);

    //Load CALO Modules
    _CALOChannelMap.LoadMap(&x);

    //Load Neutron Detectors
    _NeutronChannelMap.LoadMap(&x);
    
    if( _SCChannelMap.IsLoaded() || _TWChannelMap.IsLoaded() ||
        _CALOChannelMap.IsLoaded() || _NeutronChannelMap.IsLoaded())
        _ChannelMapIsOk = CheckMapConsistency();
    
    return _ChannelMapIsOk;
}
 


Bool_t WDChannelMap::CheckMapConsistency()
{
    Bool_t MapOk = true;

    if( _SCChannelMap.IsLoaded() )
    {
        UShort_t SCBoard = _SCChannelMap.GetSCBoard();
        if( _TWChannelMap.IsBoardLoaded(SCBoard) )
        {
            Error("CheckMapConsistency()", "SC board (%d) found in TW channel map!", SCBoard);
            MapOk = false;
        }
        else if( _CALOChannelMap.IsBoardLoaded(SCBoard) )
        {
            Error("CheckMapConsistency()", "SC board (%d) found in CALO channel map!", SCBoard);
            MapOk = false;
        }
        else if( _NeutronChannelMap.IsBoardLoaded(SCBoard) )
        {
            Error("CheckMapConsistency()", "SC board (%d) found in Neutron channel map!", SCBoard);
            MapOk = false;
        }
    }

    if( MapOk && _TWChannelMap.IsLoaded() )
    {
        std::vector<UShort_t>* TWBoards = _TWChannelMap.GetListOfBoards();
        for(auto it = TWBoards->begin(); it != TWBoards->end(); ++it)
        {
            if( _CALOChannelMap.IsBoardLoaded(*it) )
            {
                Error("CheckMapConsistency()", "Found same board (%d) in TW and CALO!", *it);
                MapOk=false;
                break;
            }
            else if( _NeutronChannelMap.IsBoardLoaded(*it) )
            {
                Error("CheckMapConsistency()", "Found same board (%d) in TW and Neutrons", *it);
                MapOk = false;
                break;
            }
        }
    }

    if( MapOk && _CALOChannelMap.IsLoaded() )
    {
        std::vector<UShort_t>* CALOBoards = _CALOChannelMap.GetListOfBoards();
        for(auto it = CALOBoards->begin(); it != CALOBoards->end(); ++it)
        {
            if( _NeutronChannelMap.IsBoardLoaded(*it) )
            {
                Error("CheckMapConsistency()", "Found same board (%d) in CALO and Neutrons", *it);
                MapOk = false;
                break;
            }
        }
    }

    return MapOk;
}


void WDChannelMap::ClearChannelMap()
{
    _SCChannelMap.Clear();
    _TWChannelMap.Clear();
    _CALOChannelMap.Clear();
    _NeutronChannelMap.Clear();
}

SCChannelMap* WDChannelMap::GetSCChannelMap() { return &_SCChannelMap; }


TWChannelMap* WDChannelMap::GetTWChannelMap() { return &_TWChannelMap; }


CALOChannelMap* WDChannelMap::GetCALOChannelMap() { return &_CALOChannelMap; }


NeutronChannelMap* WDChannelMap::GetNeutronChannelMap() { return &_NeutronChannelMap; }


Bool_t WDChannelMap::IsSCMapLoaded() { return _SCChannelMap.IsLoaded(); }


Bool_t WDChannelMap::IsTWMapLoaded() { return _TWChannelMap.IsLoaded(); }


Bool_t WDChannelMap::IsCALOMapLoaded() { return _CALOChannelMap.IsLoaded(); }


Bool_t WDChannelMap::IsNeutronMapLoaded() { return _NeutronChannelMap.IsLoaded(); }
```


-------------------------------

Updated on 2022-02-10 at 11:12:25 +0000
