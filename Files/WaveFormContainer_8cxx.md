---
title: src/WFProcessing/WaveFormContainer.cxx
summary: File containing all methods used for Waveform processing. 

---

# src/WFProcessing/WaveFormContainer.cxx

File containing all methods used for Waveform processing.  [More...](#detailed-description)

## Detailed Description

File containing all methods used for Waveform processing. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "WaveFormContainer.h"

WaveFormContainer::WaveFormContainer()
{
    data.clear();
};

WaveFormContainer::~WaveFormContainer()
{
    ClearData();
}


void WaveFormContainer::ClearData()
{
    memset(_Ped,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Amp,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Charge,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Time,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_RiseTime,0,sizeof(Float_t)*NUMBEROFCHANNELS);
}


Bool_t WaveFormContainer::IsEmpty(Int_t channel)
{
    //channel empty: return true
    if(!data.ch_on[channel]){return true;}
    else
    {
        //channel not empty: check if dynamic range overflow occurs and return false
        auto minmax = std::minmax_element(&data.w[channel][EMPTYSTARTBIN], &data.w[channel][EMPTYSTOPBIN]);

        //second filter -> remove all channels under a certain amplitude
        if(*(minmax.second) - *(minmax.first) <= EMPTYTS)
        {
            data.ch_on[channel] = false;
            return true;
        }

        return false;
    }
}


Bool_t WaveFormContainer::IsEmptyTest(Int_t channel)
{
    //channel empty: return true
    if(!data.ch_on[channel]){return true;}
    else
    {
        //channel not zero-suppressed -> check if noise or signal and
        //correct for possible dynamic range overflow
        Bool_t check = true;
        Float_t min = 3;
        Float_t max = -3;
        Float_t* itData = &data.w[channel][EMPTYSTARTBIN];
        Float_t* endLoop = &data.w[channel][EMPTYSTOPBIN];
        while(itData != endLoop)
        {
            if(*itData < min)   min = *itData;
            else if(*itData > max)  max = *itData;

            if( max - min > EMPTYTS )
            {
                check = false;
                break;
            }
            ++itData;
        }
        if(check) {return check;}
        
        //CHECK THIS PART FOR HW PROBLEMS!!!!!!!
        // if(channel != 16 && channel != 17)   MedianFilter(channel);

        auto minmax = std::minmax_element(&data.w[channel][EMPTYSTARTBIN], &data.w[channel][EMPTYSTOPBIN]);
        if(*(minmax.second) - *(minmax.first) < EMPTYTS) return true;

        return false;
    }
}


void WaveFormContainer::RescaleTime(std::vector<Float_t>* t)
{
    for(Int_t i = 0; i < t->size(); ++i)
    {
        (*t)[i] *= 1E9;
    }
}


std::pair<Float_t, Float_t> WaveFormContainer::GetPedestal(Int_t channel)
{
    if( _Ped[channel] == 0. || _PedRMS[channel] == 0.) 
    {
        //Find the pedestal of the WF as the median of the first and last bins
        std::vector<Float_t> ped(&data.w[channel][PEDESTALSTARTBIN], &data.w[channel][PEDESTALSTOPBIN]);
        ped.insert(ped.end(), &data.w[channel][ WAVEFORMBINS - PEDESTALSTOPBIN - 1 ], &data.w[channel][WAVEFORMBINS - PEDESTALSTARTBIN - 1 ]);
        std::sort( ped.begin(), ped.end() );

        _Ped[channel] = ped[ped.size()/2 + 1];

        _PedRMS[channel] = 0;
        Float_t mean = 0;
        for(int i=0; i<ped.size(); ++i)
        {
            mean += ped[i];
            _PedRMS[channel] += pow(ped[i],2);
        }
        mean /= ped.size();
        _PedRMS[channel] = TMath::Sqrt(_PedRMS[channel]/ped.size() - pow(mean, 2));

        ped.clear();
    }

    return std::make_pair(_Ped[channel], _PedRMS[channel]);
}


Float_t WaveFormContainer::GetAmplitude(Int_t channel)
{
    if( _Amp[channel] == 0 )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }
        _Amp[channel] = *(std::min_element(&data.w[channel][AMPLITUDESTARTBIN], &data.w[channel][AMPLITUDESTOPBIN])) - _Ped[channel];
    }
    
    return _Amp[channel];
}


