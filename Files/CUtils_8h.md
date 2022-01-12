---
title: src/Utilities/CUtils.h
summary: File containing all utility classes for binary decoding, data storing and file tagging. 

---

# src/Utilities/CUtils.h

File containing all utility classes for binary decoding, data storing and file tagging.  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[WDTag](/Classes/classWDTag.md)** <br>Class for WaveDREAM stand-alone files tagging.  |
| class | **[TDAQTag](/Classes/classTDAQTag.md)** <br>Class for TDAQ files tagging.  |
| class | **[WDBDATA](/Classes/classWDBDATA.md)** <br>Class for WaveDREAM board data container.  |
| class | **[TCBDATA](/Classes/classTCBDATA.md)** <br>Class for Trigger Concentrator Board data container.  |
| class | **[NeutronWF](/Classes/classNeutronWF.md)** <br>Class for Neutron WaveForms storing.  |

## Detailed Description

File containing all utility classes for binary decoding, data storing and file tagging. 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef CUTILS_H
#define CUTILS_H

#include "Parameters.h"

class WDTag
{
public:
    // Float_t Gain;                    ///< Frontend WaveDAQ Gain
    Float_t BeamEnergy;                 
    // Float_t BeamPositionX;           ///< X coordinate of the beam
    // Float_t BeamPositionY;           ///< Y coordinate of the beam
    ParticleType PrimaryParticle;       
    Int_t FileNumber;                   
};


class TDAQTag
{
public:
    Int_t RunNumber;        
    Int_t FileNumber;       
};


class WDBDATA {
    public:
    void clear()
    {
        memset(w,0,sizeof(Float_t)*NUMBEROFCHANNELS*WAVEFORMBINS);
        memset(t,0,sizeof(Float_t)*NUMBEROFCHANNELS*WAVEFORMBINS);
        memset(ch_on,0,sizeof(Bool_t)*NUMBEROFCHANNELS);
        memset(trigcell,0,sizeof(UShort_t)*NUMBEROFCHANNELS);
        memset(adc_waveform,0,sizeof(UShort_t)*(NUMBEROFCHANNELS - 2)*WAVEFORMBINS*2);
        memset(tdc_waveform,0,sizeof(UChar_t)*(NUMBEROFCHANNELS - 2)*WAVEFORMBINS/2);
        memset(trigger_data,0,sizeof(ULong_t)*WAVEFORMBINS/2);
        memset(scaler,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    }
    Float_t w[NUMBEROFCHANNELS][WAVEFORMBINS];                  
    Float_t t[NUMBEROFCHANNELS][WAVEFORMBINS];                  
    Bool_t ch_on[NUMBEROFCHANNELS];                             
    UShort_t trigcell[NUMBEROFCHANNELS];                        
    UShort_t adc_waveform[NUMBEROFCHANNELS-2][WAVEFORMBINS*2];  
    UChar_t tdc_waveform[NUMBEROFCHANNELS-2][WAVEFORMBINS/2];   
    ULong_t trigger_data[WAVEFORMBINS/2];                       
    Float_t scaler[NUMBEROFCHANNELS];                           
};

class TCBDATA {
    public:
    TCBDATA() {clear();}
    void clear()
    {
        memset(in_waveform,0,sizeof(ULong_t)*(NUMBEROFCHANNELS-2)*128);
        memset(out_waveform,0,sizeof(ULong_t)*128);
        memset(gent_waveform,0,sizeof(ULong_t)*32);
    }
    ULong_t in_waveform[NUMBEROFCHANNELS-2][128];   
    ULong_t out_waveform[128];                      
    ULong_t gent_waveform[32];                      
};


class NeutronWF{
    public:
    NeutronWF() {clear();}
    void clear()
    {
        memset(V,0,sizeof(Float_t)*WAVEFORMBINS);
        memset(T,0,sizeof(Float_t)*WAVEFORMBINS);
        IsOn=false;
    }
    Float_t V[WAVEFORMBINS];    
    Float_t T[WAVEFORMBINS];    
    Bool_t IsOn;                
};

// Data structures of all the headers in WaveDAQ binary files
// Useful for ReadBinary class
typedef struct {
    char           tag[3];
    char           version;
} FHEADER;

typedef struct {
    char           time_header[4];
} THEADER;

typedef struct {
    char           bn[2];
    unsigned short board_serial_number;
} BHEADER;

typedef struct {
    float          board_temperature;
    float          board_range;
    unsigned short sampling_frequency;
    unsigned short flags;
} DRSBHEADER;

typedef struct {
    char           event_header[4];
    unsigned short event_serial_number;
    unsigned short trigger_type;
    unsigned int serial_trigger_data;
} EHEADER;

typedef struct {
    char           c[1];
    char           cn[3];
} CHEADER;

typedef struct {
    unsigned short frontendsettings;
    unsigned short trigger_cell;
} DRSCHEADER;

typedef struct{
    float bin_width[NUMBEROFCHANNELS][WAVEFORMBINS];
} WDBBIN;

#endif
```


-------------------------------

Updated on 2022-01-12 at 10:56:23 +0000
