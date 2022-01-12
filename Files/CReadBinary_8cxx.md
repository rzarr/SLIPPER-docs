---
title: src/CReadBinary.cxx
summary: File containing all methods of CReadBinary class. 

---

# src/CReadBinary.cxx

File containing all methods of [CReadBinary](/Classes/classCReadBinary.md) class.  [More...](#detailed-description)

## Detailed Description

File containing all methods of [CReadBinary](/Classes/classCReadBinary.md) class. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "CReadBinary.h"

/*-----------------------------------------------------------------------------*/

CReadBinary::CReadBinary(std::vector<CWaveFormContainer*>* wdb_data_ptr, std::vector<TCBDATA*>* tcb_data_ptr, std::map<UShort_t, Int_t>* _WDBIdtoIdMap, std::map<UShort_t, Int_t>* ActiveBoards, Float_t* TDCTime, std::map<int, int>* TDCchMap, TH2F* hTGEN_MB, TH2F* hTGEN_frag, TH1I* hTriggerPattern, TH1I* hTriggerRates) :
    _IsFragTriggerOn(false)
{
    Nev = 0;
    
    _data_wdb = wdb_data_ptr;
    _data_tcb = tcb_data_ptr;
    _wdb_index = _WDBIdtoIdMap;
    _ActiveBoards = ActiveBoards;

    _TDCTime = TDCTime;
    _TDCchMap = TDCchMap;
    _hTGEN_MB = hTGEN_MB;
    _hTGEN_frag = hTGEN_frag;
    _hTriggerPattern = hTriggerPattern;
    _hTriggerRates = hTriggerRates;
};


CReadBinary::~CReadBinary()
{
    _bins.clear();
    
    _data_wdb->clear();
    delete _data_wdb;
    
    _data_tcb->clear();
    delete _data_tcb;
}


void CReadBinary::CheckBinaryFileHeader(FILE* f)
{
    if (f == NULL)
    {
        Error("CheckBinaryFileHeader()", "Input binary file not found");
        throw -1;
    }
    
    FHEADER  fh;
    // read input file header
    fread(&fh, sizeof(fh), 1, f);
    if (fh.tag[0] != 'W' || fh.tag[1] != 'D' || fh.tag[2] != 'Q')
    {
        Error("CheckBinaryFileHeader()", "Found invalid file header in input file, aborting.\n");
        throw -1;
    }

    if (fh.version != '0')
    {
        Error("CheckBinaryFileHeader()", "Found invalid file version \'%c\' in input binary file, should be \'8\', aborting.\n", fh.version);
        throw -1;
    }

}


void CReadBinary::LoadWaveDreamTimeCalibration(FILE* f)
{
    // read time header
    fread(&th, sizeof(th), 1, f);
    if (memcmp(th.time_header, "TIME", 4) != 0)
    {
        Error("LoadWaveDreamTimeCalibration()", "Invalid time header in input binary file, aborting.");
        throw -1;
    }

    //cycle on boards and load the time calibration
    int i;
    for (int b = 0 ; !feof(f) ; b++)
    {
        // read board header and resize data vectors
        fread(&bh, sizeof(bh), 1, f);

        if (memcmp(bh.bn, "B#", 2) == 0)
        {
            (*_wdb_index)[bh.board_serial_number] = _wdb_index->size();
            _bins.resize(_bins.size() + 1);
            
            (*_data_wdb).push_back(new CWaveFormContainer());
            
            //define board index just for shorthand lines
            UShort_t board_id = _wdb_index->at(bh.board_serial_number);

            //save the board serial number
            printf("Found time calibration for board #%d\n", bh.board_serial_number);

            // read time bin widths
            memset(_bins[board_id].bin_width, 0, sizeof(WDBBIN));
            for (chn=0 ; chn<18 ; chn++)
            {
                fread(&ch, sizeof(ch), 1, f);
                if (ch.c[0] != 'C')
                {
                    // event header found
                    fseek(f, -4, SEEK_CUR);
                    Warning("LoadWaveDreamTimeCalibration()", "Time calibration loading ended at channel::%d of board::%hu", chn, bh.board_serial_number);
                    return;
                }
                i = (ch.cn[1] - '0')*10 + ch.cn[2] - '0';

                //read the time calibration and save bin widths for each channel
                garbage=fread(_bins[board_id].bin_width[i], sizeof(float), 1024, f);
            }
        } //end of WDB time cal
        else if (memcmp(bh.bn, "T#", 2) == 0)
        {
            (*_data_tcb).push_back(new TCBDATA());
            _tcb_index[bh.board_serial_number] = _tcb_index.size();

            printf("Found data for TCB %d\n", bh.board_serial_number);
        } //end of TCB
        else
        {
            // probably event header found
            fseek(f, -4, SEEK_CUR);
            if(_bins.size() < 1)
            {
                Error("LoadWaveDreamTimeCalibration()", "Size of time calibration vector (%zu) is non positive! Event header found before time calibration!", _bins.size());
                throw -1;
            }
            return;
        }

        bh.bn[0] = 'Z'; bh.bn[1] = '&'; //set to nonsense values to avoid spurious reads
    }
}



Int_t CReadBinary::DecodeEvent(FILE* f)
{
    if(Nev % 1000 == 0){printf("Events decoded: %d\n", Nev);}

    // read event header
    int garbage = fread(&eh, sizeof(eh), 1, f);

    if (garbage < 1 || memcmp(eh.event_header, "EHDR", 4) != 0)
    {
        Error("DecodeEvent()", "Event header different wrt the expected one -> %s", eh.event_header);
        return 0;
    }

    // clear WDB and TCB data
    std::map<UShort_t, Int_t>::iterator itActive;
    for(itActive = _ActiveBoards->begin(); itActive != _ActiveBoards->end(); ++itActive)
        _data_wdb->at(itActive->second)->data.clear();
    _ActiveBoards->clear();

    std::vector<TCBDATA*>::iterator itTCB;
    for (itTCB = _data_tcb->begin(); itTCB != _data_tcb->end(); ++itTCB)
        (*itTCB)->clear();

    //loop over boards to read file
    for (b=0 ; !feof(f) ; b++)
    {
        // read board header
        garbage= fread(&bh, sizeof(bh), 1, f);

        //read WDBs
        if (memcmp(bh.bn, "B#", 2) == 0)    ReadWDBEvent(f);

        //read TCBs
        else if( memcmp(bh.bn, "T#", 2) == 0 )  ReadTCBEvent(f);

        //probably next event -> rewind
        else
        {
            fseek(f, -4, SEEK_CUR);
            break;
        }
        bh.bn[0] = 'Z'; bh.bn[1] = '&'; //set to nonsense values to avoid spurious reads
    } //end loop on boards

    // AlignTriggerCell();
    AlignSignalsRight();

    if(_hTGEN_frag != nullptr && _IsFragTriggerOn)  FillHistoTGEN(_hTGEN_frag);
    else if(_hTGEN_MB != nullptr )  FillHistoTGEN(_hTGEN_MB);

    Nev++;
    return eh.trigger_type;
}



void CReadBinary::ReadWDBEvent(FILE* f)
{
    //read DRS board header
    garbage = fread(&drsbh, sizeof(drsbh), 1, f);

    int board_id = _wdb_index->at(bh.board_serial_number);
    
    // reach channel data
    std::vector<int> ChVec;
    for (chn=0 ; !feof(f) ; chn++)
    {
        // read channel header
        garbage = fread(&ch, sizeof(ch), 1, f);
        if (ch.c[0] != 'C' && ch.c[0] != 'A' && (ch.c[0] != 'T' || ch.cn[0] == '#') && ch.c[0] != 'S')
        {
            // event header found
            fseek(f, -4, SEEK_CUR);
            break;
        }
        if( _ActiveBoards->find(bh.board_serial_number) == _ActiveBoards->end() )
            (*_ActiveBoards)[bh.board_serial_number] = board_id;

        chn_index = (ch.cn[1] - '0')*10 + ch.cn[2] - '0';
        _data_wdb->at(board_id)->data.ch_on[chn_index] = true;
        ChVec.push_back(chn_index);
        
        if(ch.c[0] == 'C')
        {
            // read trigger cell and frontend settings
            garbage = fread(drsch+chn_index, sizeof(drsch[0]), 1, f);
            (*_data_wdb)[board_id]->data.trigcell[chn_index] = drsch[chn_index].trigger_cell;

            garbage=fread(voltage, sizeof(short), 1024, f);
            Float_t timebin = 0.;
            Float_t* t_ptr = &(*_data_wdb)[board_id]->data.t[chn_index][0];
            Float_t* w_ptr = &(*_data_wdb)[board_id]->data.w[chn_index][0];
            for (int i=0 ; i < WAVEFORMBINS ; i++) 
            {
                *w_ptr = (voltage[i] / 65536. + drsbh.board_range/1000. - 0.5);
                // calculate time for this cell
                *t_ptr = timebin;
                timebin += _bins[board_id].bin_width[chn_index][(i + drsch[chn_index].trigger_cell) % WAVEFORMBINS];
                ++w_ptr;
                ++t_ptr;
            }

            CheckRangeOverflow( &(*_data_wdb)[board_id]->data.w[chn_index][1]);
        }
        //ADC
        else if(ch.c[0] == 'A')
        {
            garbage= fread((*_data_wdb)[board_id]->data.adc_waveform[chn_index], sizeof(short), 2048, f);
        }
        else if(ch.c[0] == 'T')
        {
            //TDC
            if(ch.cn[0] == '0')
            {
                garbage=fread((*_data_wdb)[board_id]->data.tdc_waveform[chn_index], sizeof(char), 512, f);
            }
            //TRG
            else if(ch.cn[0] == 'R')
            {
                garbage= fread((*_data_wdb)[board_id]->data.trigger_data, sizeof(long), 512, f);
            }
        }
        else if(ch.c[0] == 'S') {
            //Scaler
            garbage=fread(scaler_data, sizeof(long), 18, f);
            garbage=fread(&scaler_time, sizeof(long), 1, f);
            for (int i=0 ; i<18 ; i++) {
                (*_data_wdb)[board_id]->data.scaler[i] = (Float_t) (scaler_data[i]-scaler_data_old[i])/(scaler_time-scaler_time_old)/12.5e-9;
                scaler_data_old[i] = scaler_data[i];
            }
            scaler_time_old = scaler_time;
        }
    }// end for channels 
}


void CReadBinary::CheckRangeOverflow(Float_t* w_ptr)
{
    for (int i=1 ; i < WAVEFORMBINS ; i++) 
    {
        if( fabs(*w_ptr - *(w_ptr-1)) > 0.5 )
        {
            if( *w_ptr > *(w_ptr - 1) )
                *w_ptr -= 1.;
            
            else if( *w_ptr < *(w_ptr - 1) )
                *w_ptr += 1.;
            }

        ++w_ptr;
    }
}


void CReadBinary::ReadTCBEvent(FILE* f)
{
    // printf("Found data for TCB %d\n", bh.board_serial_number);
    
    if(_tcb_index.find(bh.board_serial_number) == _tcb_index.end())
    {
        _tcb_index[bh.board_serial_number] = _tcb_index.size();
        (*_data_tcb).push_back(new TCBDATA());
    }
    int board_id = _tcb_index[bh.board_serial_number];
    unsigned int nBanks;
    fread(&nBanks, sizeof(nBanks), 1, f);
    
    // if(n<10){printf("Found %d banks for TCB %d\n", nBanks, bh.board_serial_number);}
    
    for(unsigned int iBank=0; iBank<nBanks; ++iBank)
    {
        char bankName[4];
        unsigned int bankSize;
        fread(&bankName, sizeof(char), 4, f);
        fread(&bankSize, sizeof(bankSize), 1, f);
        // printf("tcb %d with id %d: got bank %c%c%c%c size:%u\n", bh.board_serial_number, board_id, bankName[0], bankName[1], bankName[2], bankName[3], bankSize);

        unsigned int temp[1000];
        fread(&temp, sizeof(unsigned int), bankSize, f);


        if(bankName[0] == 'I' && bankName[1] == 'N')
        {
            int serdesNumber = (bankName[2] - '0')*10 + (bankName[3]-'0');
            for(int i=0; i<128; ++i)
            {
                uint64_t val = temp[129 + (i + temp[0])%128];

                val = val << 32;
                val |= temp[1 + (i + temp[0])%128];
                (*_data_tcb)[board_id]->in_waveform[serdesNumber][i] = val;
            }
        }
        else if (bankName[0]=='T' && bankName[1]=='G' && bankName[2]=='E' && bankName[3]=='N')
        {
            for(unsigned int ibin = 0; ibin<32; ibin++)
                _TriggerGenerationBin[(ibin + 32 - temp[0]) % 32] = temp[ibin+1]; // bit 31:0

            for(unsigned int ibin = 0; ibin<32; ibin++)
                _TriggerGenerationBin[(ibin + 32 - temp[0]) % 32] = (((uint64_t)temp[ibin+33])<<32) | _TriggerGenerationBin[(ibin + 32 - temp[0]) % 32]; // bit 63:32
        }
        else if (bankName[0]=='T' && bankName[1]=='R' && bankName[2]=='G' && bankName[3]=='I')
        {
            // for(int i=0; i<bankSize; ++i){printf("%4d:%08x\t%u\n", i, temp[i], temp[i]);}
            uint64_t TriggerPattern = ((uint64_t)temp[1]) | (((uint64_t)temp[2])<<32);
            
            _TotalTime = ((Float_t) temp[3])*1E-6; //in seconds!!!

            // printf("TriggerPattern::%lx\n", TriggerPattern);
            if(!_IsFragTriggerOn && ((TriggerPattern >> 1)&0x1) == 1 )
                _IsFragTriggerOn = true;
            
            if(_hTriggerPattern != nullptr) FillHistoTrigPattern(TriggerPattern);
        }
        else if (bankName[0]=='T' && bankName[1]=='R' && bankName[2]=='G' && bankName[3]=='C')
        {
            // for(int i=0; i<bankSize; ++i){printf("%4d:%08x\t%u\n", i, temp[i], temp[i]);}
            memcpy(_TriggerCount, temp, sizeof(_TriggerCount));
        }
    }
}


void CReadBinary::FillHistoTGEN(TH2F* hTGEN)
{
    uint64_t TriggerGenerationBin = 0;
    uint64_t TrigOr = 0;
    for(unsigned int iclktick=0; iclktick<32; iclktick++)
    {
        TriggerGenerationBin = _TriggerGenerationBin[iclktick];
        TrigOr = TrigOr | TriggerGenerationBin;
        int bit[14]={0,1,2,3,4,5,6,7,8,9,10,11,12,63};
        for(int ialgo=0; ialgo<14; ialgo++)
        {
            if( ((TriggerGenerationBin >> bit[ialgo])&0x1 )== 1)
                hTGEN->Fill( (float)iclktick, (float) ialgo);
        }
        _TriggerGenerationBin[iclktick] = 0; //auto reset ouput
    /*
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 0) & 0x1); // MARGOR
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 1) & 0x1); // MARG MAJ
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 2) & 0x1); // MARG MAJ REG
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 3) & 0x1); // TOFTRG
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 4) & 0x1); // CALOOR
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 5) & 0x1); // NEUTRON
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 6) & 0x1); // INTERSPILL TRG?
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 7) & 0x1); // TRIGBACKTRG ?
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 8) & 0x1); // FRAGTOFREG
    _hTGEN->Fill(i+1, (TriggerGenerationBin >> 9) & 0x1); // FRAGVETO
    _hTGEN->Fill(i+1, (TriggerGenerationBin >>10) & 0x1); // FRAGTOFROMEREG
    _hTGEN->Fill(i+1, (TriggerGenerationBin >>11) & 0x1); // FRAGVETOROME
    _hTGEN->Fill(i+1, (TriggerGenerationBin >>12) & 0x1); // FRAGTOFREGT1
    _hTGEN->Fill(i+1, (TriggerGenerationBin >>63) & 0x1); // TRIGGER
    */
    }
}

void CReadBinary::FillHistoTrigRates()
{
    for(int i=0; i<64; ++i)
        _hTriggerRates->SetBinContent(i + 2, (Double_t)_TriggerCount[i]/_TotalTime);
}


void CReadBinary::FillHistoTrigPattern(uint64_t TriggerPattern)
{
    uint64_t mask=0x1;
    for(unsigned int i=0; i<64; i++){
        if( (TriggerPattern&mask)!=0 )  _hTriggerPattern->Fill(i);
        mask =mask<<1;
    }
}


void CReadBinary::AlignTriggerCell()
{
    std::vector<CWaveFormContainer*>::iterator itWDB;
    
    int SCboard_id = _wdb_index->at( (UShort_t)SCBOARD );
    t1 = _data_wdb->at(SCboard_id)->data.t[16][(WAVEFORMBINS - drsch[16].trigger_cell) % WAVEFORMBINS];
    for (itWDB = _data_wdb->begin(); itWDB != _data_wdb->end(); ++itWDB)
    {
        for (unsigned int i = 0; i < NUMBEROFCHANNELS; ++i)
        {
            if( !(*itWDB)->data.ch_on[i] )  continue; 

            t2 = (*itWDB)->data.t[i][(WAVEFORMBINS - drsch[i].trigger_cell) % WAVEFORMBINS];
            dt = t1 - t2;
            Float_t* time_ptr = &((*itWDB)->data.t[i][0]);
            for (int j=0 ; j<WAVEFORMBINS ; j++)
            {
                *time_ptr += dt;
                ++time_ptr;
            }
        }
    }
    return;
}


void CReadBinary::AlignSignalsRight()
{
    std::vector<CWaveFormContainer*>::iterator itWDB;
    
    int SCboard_id = _wdb_index->at( (UShort_t)SCBOARD );
    t1 = _data_wdb->at(SCboard_id)->data.t[16][WAVEFORMBINS - 1];
    for (itWDB = _data_wdb->begin(); itWDB != _data_wdb->end(); ++itWDB)
    {
        for (unsigned int i = 0; i < NUMBEROFCHANNELS; ++i)
        {
            if( !(*itWDB)->data.ch_on[i] )  continue; 

            t2 = (*itWDB)->data.t[i][WAVEFORMBINS - 1];
            dt = t1 - t2;
            Float_t* time_ptr = &((*itWDB)->data.t[i][0]);
            for (int j=0 ; j<WAVEFORMBINS ; j++)
            {
                *time_ptr += dt;
                ++time_ptr;
            }
        }
    }
    return;
}


Bool_t CReadBinary::ReadEvtStartWords(FILE* f)
{
    Bool_t check = false;
    char eh[4];
    // int pos=0;
    while( !feof(f) )
    {
        fread(eh, sizeof(eh), 1, f);
        if(memcmp(eh, "EHDR", 4) == 0)
        {
            check = true;
            break;
        }
    }

    if(check) fseek(f, -4, SEEK_CUR);
    return check;
}



/***************************************** TDC *************************************/

Bool_t CReadBinary::ReadTDCData(FILE* f)
{
    unsigned int buffer1;

    fread(&buffer1, sizeof(buffer1), 1, f);
    fread(&buffer1, sizeof(buffer1), 1, f);
    fread(&buffer1, sizeof(buffer1), 1, f);
    fread(&buffer1, sizeof(buffer1), 1, f);
    
    // cout << "GlobHeader::" << std::hex << buffer1 << endl;

    fread(&buffer1, sizeof(buffer1), 1, f);

    buffer1 = ( buffer1 >>27 ) & 0x1f;
    
    fseek(f, -4, SEEK_CUR);

    int count = 0;

    while ( buffer1 != 0x10 )
    {
        if ( buffer1 == 0x0 )
        {
            fread(&buffer1, sizeof(buffer1), 1, f);
            count++;
            unsigned int c = ( buffer1 >> 19 ) & 0x7F;
            unsigned int m = buffer1 & 0x7FFFF;
            m *= 0.1;
            if(_TDCchMap->size() != 4)
            {
                if(_TDCchMap->find(c) == _TDCchMap->end())
                    (*_TDCchMap)[c] = _TDCchMap->size();
            }

            if(_TDCchMap->find(c) == _TDCchMap->end())
            {
                Error("ReadTDCData()", "Found channel %d that is not in the TDCchMap!", c);
                throw -1;
            }
            _TDCTime[ _TDCchMap->at(c) ] = m;
        }
        else if ( buffer1 == 0x1 ){ fread(&buffer1, sizeof(buffer1), 1, f); }
        else if ( buffer1 == 0x3 ){ fread(&buffer1, sizeof(buffer1), 1, f); }
        else if ( buffer1 == 0x11 ){ fread(&buffer1, sizeof(buffer1), 1, f); }
        else
        {
            Error("ReadTDCData()", "Unexpected sequence in TDC readout");
            throw -1;
        }
        
        fread(&buffer1, sizeof(buffer1), 1, f);

        buffer1 = ( buffer1 >>27 ) & 0x1f;
    
        fseek(f, -4, SEEK_CUR);
    }
    fread(&buffer1, sizeof(buffer1), 1, f);
    fread(&buffer1, sizeof(buffer1), 1, f);
    fread(&buffer1, sizeof(buffer1), 1, f);

    if(count != 4)
    {
        char eh[4];
        while(!feof(f) && memcmp(eh, "EHDR", 4) != 0)
        {
            fread(&eh, sizeof(eh), 1, f);
        }
        return false;
    }
    else
    {
        return true;
    }
}


/********************************* FRAG TRIGGER ************************************/

Bool_t CReadBinary::IsFragTriggerOn()
{
    return _IsFragTriggerOn;
}

void CReadBinary::ResetFragTrigger()
{
    _IsFragTriggerOn = false;
}
```


-------------------------------

Updated on 2022-01-12 at 16:47:44 +0000