Float_t WaveFormContainer::GetCharge(Int_t channel, Int_t start_bin, Int_t stop_bin)
{
    if( _Charge[channel] == 0. )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }

        Float_t a1, a2, t1, t2;
        Float_t m, q, t_half;

        for(Int_t bin = start_bin; bin < stop_bin; ++bin)
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
        }

        _Charge[channel] *= 1E9; //rescale because time needs to be in ns
    }
    
    return _Charge[channel];
}


Float_t WaveFormContainer::GetTimeCFD(Int_t channel, UShort_t board, Int_t event, TFile* fOut, TString detector)
{
    if( _Time[channel] == 0.)
    {
        //Call the method below to calculate the CFD time
        if(_Ped[channel] == 0) { GetPedestal(channel); }
        if(_Amp[channel] == 0) { GetAmplitude(channel); }

        Float_t AbsoluteThreshold = DEFAULTCFDTHRESHOLD*_Amp[channel] + _Ped[channel];

        // evaluate the thresholds
        Float_t Min = *std::min_element(&data.w[channel][TIMESTAMPSTARTBIN], &data.w[channel][TIMESTAMPSTOPBIN]);
        for(Int_t bin = TIMESTAMPSTARTBIN; bin < TIMESTAMPSTOPBIN; ++bin)
        {
            if(data.w[channel][bin] == Min)
            {
                while(data.w[channel][bin-1] < AbsoluteThreshold){bin --;}
                //Analytical formula for the timestamp -> linear interpolation
                _Time[channel] = data.t[channel][bin] - (data.w[channel][bin] - AbsoluteThreshold)* (data.t[channel][bin] - data.t[channel][bin-1])/(data.w[channel][bin] - data.w[channel][bin-1]);
                _Time[channel] *= 1E9; //rescale from s to ns
                break;
            }
        }

        if(board != 0)
        {
            //Save waveforms and CFD related graphs if in debug mode
            SaveWF(board, channel, event, fOut, detector);

            if(!fOut->GetDirectory(Form("Waves%s/Event_%d", detector.Data(), event)))
                fOut->mkdir(Form("Waves%s/Event_%d", detector.Data(), event));
            
            fOut->cd(Form("Waves%s/Event_%d", detector.Data(), event));
            TGraph* CFD_TH = new TGraph(2);
            CFD_TH->SetPoint(0, data.t[channel][0]*1E9, AbsoluteThreshold);
            CFD_TH->SetPoint(1, data.t[channel][WAVEFORMBINS - 1]*1E9, AbsoluteThreshold);
            CFD_TH->SetLineStyle(kDashed);
            CFD_TH->SetLineColor(kBlue);
            CFD_TH->SetLineWidth(1);
            CFD_TH->Write(Form("Board%d_ch%d_CFD_TH", board, channel));
            TGraph* tcfd = new TGraph(2);
            tcfd->SetPoint(0, _Time[channel], _Ped[channel]);
            tcfd->SetPoint(1, _Time[channel], AbsoluteThreshold);
            tcfd->SetLineColor(kRed);
            tcfd->SetLineWidth(2);
            tcfd->SetMarkerSize(0);
            tcfd->Write(Form("Board%d_ch%d_TCFD", board, channel));

            delete CFD_TH;
            delete tcfd;
        }
    }

    return _Time[channel];
}




