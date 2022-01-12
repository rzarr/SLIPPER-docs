---
title: src/CWaveFormContainer.cxx
summary: File containing all methods used for Waveform processing. 

---

# src/CWaveFormContainer.cxx

File containing all methods used for Waveform processing.  [More...](#detailed-description)

## Detailed Description

File containing all methods used for Waveform processing. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "CWaveFormContainer.h"

CWaveFormContainer::CWaveFormContainer()
{
    data.clear();
};


void CWaveFormContainer::ClearData()
{
    memset(_Ped,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Amp,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Charge,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_Time,0,sizeof(Float_t)*NUMBEROFCHANNELS);
    memset(_RiseTime,0,sizeof(Float_t)*NUMBEROFCHANNELS);

    return;
}


Bool_t CWaveFormContainer::IsEmpty(Int_t channel)
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


Bool_t CWaveFormContainer::IsEmptyTest(Int_t channel)
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


void CWaveFormContainer::RescaleTime(std::vector<Float_t>* t)
{
    for(Int_t i = 0; i < t->size(); ++i)
    {
        (*t)[i] *= 1E9;
    }
}


std::pair<Float_t, Float_t> CWaveFormContainer::GetPedestal(Int_t channel)
{
    if( _Ped[channel] == 0. || _PedRMS[channel] == 0.) 
    {
        std::vector<Float_t> temp;
        Float_t old_mean = 0, new_mean = 0;
        for (Int_t bin = PEDESTALSTARTBIN; bin <= PEDESTALSTOPBIN; ++bin)
        {
            temp.push_back( data.w[channel][bin] );

            new_mean += (data.w[channel][bin] - old_mean)/(bin + 1 - PEDESTALSTARTBIN);
            _PedRMS[channel] += pow(old_mean,2) - pow(new_mean,2) + ( pow(data.w[channel][bin] ,2) - pow(_PedRMS[channel],2) - pow(old_mean,2) ) / (bin + 1 - PEDESTALSTARTBIN);
            old_mean = new_mean;
        }
        std::sort( temp.begin(), temp.end() );
        _Ped[channel] = temp[(PEDESTALSTOPBIN - PEDESTALSTARTBIN)/2];
        temp.clear();

        _PedRMS[channel] = TMath::Sqrt(_PedRMS[channel]);
    }

    return std::make_pair(_Ped[channel], _PedRMS[channel]);
}


Float_t CWaveFormContainer::GetAmplitude(Int_t channel)
{
    if( _Amp[channel] == 0 )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }
        _Amp[channel] = *(std::min_element(&data.w[channel][AMPLITUDESTARTBIN], &data.w[channel][AMPLITUDESTOPBIN])) - _Ped[channel];
    }
    
    return _Amp[channel];
}


Float_t CWaveFormContainer::GetCharge(Int_t channel, Int_t start_bin, Int_t stop_bin)
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

        if(_Charge[channel] < 0) { _Charge[channel]*=-1; }
    }
    
    return _Charge[channel];
}


Float_t CWaveFormContainer::GetChargeCALO(Int_t channel)
{
    if( _Charge[channel] == 0 )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }
        if(_Amp[channel] == 0){ GetAmplitude(channel); }

        _Charge[channel] = 0.;

        Float_t a1, a2, t1, t2;
        Float_t m, q, t_half;
        
        Int_t bin = CHARGESTARTBIN;
        Bool_t foundMax = false;
        while(bin < CHARGESTOPBIN)
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

        if(_Charge[channel] < 0) { _Charge[channel] = 0.; }
    }
    
    return _Charge[channel];
}



Float_t CWaveFormContainer::GetTimeCFD(Int_t channel, UShort_t board, Int_t event, TFile* fOut, TString detector)
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




Float_t CWaveFormContainer::GetTimeLinear(Int_t channel, UShort_t board, Int_t event, TFile* fOut, TString detector)
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
                while(data.w[channel][bin-1] < AbsoluteThreshold){bin --;}
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
            Tangent->SetPoint(0, 1E9*(_Ped[channel] + 0.02 - lf->GetParameter(0))/lf->GetParameter(1),_Ped[channel] + 0.02);
            Tangent->SetPoint(1, 1E9*(_Ped[channel] + _Amp[channel] - 0.02 - lf->GetParameter(0))/lf->GetParameter(1),_Ped[channel] + _Amp[channel] - 0.02);
            Tangent->SetLineStyle(kDashDotted);
            Tangent->SetLineColor(kViolet);
            Tangent->SetLineWidth(2);
            Tangent->Write(Form("Board%d_ch%d_Tangent", board, channel));
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


