---
title: src/WFProcessing/CALOWaveFormContainer.cxx
summary: File containing all methods used for Calorimeter Waveform processing. 

---

# src/WFProcessing/CALOWaveFormContainer.cxx

File containing all methods used for Calorimeter Waveform processing.  [More...](#detailed-description)

## Detailed Description

File containing all methods used for Calorimeter Waveform processing. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "CALOWaveFormContainer.h"

CALOWaveFormContainer::CALOWaveFormContainer()
{
    WaveFormContainer();
}


Float_t CALOWaveFormContainer::GetChargeCALO(Int_t channel, Int_t start_bin, Int_t stop_bin)
{
    if( _Charge[channel] == 0 )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }
        if(_Amp[channel] == 0){ GetAmplitude(channel); }

        _Charge[channel] = 0.;

        Float_t a1, a2, t1, t2;
        Float_t m, q, t_half;
        
        Int_t bin = start_bin;
        Bool_t foundMax = false;
        while(bin < stop_bin)
        {
            t1 = data.t[channel][bin];
            t2 = data.t[channel][bin + 1];
            a1 = _Ped[channel] - data.w[channel][bin];
            a2 = _Ped[channel] - data.w[channel][bin + 1];

            if(a1*a2 < 0)
            {
                m = (a2 - a1)/(t2 - t1);
                q = a2 - m*t2;
                t_half = -q/m;
                _Charge[channel] += 0.5*a1*(t_half - t1);
                _Charge[channel] += 0.5*a2*(t2 - t_half);
            }
            else
            {
                _Charge[channel] += 0.5*(a1 + a2)*(t2 - t1);
            }

            if(!foundMax && a1 == fabs(_Amp[channel]))
                foundMax = true;
            
            if(foundMax && a2 > 0)
                break;
            
            ++bin;
        }

        _Charge[channel] *= 1E9; //rescale because time needs to be in ns
    }
    
    return _Charge[channel];
}
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