Float_t WaveFormContainer::GetRiseTime(Int_t channel)
{
    if( _RiseTime[channel] == 0 )
    {
        if(_Ped[channel] == 0) { GetPedestal(channel); }
        if(_Amp[channel] == 0) { GetAmplitude(channel); }

        Float_t Threshold10 = 0.1*_Amp[channel] + _Ped[channel];
        Float_t Threshold90 = 0.9*_Amp[channel] + _Ped[channel];
        Float_t T10=0, T90=0; //variables needed to compute the rise time of the signal

        for(Int_t bin = TIMESTAMPSTARTBIN; bin < TIMESTAMPSTOPBIN; ++bin)
        {
            if(T10 != 0 && T90 != 0) { break; }
            if(T10==0 && data.w[channel][bin] < Threshold10)
            {
                //Analytical formula for the timestamp -> linear interpolation
                T10 = data.t[channel][bin] - (data.w[channel][bin] - Threshold10)* (data.t[channel][bin] - data.t[channel][bin-1])/(data.w[channel][bin] - data.w[channel][bin-1]);
            }

            if(T90==0 && data.w[channel][bin] < Threshold90)
            {
                //Analytical formula for the timestamp -> linear interpolation
                T90 = data.t[channel][bin] - (data.w[channel][bin] - Threshold90)* (data.t[channel][bin] - data.t[channel][bin-1])/(data.w[channel][bin] - data.w[channel][bin-1]);
            }
        }

        _RiseTime[channel] = 1E9*(T90 - T10); // rise time in ns
    }

    return _RiseTime[channel];
}


void WaveFormContainer::MedianFilter(Int_t channel)
{
    std::vector<Float_t> tmp_amp, tmp;
    for(Int_t i = 3; i < sizeof(data.w[channel])/sizeof(Float_t)-3; ++i)
    {
        //store 7 points around index i in a temporary vector
        for(Int_t j = i-3; j <= i+3; ++j)
        {
            tmp.push_back(data.w[channel][j]);
        }
        //sort the vector and store the median
        std::sort(tmp.begin(), tmp.end());
        tmp_amp.push_back(tmp[3]);
        tmp.clear();
    }

    //rewrite the waveform through the vector of the medians
    for(Int_t i = 0; i < tmp_amp.size(); ++i)
    {
        data.w[channel][i+3] = tmp_amp[i];
    }
    //Manually set the first and last points
    data.w[channel][0] = tmp_amp[0];
    data.w[channel][1] = tmp_amp[0];
    data.w[channel][2] = tmp_amp[0];
    data.w[channel][WAVEFORMBINS - 1] = tmp_amp[0];
    data.w[channel][WAVEFORMBINS - 2] = tmp_amp[0];
    data.w[channel][WAVEFORMBINS - 3] = tmp_amp[0];

    tmp_amp.clear();

}