Float_t CWaveFormContainer::GetRiseTime(Int_t channel)
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


void CWaveFormContainer::MedianFilter(Int_t channel)
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


Float_t CWaveFormContainer::GetTimeSC(std::vector<Int_t>* Channels, UShort_t BoardId, Int_t event, TFile* fOut)
{
    //Declare the arrays for the sum of the WFs
    std::vector<Float_t> SC_Sum_W, SC_Sum_T;

    SumSCWavefoms(Channels, &SC_Sum_W, &SC_Sum_T);

    //Cycle on the channels to save the single signals
    if(BoardId != 0)
    {
        for(std::vector<Int_t>::iterator itCh = Channels->begin(); itCh != Channels->end(); ++itCh)
            SaveWF(BoardId, *itCh, event, fOut, "SC", "");
    }

    //Analyze the final WF
    Float_t baseline;
    Int_t bin_th;

    //Find the minimum of the WF
    Float_t min = *std::min_element(std::begin(SC_Sum_W), std::end(SC_Sum_W));

    //Find the pedestal of the WF as the median of the first 20 bins
    std::vector<Float_t> ped(&SC_Sum_W[0], &SC_Sum_W[30]); //find pedestal in ~7.5 ns
    std::sort( ped.begin(), ped.end() );
    baseline = ped[ped.size()/2 + 1];
    ped.clear();
    //Set the CFD threshold 0.3 times the amplitude of the WF
    Float_t cfd_th = baseline + (min - baseline)*SCCFDTHRESHOLD;

    Float_t SCTime = 0;
    //Find the point where the WF passes the CFD_th through linear interpolation
    for(Int_t i = 0; i < SC_Sum_T.size(); ++i)
    {
        if(SC_Sum_W[i] == min)
        {
            while(SC_Sum_W[i-1] < cfd_th){i --;}
            
            SCTime = SC_Sum_T[i] - (SC_Sum_W[i] - cfd_th)*(SC_Sum_T[i] - SC_Sum_T[i-1])/(SC_Sum_W[i] - SC_Sum_W[i-1]);
            SCTime *= 1E9; //rescale from s to ns
            bin_th = i;
            break;
        }
    }

    if(BoardId != 0)
    {
        //Rescale time for the plot
        for(int i = 0; i < SC_Sum_T.size(); ++i)
            SC_Sum_T[i] *= 1E9;

        //Save some other graphs if in debug mode
        TGraph* WaveGraph = new TGraph(SC_Sum_T.size(), &SC_Sum_T[0], &SC_Sum_W[0]);

        if(!fOut->GetDirectory(Form("WavesSC/Event_%d", event)))
        {
            fOut->mkdir(Form("WavesSC/Event_%d", event));
        }
        fOut->cd(Form("WavesSC/Event_%d", event));
        WaveGraph->SetTitle(Form("SC WF sum board %d; Time [ns]; Amplitude [a.u.]", BoardId));
        WaveGraph->SetLineWidth(2);
        WaveGraph->SetLineColor(kBlack);
        WaveGraph->Write(Form("SC_WAVE_SUM board %d", BoardId));
        TGraph* line = new TGraph(2);
        line->SetPoint(0, SCTime, baseline);
        line->SetPoint(1, SCTime, WaveGraph->Eval(SCTime));
        line->SetLineColor(kRed);
        line->SetLineWidth(2);
        line->Write("SC_SUM_CFD");
        TGraph* threshold = new TGraph(2);
        threshold->SetPoint(0, SC_Sum_T[0], cfd_th);
        threshold->SetPoint(1, SC_Sum_T[SC_Sum_T.size() - 1], cfd_th);
        threshold->SetLineWidth(1);
        threshold->SetLineColor(kBlue);
        threshold->SetLineStyle(kDashed);
        threshold->Write("SC_SUM_CFDth");
        delete line;
        delete threshold;
        delete WaveGraph;
    }

    SC_Sum_W.clear();
    SC_Sum_T.clear();

    return SCTime;
}



