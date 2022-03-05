---
title: src/WFProcessing/SCWaveFormContainer.cxx
summary: File containing all methods used for Start Counter Waveform processing. 

---

# src/WFProcessing/SCWaveFormContainer.cxx

File containing all methods used for Start Counter Waveform processing.  [More...](#detailed-description)

## Detailed Description

File containing all methods used for Start Counter Waveform processing. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "SCWaveFormContainer.h"

SCWaveFormContainer::SCWaveFormContainer()
{
    WaveFormContainer();
    _SC_Sum_T.clear();
    _SC_Sum_W.clear();
    _SCped=0;
}


void SCWaveFormContainer::ClearData()
{
    WaveFormContainer::ClearData();
    _SC_Sum_T.clear();
    _SC_Sum_W.clear();
    _SCped=0;

    return;
}


Float_t SCWaveFormContainer::GetChargeSC(Int_t channel, Int_t start_bin, Int_t stop_bin)
{
    if( _Charge[channel] == 0. )
    {
        if(_Ped[channel] == 0){ GetPedestal(channel); }

        Float_t a1, a2, t1, t2;
        Float_t m, q, t_half;
        Float_t IntegralThreshold = _Ped[channel] + 2*_PedRMS[channel];

        for(Int_t bin = start_bin; bin < stop_bin; ++bin)
        {
            if(data.w[channel][bin] > IntegralThreshold || data.w[channel][bin+1] > IntegralThreshold)  continue;
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



Float_t SCWaveFormContainer::GetSCTotalCharge(std::vector<Int_t>* Channels)
{
    Float_t charge = 0;

    if(_SCped == 0) SumSCWavefoms(Channels);

    Float_t a1, a2, t1, t2;
    Float_t m, q, t_half;
    Float_t chargeStep;
    Float_t Threshold = _SCped + 2*_SCpedRMS;

    for(Int_t bin = 0; bin < _SC_Sum_W.size() - 1; ++bin)
    {
        if(_SC_Sum_W[bin] > Threshold || _SC_Sum_W[bin+1] > Threshold) continue;

        chargeStep=0;
        t1 = _SC_Sum_T[bin];
        t2 = _SC_Sum_T[bin + 1];
        a1 = _SCped - _SC_Sum_W[bin];
        a2 = _SCped - _SC_Sum_W[bin + 1];


        if(a1*a2 < 0)
        {
            m = (a2 - a1)/(t2 - t1);
            q = a2 - m*t2;
            t_half = -q/m;
            chargeStep += 0.5*a1*(t_half - t1);
            chargeStep += 0.5*a2*(t2 - t_half);
        }
        else
        {
            chargeStep += 0.5*(a1 + a2)*(t2 - t1);
        }

        charge += chargeStep;
    }

    charge *= 1E9; //rescale because time needs to be in ns

    // if(charge < 0) { charge*=-1; }
    
    return charge;
}



Float_t SCWaveFormContainer::GetTimeSC(Bool_t* IsPossiblePileUp, std::vector<Int_t>* Channels, UShort_t BoardId, Int_t event, TFile* fOut)
{
    SumSCWavefoms(Channels);

    //Cycle on the channels to save the single signals
    if(fOut)
    {
        for(std::vector<Int_t>::iterator itCh = Channels->begin(); itCh != Channels->end(); ++itCh)
            SaveWF(BoardId, *itCh, event, fOut, "SC", "");
    }
    *IsPossiblePileUp = CheckForPileUp(&_SC_Sum_W, &_SC_Sum_T, event, fOut);

    //Analyze the final WF
    Int_t bin_th;

    //Find the minimum of the WF
    Float_t min = *std::min_element(std::begin(_SC_Sum_W), std::end(_SC_Sum_W));

    //Set the CFD threshold 0.3 times the amplitude of the WF
    Float_t cfd_th = _SCped + (min - _SCped)*SCCFDTHRESHOLD;

    Float_t SCTime = 0;
    //Find the point where the WF passes the CFD_th through linear interpolation
    for(Int_t i = 0; i < _SC_Sum_T.size(); ++i)
    {
        if(_SC_Sum_W[i] == min)
        {
            while(_SC_Sum_W[i-1] < cfd_th){i --;}
            
            SCTime = _SC_Sum_T[i] - (_SC_Sum_W[i] - cfd_th)*(_SC_Sum_T[i] - _SC_Sum_T[i-1])/(_SC_Sum_W[i] - _SC_Sum_W[i-1]);
            SCTime *= 1E9; //rescale from s to ns
            bin_th = i;
            break;
        }
    }

    if(fOut)
    {
        //Rescale time for the plot
        for(int i = 0; i < _SC_Sum_T.size(); ++i)
            _SC_Sum_T[i] *= 1E9;

        //Save some other graphs if in debug mode
        TGraph* WaveGraph = new TGraph(_SC_Sum_T.size(), &_SC_Sum_T[0], &_SC_Sum_W[0]);

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
        line->SetPoint(0, SCTime, _SCped);
        line->SetPoint(1, SCTime, WaveGraph->Eval(SCTime));
        line->SetLineColor(kRed);
        line->SetLineWidth(2);
        line->Write("SC_SUM_CFD");
        TGraph* threshold = new TGraph(2);
        threshold->SetPoint(0, _SC_Sum_T[0], cfd_th);
        threshold->SetPoint(1, _SC_Sum_T[_SC_Sum_T.size() - 1], cfd_th);
        threshold->SetLineWidth(1);
        threshold->SetLineColor(kBlue);
        threshold->SetLineStyle(kDashed);
        threshold->Write("SC_SUM_CFDth");
        TGraph* ped_line = new TGraph(2);
        ped_line->SetPoint(0, _SC_Sum_T[0], _SCped);
        ped_line->SetPoint(1, _SC_Sum_T[_SC_Sum_T.size() - 1], _SCped);
        ped_line->SetLineWidth(1);
        ped_line->SetLineColor(kGreen+3);
        ped_line->SetLineStyle(kDashed);
        ped_line->Write("SC_SUM_ped");
        delete line;
        delete threshold;
        delete ped_line;
        delete WaveGraph;
    }

    return SCTime;
}



Float_t SCWaveFormContainer::GetTimeSC_Linear(std::vector<Int_t>* Channels)
{
    SumSCWavefoms(Channels);

    //Analyze the final WF
    Int_t bin_th;
    //Declare dummy double vectors for TLinearFitter
    std::vector<Double_t> t_tmp, w_tmp;

    //Find the minimum of the WF
    Float_t min = *std::min_element(std::begin(_SC_Sum_W), std::end(_SC_Sum_W));

    //Set the CFD threshold 0.3 times the amplitude of the WF
    Float_t cfd_th = _SCped + (min - _SCped)*SCCFDTHRESHOLD;

    Float_t SCTime;
    //Find the point where the WF passes the CFD_th through linear interpolation
    for(Int_t i = 0; i < _SC_Sum_T.size(); ++i)
    {
        if(_SC_Sum_W[i] == min)
        {
            while(_SC_Sum_W[i-1] < cfd_th){ i --;}
            //Assign data for the linear fitter
            for(Int_t j = i-2; j <= i+1; ++j)
            {
                t_tmp.push_back( Double_t(_SC_Sum_T[j]) );
                w_tmp.push_back( Double_t(_SC_Sum_W[j]) );
            }
            TLinearFitter *lf = new TLinearFitter(2, "pol1", "");
            lf->AssignData(t_tmp.size(), 1, t_tmp.data(), w_tmp.data());
            lf->Eval();
            SCTime = (_SCped - lf->GetParameter(0))/lf->GetParameter(1);
            SCTime *= 1E9; //rescale from s to ns
            delete lf;
            break;
        }
    }

    _SC_Sum_W.clear();
    _SC_Sum_T.clear();

    return SCTime;
}


void SCWaveFormContainer::SumSCWavefoms(std::vector<Int_t>* Channels)
{
    if( _SC_Sum_T.size() < 1 )
    {
        //Decide a time interval where to look for SC timestamps
        Int_t sum_start_bin = SCSUMSTARTBIN; //~ 2 ns
        Int_t sum_bin_length = SCSUMSTOPBIN - SCSUMSTARTBIN; //~ 75 ns

        //Set the timestamps of the final WF
        Float_t time_step = (data.t[0][WAVEFORMBINS - 1] - data.t[0][0])/(WAVEFORMBINS - 1);
        for(Int_t i = 0; i < sum_bin_length; ++i)
        {
            _SC_Sum_T.push_back(data.t[0][0] + (sum_start_bin + i)*time_step);
        }

        Float_t *x_down, *x_up, *y_down, *y_up;
        //Cycle on the channels to check their "goodness" and add them to the final WF
        for(std::vector<Int_t>::iterator itCh = Channels->begin(); itCh != Channels->end(); ++itCh)
        {
            x_down = &data.t[*itCh][SCSUMSTARTBIN];
            x_up = &data.t[*itCh][SCSUMSTARTBIN + 1];
            y_down = &data.w[*itCh][SCSUMSTARTBIN];
            y_up = &data.w[*itCh][SCSUMSTARTBIN + 1];
            Float_t value = 0;
            Int_t current_ch_bin = 0;
            for(Int_t i = 0; i<sum_bin_length; ++i)
            {
                while( _SC_Sum_T[i] >= *x_up )
                {
                    x_down++;
                    x_up++;
                    y_down++;
                    y_up++;
                }
                value = *y_down + ( _SC_Sum_T[i] - *x_down)*(*y_up - *y_down)/(*x_up - *x_down);

                if( *itCh == Channels->at(0) )
                    _SC_Sum_W.push_back(value);

                else
                    _SC_Sum_W[i] += value;
            }
        }

    }

    if(_SCped == 0)
    {
        //Find the pedestal of the WF as the median of the first 20 bins
        std::vector<Float_t> ped(&_SC_Sum_W[0], &_SC_Sum_W[20]); //find pedestal in ~7.5 ns
        ped.insert(ped.end(), &_SC_Sum_W[ _SC_Sum_W.size() - 21 ], &_SC_Sum_W[ _SC_Sum_W.size() - 1 ]);
        std::sort( ped.begin(), ped.end() );
        _SCped = ped[ped.size()/2 + 1];

        _SCpedRMS = 0;
        Float_t mean = 0;
        for(int i=0; i<ped.size(); ++i)
        {
            mean += ped[i];
            _SCpedRMS += pow(ped[i],2);
        }
        mean /= ped.size();
        _SCpedRMS = TMath::Sqrt(_SCpedRMS/ped.size() - pow(mean, 2));

        ped.clear();
    }
}


Bool_t SCWaveFormContainer::CheckForPileUp(std::vector<Float_t>* w_ptr, std::vector<Float_t>* t_ptr, Int_t event, TFile* fOut)
{
    std::vector<Float_t> Der_W, Der_T;

    Float_t* x_down = &t_ptr->at(0);
    Float_t* x_up = &t_ptr->at(4);
    Float_t* y_down = &w_ptr->at(0);
    Float_t* y_up = &w_ptr->at(4);
    Float_t max = 0;

    for(int i = 0; i < w_ptr->size() - 5; ++i)
    {
        Der_T.push_back( *(x_down + 2) );
        Der_W.push_back( 1E-9*(*y_up - *y_down)/(*x_up - *x_down) );
        x_down++;
        x_up++;
        y_down++;
        y_up++;
        if(Der_W[i] > max) max = Der_W[i];
    }

    Float_t PileUpThreshold = 0.5*max;
    Int_t Ncross = 0;
    Int_t slope=-1;
    for(int i=1; i<Der_W.size(); ++i)
    {
        if( (fabs( Der_W[i] ) - PileUpThreshold)*(fabs( Der_W[i-1] ) - PileUpThreshold) < 0)
            Ncross++;
    }

    if(fOut)
    {
        //Rescale time for the plot
        for(int i = 0; i < Der_T.size(); ++i)   Der_T[i] *= 1E9;

        //Save some other graphs if in debug mode
        TGraph* WaveGraph = new TGraph(Der_T.size(), &Der_T[0], &Der_W[0]);

        if(!fOut->GetDirectory(Form("WavesSC/Event_%d", event)))
        {
            fOut->mkdir(Form("WavesSC/Event_%d", event));
        }
        fOut->cd(Form("WavesSC/Event_%d", event));
        WaveGraph->SetTitle("SC WF der; Time [ns]; Derivative [V/ns]");
        WaveGraph->SetLineWidth(2);
        WaveGraph->SetLineColor(kBlack);
        WaveGraph->Write(Form("SC_WAVE_DER_Cross%d",Ncross));
        TGraph* lineUp = new TGraph(2);
        lineUp->SetPoint(0, Der_T[0], PileUpThreshold);
        lineUp->SetPoint(1, Der_T[Der_T.size() - 1], PileUpThreshold);
        lineUp->SetLineColor(kRed);
        lineUp->SetLineStyle(kDashed);
        lineUp->SetLineWidth(2);
        lineUp->Write("Der_Th_Up");
        TGraph* lineDown = new TGraph(2);
        lineDown->SetPoint(0, Der_T[0], -PileUpThreshold);
        lineDown->SetPoint(1, Der_T[Der_T.size() - 1], -PileUpThreshold);
        lineDown->SetLineColor(kRed);
        lineDown->SetLineStyle(kDashed);
        lineDown->SetLineWidth(2);
        lineDown->Write("Der_Th_Down");
        delete WaveGraph;
        delete lineUp;
        delete lineDown;
    }

    if(Ncross == 4)
        return false;
    else
        return true;
}
```


-------------------------------

Updated on 2022-03-05 at 18:47:20 +0000