Float_t WaveFormContainer::GetCLKPhase(Int_t channel, UShort_t board, Int_t event, TFile* fOut)
{
    if(channel != 16 && channel != 17)
    {
        Error("GetCLKPhase()", "Channel number != (16,17) --> ch %d", channel);
        throw -1;
    }

    //Save uncorrected CLK signals if in debug
    if(board != 0)  SaveWF(board, channel, event, fOut, "CLK", "Uncorr");

    /*This cycle corrects the effects
    * caused by dynamic range "overflow" in CLKs --> CHECK IF NEEDED!
    */
    auto minmax = std::minmax_element(&data.w[channel][CLKSTARTBIN], &data.w[channel][CLKSTOPBIN]);

    //Find the zero of the CLK waveform
    Float_t wave_0 = (*(minmax.second) + *(minmax.first))/2;
    
    std::vector<Double_t> tarrclk_s, n_clk_s;

    Float_t tarr=0.;
    Int_t count=0, timebin=CLKSTOPBIN;
    //the endloop variable checks if the cycle gets to the end of the WF
    Bool_t endloop=false;

    //find the zero crossing points
    while((timebin > CLKSTARTBIN) && !endloop && count <= 10)
    {
        Float_t amp = data.w[channel][timebin];
        //This part of the cycle is needed to find a rising edge
        while(amp<=wave_0) //Skip the negative part of the WF
        {
            timebin--;
            if(timebin == CLKSTARTBIN + 1)
            {
                endloop=true;
                break;
            }
        amp = data.w[channel][timebin];
        }
        if(endloop)break;

        while(amp>wave_0) //Find the end of the negative part of the WF
        {
            timebin--;
            if(timebin == CLKSTARTBIN + 1)
            {
                endloop=true;
                break;
            }
            amp = data.w[channel][timebin];
        }
        if(endloop)break;

        //find the zero-crossing point by linear interpolation
        tarr = data.t[channel][timebin+1] - (data.w[channel][timebin+1] - wave_0)*(data.t[channel][timebin+1] - data.t[channel][timebin])/(data.w[channel][timebin+1] - data.w[channel][timebin]);
        tarr *= 1E9; //rescale from s to ns

        //Register the data for the fit
        count++;
        tarrclk_s.push_back(tarr);
        n_clk_s.push_back(count); //Number of CLK cycles
    }
    std::reverse( tarrclk_s.begin(), tarrclk_s.end() );

    //Fit the zero-crossing points to get the clock phase
    TGraph* WaveGraphFIT = new TGraph(count, &n_clk_s[0], &tarrclk_s[0]);
    // WaveGraphFIT->Fit("fun", "RQ");
    TLinearFitter *lf = new TLinearFitter(2, "pol1", "");
    lf->AssignData(count, 1, n_clk_s.data(), tarrclk_s.data());
    lf->Eval();

    if(board != 0)
    {
        SaveWF(board, channel, event, fOut, "CLK");
        //Save the fit curve
        if(!fOut->GetDirectory(Form("WavesCLK/Event_%d", event)))
            fOut->mkdir(Form("WavesCLK/Event_%d", event));
        
        TF1* f = new TF1("fun","pol1", 0, 12);
        f->SetParameters(lf->GetParameter(0), lf->GetParameter(1));

        fOut->cd(Form("WavesCLK/Event_%d", event));
        WaveGraphFIT->SetTitle(Form("CLK board %d ch %d linear fit; N_{cycles}; Zero-crossing time [ns]", board, channel));
        WaveGraphFIT->SetMarkerStyle(20);
        WaveGraphFIT->SetLineWidth(0);
        WaveGraphFIT->SetLineColor(kRed);
        WaveGraphFIT->Write(Form("CLK board%d_ch%d_FIT", board, channel));
        f->Write(Form("Board%d_ch%d_LinFit", board, channel));
        delete f;
    }

    Float_t CLKphase = lf->GetParameter(0);

    //some garbage collection
    delete WaveGraphFIT;
    delete lf;
    tarrclk_s.clear();
    n_clk_s.clear();

    return CLKphase;
}


void WaveFormContainer::CopyWaveform(NeutronWF* nWF, Int_t channel)
{
    if(! IsEmpty(channel) )
    {
        GetPedestal( channel );
        Float_t* amp_ptr = &data.w[channel][0];
        for(int i=0; i<WAVEFORMBINS; ++i)
        {
            nWF->V[i] = _Ped[channel] - *amp_ptr;
            amp_ptr++;
        }
        std::copy(std::begin(data.t[channel]), std::end(data.t[channel]), std::begin(nWF->T));
        nWF->IsOn=true;
    }
    else
        nWF->IsOn=false;
}


void WaveFormContainer::SaveWF(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag)
{
    std::vector<Float_t> tmp_time(std::begin(data.t[channel]), std::end(data.t[channel]));
    RescaleTime(&tmp_time);

    if(!fOut->GetDirectory(Form("Waves%s/Event_%d", detector.Data(), event)))
        fOut->mkdir(Form("Waves%s/Event_%d", detector.Data(), event));

    fOut->cd(Form("Waves%s/Event_%d", detector.Data(), event));
    TGraph* WaveGraph = new TGraph(WAVEFORMBINS, &tmp_time[0], &data.w[channel][0]);
    WaveGraph->SetLineColor(kBlack);
    WaveGraph->SetLineWidth(2);
    WaveGraph->SetTitle(Form("%s %s board %d ch %d; Time [ns]; Amplitude [V]", tag.Data(), detector.Data(), board, channel));
    WaveGraph->Write(Form("%s %s board%d_ch%d", tag.Data(), detector.Data(), board, channel));
    delete WaveGraph;

    return;
}
```


-------------------------------

Updated on 2022-03-07 at 17:56:09 +0100
