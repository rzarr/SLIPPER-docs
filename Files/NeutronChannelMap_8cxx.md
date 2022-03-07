---
title: src/ChannelMap/NeutronChannelMap.cxx
summary: File containing all methods of the Channel Map for Neutron detectors. 

---

# src/ChannelMap/NeutronChannelMap.cxx

File containing all methods of the Channel Map for Neutron detectors.  [More...](#detailed-description)

## Detailed Description

File containing all methods of the Channel Map for Neutron detectors. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "NeutronChannelMap.h"

NeutronChannelMap::NeutronChannelMap()
{
    BaseMap();
}

NeutronChannelMap::~NeutronChannelMap()
{
    Clear();
}


Bool_t NeutronChannelMap::LoadMap(XmlParser* x)
{
    Bool_t _IsMapLoaded = false;

    std::vector<XMLNodePointer_t> DetVector = x->GetChildNodesByName(x->GetMainNode(),"NEUTRON");
    for(std::vector<XMLNodePointer_t>::iterator it = DetVector.begin(); it != DetVector.end(); ++it)
    {
        std::string DetName = x->GetContentAsString("NAME", *it);
        UShort_t BoardSlow = (UShort_t)x->GetContentAsInt("BOARD_SLOW", *it);
        UShort_t BoardFast = (UShort_t)x->GetContentAsInt("BOARD_FAST", *it);
        std::vector<Int_t> ChSlow = x->GetContentAsIntVec("CHANNELS_SLOW", *it);
        std::vector<Int_t> GlobSlow = x->GetContentAsIntVec("GLOBAL_CH_SLOW", *it);
        std::vector<Int_t> ChFast = x->GetContentAsIntVec("CHANNELS_FAST", *it);
        std::vector<Int_t> GlobFast = x->GetContentAsIntVec("GLOBAL_CH_FAST", *it);

        AddDetector(DetName, BoardSlow, ChSlow, GlobSlow, BoardFast, ChFast, GlobFast);
    }

    if(_ListOfBoards.size() > 0 && CheckMapConsistency())
        _IsMapLoaded = true;

    return _IsMapLoaded;
}



void NeutronChannelMap::AddDetector(std::string DetName, UShort_t BoardSlow, std::vector<Int_t> ChSlow, std::vector<Int_t> GlobSlow, UShort_t BoardFast, std::vector<Int_t> ChFast, std::vector<Int_t> GlobFast)
{
    if( _BoardSlow == 0 )
    {
        _BoardSlow = BoardSlow;
        _ListOfBoards.push_back(_BoardSlow);
    }
    else if( _BoardSlow != BoardSlow)
    {
        Error("AddDetector()", "Detector %s loaded with slow board (%hu) different from the one already loaded (%hu)!", DetName.c_str(), BoardSlow, _BoardSlow);
        throw -1;
    }

    if( _BoardFast == 0 )
    {
        _BoardFast = BoardFast;
        _ListOfBoards.push_back(_BoardFast);
    }
    else if( _BoardFast != BoardFast)
    {
        Error("AddDetector()", "Detector %s loaded with fast board (%hu) different from the one already loaded (%hu)!", DetName.c_str(), BoardFast, _BoardFast);
        throw -1;
    }

    if( ChSlow.size() < 1 || ChFast.size() < 1 )
    {
        Error("AddDetector()", "Detector %s is missing either fast (%zu) or slow (%zu) channels!", DetName.c_str(), ChFast.size(), ChSlow.size());
        throw -1;
    }

    if(ChSlow.size() != GlobSlow.size() || ChFast.size() != GlobFast.size())
    {
        Error("AddDetector()", "Mismatch between slow/fast channel vectors (size=%zu/%zu) and global channel Ids (size=%zu/%zu) in detector %s!", ChSlow.size(), ChFast.size(), GlobSlow.size(), GlobFast.size(), DetName.c_str());
        throw -1;
    }

    for(int i=0; i< ChSlow.size(); ++i)
    {
        _SlowCh.push_back(ChSlow[i]);
        _BoardChToDetMap[std::make_pair(_BoardSlow, ChSlow[i])] = DetName;
        _BoardChToGlobMap[std::make_pair(_BoardSlow, ChSlow[i])] = GlobSlow[i];
        Message::DisplayMessage(Form("%s SLOW => BOARD %hu  CHANNEL %d  GLOBAL_SLOW %d", DetName.c_str(), BoardSlow, ChSlow[i], GlobSlow[i]));
    }
    for(int i=0; i< ChFast.size(); ++i)
    {
        _FastCh.push_back(ChFast[i]);
        _BoardChToDetMap[std::make_pair(_BoardFast, ChFast[i])] = DetName;
        _BoardChToGlobMap[std::make_pair(_BoardFast, ChFast[i])] = GlobFast[i];
        Message::DisplayMessage(Form("%s FAST => BOARD %hu  CHANNEL %d  GLOBAL_FAST %d", DetName.c_str(), BoardFast, ChFast[i], GlobFast[i]));
    }
}


Bool_t NeutronChannelMap::CheckMapConsistency()
{
    if(_ListOfBoards.size() < 1)
    {
        Warning("CheckMapConsistency()", "No Neutron detector board loaded in ChannelMap!");
        return false;
    }
    else if(_ListOfBoards.size() != 2)
    {
        Warning("CheckMapConsistency()", "Neutron map has more than 2 boards! Check and re-run for neutron data, removing map from output...");
        return false;
    }
    else if(_BoardSlow==0 || _BoardFast==0)
    {
        Warning("CheckMapConsistency()", "Either Slow (%hu) or Fast (%hu) board set incorrectly in neutron map! Check and re-run for neutron data, removing map from output...", _BoardSlow, _BoardFast);
        return false;
    }
    else if(_SlowCh.size() != NEUTRONSLOWCHANNELS || _FastCh.size() != NEUTRONFASTCHANNELS)
    {
        Warning("CheckMapConsistency()", "Number of Slow/Fast channels (%zu/%zu) different from expected (%d/%d)! Removing map from output...", _SlowCh.size(), _FastCh.size(), NEUTRONSLOWCHANNELS, NEUTRONFASTCHANNELS);
        return false;
    }

    if( _BoardChToDetMap.size() != _SlowCh.size() + _FastCh.size() || _BoardChToDetMap.size() != _BoardChToGlobMap.size())
    {
        Warning("CheckMapConsistency()", "Size of internal control maps not matching! Check if board-channel pairs are repeated inside neutron channel map. Removing map from output...");
        return false;
    }

    return true;
}


std::string NeutronChannelMap::GetDetFromBoardCh(std::pair<UShort_t, Int_t> BoardChPair)
{
    if( _BoardChToDetMap.find(BoardChPair) == _BoardChToDetMap.end() )
    {
        Error("GetDetFromBoardCh()", "Requested board-channel pair (%hu-%d) not found in channel map!", BoardChPair.first, BoardChPair.second);
        throw -1;
    }
    else
        return _BoardChToDetMap[BoardChPair];
}


Bool_t NeutronChannelMap::GetGlobFromBoardCh(std::pair<UShort_t, Int_t> BoardChPair, Int_t* globCh)
{
    if( _BoardChToGlobMap.find(BoardChPair) == _BoardChToGlobMap.end() )
    {
        // Warning("GetGlobFromBoardCh()", "Requested board-channel pair (%hu-%d) not found in channel map!", BoardChPair.first, BoardChPair.second);
        return false;
    }
    else
    {
        *globCh = _BoardChToGlobMap[BoardChPair];
        return true;
    }
}



std::vector<Int_t>* NeutronChannelMap::GetChSlow() { return &_SlowCh; }


std::vector<Int_t>* NeutronChannelMap::GetChFast() { return &_FastCh; }


UShort_t NeutronChannelMap::GetBoardSlow() { return _BoardSlow; }


UShort_t NeutronChannelMap::GetBoardFast() { return _BoardFast; }




void NeutronChannelMap::Clear()
{
    BaseMap::Clear();
    _SlowCh.clear();
    _FastCh.clear();
    _BoardChToDetMap.clear();
    _BoardChToGlobMap.clear();
}
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