Float_t CWaveFormContainer::GetTimeSC_Linear(std::vector<Int_t>* Channels)
{
    //Declare the arrays for the sum of the WFs
    std::vector<Float_t> SC_Sum_W, SC_Sum_T;

    SumSCWavefoms(Channels, &SC_Sum_W, &SC_Sum_T);

    //Analyze the final WF
    Float_t baseline;
    Int_t bin_th;
    //Declare dummy double vectors for TLinearFitter
    std::vector<Double_t> t_tmp, w_tmp;

    //Find the minimum of the WF
    Float_t min = *std::min_element(std::begin(SC_Sum_W), std::end(SC_Sum_W));

    //Find the pedestal of the WF as the median of the first 20 bins
    std::vector<Float_t> ped(&SC_Sum_W[0], &SC_Sum_W[30]); //find pedestal in ~7.5 ns
    std::sort(ped.begin(), ped.end());
    baseline = ped[ped.size()/2 + 1];
    ped.clear();
    //Set the CFD threshold 0.3 times the amplitude of the WF
    Float_t cfd_th = baseline + (min - baseline)*SCCFDTHRESHOLD;

    Float_t SCTime;
    //Find the point where the WF passes the CFD_th through linear interpolation
    for(Int_t i = 0; i < SC_Sum_T.size(); ++i)
    {
        if(SC_Sum_W[i] == min)
        {
            while(SC_Sum_W[i-1] < cfd_th){ i --;}
            //Assign data for the linear fitter
            for(Int_t j = i-2; j <= i+1; ++j)
            {
                t_tmp.push_back( Double_t(SC_Sum_T[j]) );
                w_tmp.push_back( Double_t(SC_Sum_W[j]) );
            }
            TLinearFitter *lf = new TLinearFitter(2, "pol1", "");
            lf->AssignData(t_tmp.size(), 1, t_tmp.data(), w_tmp.data());
            lf->Eval();
            SCTime = (baseline - lf->GetParameter(0))/lf->GetParameter(1);
            SCTime *= 1E9; //rescale from s to ns
            delete lf;
            break;
        }
    }

    SC_Sum_W.clear();
    SC_Sum_T.clear();

    return SCTime;
}


void CWaveFormContainer::SumSCWavefoms(std::vector<Int_t>* Channels, std::vector<Float_t>* SC_Sum_W, std::vector<Float_t>* SC_Sum_T)
{
    //Decide a time interval where to look for SC timestamps
    Int_t sum_start_bin = SCSUMSTARTBIN; //~ 2 ns
    Int_t sum_bin_length = SCSUMSTOPBIN - SCSUMSTARTBIN; //~ 75 ns

    //Set the timestamps of the final WF
    Float_t time_step = (data.t[0][WAVEFORMBINS - 1] - data.t[0][0])/(WAVEFORMBINS - 1);
    for(Int_t i = 0; i < sum_bin_length; ++i)
    {
        SC_Sum_T->push_back(data.t[0][0] + (sum_start_bin + i)*time_step);
    }

    //Cycle on the channels to check their "goodness" and add them to the final WF
    for(std::vector<Int_t>::iterator itCh = Channels->begin(); itCh != Channels->end(); ++itCh)
    {
        Float_t* x_down = &data.t[*itCh][SCSUMSTARTBIN];
        Float_t* x_up = &data.t[*itCh][SCSUMSTARTBIN + 1];
        Float_t* y_down = &data.w[*itCh][SCSUMSTARTBIN];
        Float_t* y_up = &data.w[*itCh][SCSUMSTARTBIN + 1];
        Float_t value = 0;
        Int_t current_ch_bin = 0;
        for(Int_t i = 0; i<sum_bin_length; ++i)
        {
            while( (*SC_Sum_T)[i] >= *x_up )
            {
                x_down++;
                x_up++;
                y_down++;
                y_up++;
            }
            value = *y_down + ( (*SC_Sum_T)[i] - *x_down)*(*y_up - *y_down)/(*x_up - *x_down);

            if( *itCh == Channels->at(0) )
                SC_Sum_W->push_back(value);

            else
                (*SC_Sum_W)[i] += value;
        }
    }
}



Float_t CWaveFormContainer::GetCLKPhase(Int_t channel, UShort_t board, Int_t event, TFile* fOut)
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


void CWaveFormContainer::CopyWaveform(NeutronWF* nWF, Int_t channel)
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


void CWaveFormContainer::SaveWF(Int_t board, Int_t channel, Int_t event, TFile * fOut, TString detector, TString tag)
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

Updated on 2022-01-12 at 10:56:23 +0000
