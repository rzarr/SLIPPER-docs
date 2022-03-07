---
title: src/WFProcessing/TWWaveFormContainer.cxx
summary: File containing all methods used for TOF-Wall Waveform processing. 

---

# src/WFProcessing/TWWaveFormContainer.cxx

File containing all methods used for TOF-Wall Waveform processing.  [More...](#detailed-description)

## Detailed Description

File containing all methods used for TOF-Wall Waveform processing. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "TWWaveFormContainer.h"

TWWaveFormContainer::TWWaveFormContainer()
{
    WaveFormContainer();
}


Float_t TWWaveFormContainer::GetTimeLinear(Int_t channel, UShort_t board, Int_t event, TFile* fOut, TString detector)
{
    if( _Time[channel] == 0 )
    {
        if(_Ped[channel] == 0) { GetPedestal(channel); }
        if(_Amp[channel] == 0) { GetAmplitude(channel); }
        
        //Declare dummy double vectors for TLinearFitter
        std::vector<Double_t> t_tmp, w_tmp;
        TLinearFitter *lf = new TLinearFitter(2, "pol1", "");

        Float_t AbsoluteThreshold = DEFAULTCFDTHRESHOLD*_Amp[channel] + _Ped[channel];

        // evaluate the thresholds
        Float_t Min = *std::min_element(&data.w[channel][TIMESTAMPSTARTBIN], &data.w[channel][TIMESTAMPSTOPBIN]);

        for(Int_t bin = TIMESTAMPSTARTBIN; bin < TIMESTAMPSTOPBIN; ++bin)
        {
            if(data.w[channel][bin] == Min)
            {
                while(data.w[channel][bin-1] < AbsoluteThreshold && bin > 2){bin --;}
                
                if(bin==2)
                {
                    _Time[channel] = -1;
                    break;
                }

                //Assign data for the linear fitter
                for(Int_t i = bin-2; i <= bin+1; ++i)
                {
                    t_tmp.push_back( data.t[channel][i] );
                    w_tmp.push_back( data.w[channel][i] );
                }
                //Fit the 4 data points around the 30% threshold and extrapolate to the baseline
                lf->AssignData(t_tmp.size(), 1, t_tmp.data(), w_tmp.data());
                lf->Eval();
                _Time[channel] = (_Ped[channel] - lf->GetParameter(0))/lf->GetParameter(1);
                _Time[channel] *= 1E9; //rescale from s to ns
                break;
            }
            t_tmp.clear();
            w_tmp.clear();
        }

        if(board != 0)
        {
            //Save waveforms and CFD related graphs if in debug mode
            SaveWF(board, channel, event, fOut, detector);

            if(!fOut->GetDirectory(Form("Waves%s/Event_%d", detector.Data(), event)))
                fOut->mkdir(Form("Waves%s/Event_%d", detector.Data(), event));

            fOut->cd(Form("Waves%s/Event_%d", detector.Data(), event));
            TGraph* Tangent = new TGraph(2);
            if(_Time[channel] > 0)
            {
                Tangent->SetPoint(0, 1E9*(_Ped[channel] + 0.02 - lf->GetParameter(0))/lf->GetParameter(1),_Ped[channel] + 0.02);
                Tangent->SetPoint(1, 1E9*(_Ped[channel] + _Amp[channel] - 0.02 - lf->GetParameter(0))/lf->GetParameter(1),_Ped[channel] + _Amp[channel] - 0.02);
                Tangent->SetLineStyle(kDashDotted);
                Tangent->SetLineColor(kViolet);
                Tangent->SetLineWidth(2);
                Tangent->Write(Form("Board%d_ch%d_Tangent", board, channel));
            }
            TGraph* CFD_TH = new TGraph(2);
            CFD_TH->SetPoint(0, data.t[channel][0]*1E9, AbsoluteThreshold);
            CFD_TH->SetPoint(1, data.t[channel][WAVEFORMBINS - 1]*1E9, AbsoluteThreshold);
            CFD_TH->SetLineStyle(kDashed);
            CFD_TH->SetLineColor(kBlue);
            CFD_TH->SetLineWidth(2);
            CFD_TH->Write(Form("Board%d_ch%d_CFD_TH", board, channel));
            TGraph* tLine = new TGraph(2);
            tLine->SetPoint(0, _Time[channel], _Ped[channel]);
            tLine->SetPoint(1, _Time[channel], _Ped[channel] + _Amp[channel] - 0.02);
            tLine->SetLineColor(kRed);
            tLine->SetLineWidth(2);
            tLine->SetMarkerSize(0);
            tLine->Write(Form("Board%d_ch%d_Time", board, channel));
            TGraph* pLine = new TGraph(2);
            pLine->SetPoint(0, 1E9*data.t[channel][0], _Ped[channel]);
            pLine->SetPoint(1, 1E9*data.t[channel][WAVEFORMBINS-1], _Ped[channel]);
            pLine->SetLineColor(kGreen+3);
            pLine->SetLineStyle(kDashed);
            pLine->SetLineWidth(2);
            pLine->SetMarkerSize(0);
            pLine->Write(Form("Board%d_ch%d_Ped", board, channel));

            delete Tangent;
            delete tLine;
            delete pLine;
            delete CFD_TH;
        }
        delete lf;
    }

    return _Time[channel];
}
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
