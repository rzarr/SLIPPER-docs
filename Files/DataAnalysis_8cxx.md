---
title: src/DataAnalysis.cxx
summary: File containing all methods of DataAnalysis class. 

---

# src/DataAnalysis.cxx

File containing all methods of [DataAnalysis](/Classes/classDataAnalysis.md) class.  [More...](#detailed-description)

## Detailed Description

File containing all methods of [DataAnalysis](/Classes/classDataAnalysis.md) class. 

**Author**: M. Montefiori and R. Zarrella 



## Source code

```cpp

#include "DataAnalysis.h"

DataAnalysis::DataAnalysis()
{
    std::cout << "Let's analyze!" << std::endl;
    _NumberOfGhosts = 0;
}


bool DataAnalysis::CheckTriggeredBars()
{
    if (std::count(std::begin(_Charge), std::end(_Charge), 0) >= 38)
    {
        //std::cout << std::count(std::begin(_Charge), std::end(_Charge), 0) << std::endl;
        return true;
    }
    
    else 
    {
        
        return false;
    }
}


void DataAnalysis::InitHistos()
{
    std::cout << "Histograms initialization" << std::endl;

    _hitmap_Channels_A = new TH1F("", "", 40, -0.5, 39.5);
    _hitmap_Channels_A->SetStats(0);
    _hitmap_Channels_A->SetFillColor(kRed);
    _hitmap_Channels_A->SetBarWidth(0.4);
    _hitmap_Channels_A->SetBarOffset(0.55);
    _hitmap_Channels_A->SetXTitle("Bar");
    _hitmap_Channels_A->SetYTitle("Counts");
    _hitmap_Channels_A->SetDirectory( fOut->GetDirectory("Hitmap channels") );

    _hitmap_Channels_B = new TH1F("", "", 40, -0.5, 39.5);
    _hitmap_Channels_B->SetStats(0);
    _hitmap_Channels_B->SetFillColor(kBlue);
    _hitmap_Channels_B->SetBarWidth(0.45);
    _hitmap_Channels_B->SetBarOffset(0.1);
    _hitmap_Channels_B->SetXTitle("Bar");
    _hitmap_Channels_B->SetYTitle("Counts");
    _hitmap_Channels_B->SetDirectory( fOut->GetDirectory("Hitmap channels") );
    

    for (Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
    {
        
        RearBar = PosID % 20;
        FrontBar = (PosID / 20) + 20;

        _hist_Charge_Front[PosID] = new TH1F(Form("Int %dx%d", FrontBar, RearBar), "", 300, 0, 30);
        _hist_Charge_Front[PosID]->SetTitle(Form("Intersection %d - %d", FrontBar, RearBar));
        _hist_Charge_Front[PosID]->SetXTitle("Charge");
        _hist_Charge_Front[PosID]->SetYTitle("Counts");
        _hist_Charge_Front[PosID]->SetDirectory( fOut->GetDirectory("Charges Front") );

        _hist_Charge_Rear[PosID] = new TH1F(Form("Int %dx%d", RearBar, FrontBar ), "", 300, 0, 30);
        _hist_Charge_Rear[PosID]->SetTitle(Form("Intersection %d - %d", RearBar, FrontBar));
        _hist_Charge_Rear[PosID]->SetXTitle("Charge");
        _hist_Charge_Rear[PosID]->SetYTitle("Counts");
        _hist_Charge_Rear[PosID]->SetDirectory( fOut->GetDirectory("Charges Rear") );

        _hist_Ampl_A_Front[PosID] = new TH1F(Form("Int_%dx%d Ch_%d", FrontBar, RearBar, 2*FrontBar), "", 400, 0, 1.5);
        _hist_Ampl_A_Front[PosID]->SetTitle(Form("Intersection %d - %d -> Channel %d", FrontBar, RearBar, 2*FrontBar));
        _hist_Ampl_A_Front[PosID]->SetXTitle("Amplitude A [V]");
        _hist_Ampl_A_Front[PosID]->SetYTitle("Counts");
        _hist_Ampl_A_Front[PosID]->SetDirectory( fOut->GetDirectory("Amplitudes Front/Left") );

        _hist_Ampl_B_Front[PosID] = new TH1F(Form("Int_%dx%d Ch_%d", FrontBar, RearBar, 2*FrontBar+1), "", 400, 0, 1.5);
        _hist_Ampl_B_Front[PosID]->SetTitle(Form("Intersection %d - %d -> Channel %d", FrontBar, RearBar, 2*FrontBar+1));
        _hist_Ampl_B_Front[PosID]->SetXTitle("Amplitude B [V]");
        _hist_Ampl_B_Front[PosID]->SetYTitle("Counts");
        _hist_Ampl_B_Front[PosID]->SetDirectory( fOut->GetDirectory("Amplitudes Front/Right") );

        _hist_Ampl_A_Rear[PosID] = new TH1F(Form("Int_%dx%d Ch_%d", RearBar, FrontBar, 2*RearBar), "", 400, 0, 1.5);
        _hist_Ampl_A_Rear[PosID]->SetDirectory( fOut->GetDirectory("Amplitudes Rear/Up") );
        _hist_Ampl_A_Rear[PosID]->SetXTitle("Amplitude A [V]");
        _hist_Ampl_A_Rear[PosID]->SetYTitle("Counts");
        _hist_Ampl_A_Rear[PosID]->SetTitle(Form("Intersection %d - %d -> Channel %d", RearBar, FrontBar, 2*RearBar));

        _hist_Ampl_B_Rear[PosID] = new TH1F(Form("Int_%dx%d Ch_%d", RearBar, FrontBar, 2*RearBar+1), "", 400, 0, 1.5);
        _hist_Ampl_B_Rear[PosID]->SetTitle(Form("Intersection %d - %d -> Channel %d", RearBar, FrontBar, 2*RearBar+1));
        _hist_Ampl_B_Rear[PosID]->SetXTitle("Amplitude B [V]");
        _hist_Ampl_B_Rear[PosID]->SetYTitle("Counts");
        _hist_Ampl_B_Rear[PosID]->SetDirectory( fOut->GetDirectory("Amplitudes Rear/Down") );

        _hist_DeltaT_AB_Front[PosID] = new TH1F(Form("Int %dx%d", FrontBar, RearBar), "", 400, -6, 6);
        _hist_DeltaT_AB_Front[PosID]->SetTitle(Form("Intersection %d - %d", FrontBar, RearBar));
        _hist_DeltaT_AB_Front[PosID]->SetXTitle("#Delta t_{AB} [ns]");
        _hist_DeltaT_AB_Front[PosID]->SetYTitle("Counts");
        _hist_DeltaT_AB_Front[PosID]->SetDirectory( fOut->GetDirectory("DeltaT_AB Front") );

        _hist_DeltaT_AB_Rear[PosID] = new TH1F(Form("Int %dx%d", RearBar, FrontBar ), "", 400, -6, 6);
        _hist_DeltaT_AB_Rear[PosID]->SetTitle(Form("Intersection %d - %d", RearBar, FrontBar));
        _hist_DeltaT_AB_Rear[PosID]->SetXTitle("#Delta t_{AB} [ns]");
        _hist_DeltaT_AB_Rear[PosID]->SetYTitle("Counts");
        _hist_DeltaT_AB_Rear[PosID]->SetDirectory( fOut->GetDirectory("DeltaT_AB Rear") );
    }

    _hitmap_DeltaT_Front = new TH2F("TimeRes_Front", "DeltaT_AB resolution Front Layer", 20, -0.5, 19.5, 20, 19.5, 39.5);
    _hitmap_DeltaT_Front->SetStats(0);
    _hitmap_DeltaT_Front->SetXTitle("Rear Bar");
    _hitmap_DeltaT_Front->SetYTitle("Front Bar");
    _hitmap_DeltaT_Front->SetOption("colz");
    _hitmap_DeltaT_Front->SetDirectory( fOut->GetDirectory("DeltaT_AB calibration") );

    _hitmap_DeltaT_Rear = new TH2F("TimeRes_Rear", "DeltaT_AB resolution Rear Layer", 20, -0.5, 19.5, 20, 19.5, 39.5);
    _hitmap_DeltaT_Rear->SetStats(0);
    _hitmap_DeltaT_Rear->SetXTitle("Rear Bar");
    _hitmap_DeltaT_Rear->SetYTitle("Front Bar");
    _hitmap_DeltaT_Rear->SetOption("colz");
    _hitmap_DeltaT_Rear->SetDirectory( fOut->GetDirectory("DeltaT_AB calibration") );

}


void DataAnalysis::SetOutputStructures(TTree* t)
{
    t->SetBranchStatus("*", 0);

    t->SetBranchStatus("BAR_Charge", 1);
    t->SetBranchStatus("BAR_ChargeA", 1);
    t->SetBranchStatus("BAR_ChargeB", 1);
    t->SetBranchStatus("BAR_AmpA", 1);
    t->SetBranchStatus("BAR_AmpB", 1);
    t->SetBranchStatus("BAR_DeltaT_AB", 1);

    t->SetBranchAddress("BAR_Charge", _Charge);
    t->SetBranchAddress("BAR_ChargeA", _Charge_A);
    t->SetBranchAddress("BAR_ChargeB", _Charge_B);
    t->SetBranchAddress("BAR_AmpA", _Ampl_A);
    t->SetBranchAddress("BAR_AmpB", _Ampl_B);
    t->SetBranchAddress("BAR_DeltaT_AB", _DeltaT_AB);
}


void DataAnalysis::FillHistograms()
{
    for (Int_t IdBar = 0; IdBar < NUMBEROFTWBARS; ++IdBar)
    {
        if (_Charge_A[IdBar] !=0) _hitmap_Channels_A->Fill(IdBar); 
        if (_Charge_B[IdBar] !=0) _hitmap_Channels_B->Fill(IdBar); 
                    
        
    }

    for (Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
        {       
        RearBar = PosID % 20;
        FrontBar = (PosID / 20) + 20;
        
        if (_Charge[RearBar] != 0 && _Charge[FrontBar] != 0) 
        {
                _hist_Charge_Front[PosID]->Fill(_Charge[FrontBar]);
                _hist_Charge_Rear[PosID]->Fill(_Charge[RearBar]);
        }

        if (_Ampl_A[RearBar] != 0 && _Ampl_B[RearBar] != 0) // and check chrge front !=0
        {
            if (_Charge[FrontBar] != 0)
            {
                _hist_Ampl_A_Rear[PosID]->Fill(-_Ampl_A[RearBar]);
                _hist_Ampl_B_Rear[PosID]->Fill(-_Ampl_B[RearBar]);
            }
            
        }
        if (_Ampl_A[FrontBar] != 0 && _Ampl_B[FrontBar] != 0) // and check chrge rear !=0
        {
            if (_Charge[RearBar] != 0)
            {
                _hist_Ampl_A_Front[PosID]->Fill(-_Ampl_A[FrontBar]);
                _hist_Ampl_B_Front[PosID]->Fill(-_Ampl_B[FrontBar]);
            }
            
        }  
            
        if (_DeltaT_AB[FrontBar] != 0 && _DeltaT_AB[RearBar] != 0)   
        {
            _hist_DeltaT_AB_Front[PosID]->Fill(_DeltaT_AB[FrontBar]);
            _hist_DeltaT_AB_Rear[PosID]->Fill(_DeltaT_AB[RearBar]);
        }           
        }
    
}


TF1* DataAnalysis::FitGauss(TH1F* hist)
{
    TCanvas* c = new TCanvas();
    TF1* FitFunc = new TF1("fitfunc", "[0]*TMath::Gaus(x, [1], [2])");
    Double_t a, mu, sigma;
    a = hist->GetMaximum();
    mu = hist->GetBinCenter(hist->GetMaximumBin());
    sigma = 0.1;
    FitFunc->SetParameters(a, mu, sigma);
    hist->Fit(FitFunc, "q", "", mu - 4*sigma, mu + 4*sigma);
    delete c;
    return FitFunc;
}


void DataAnalysis::AnalyzeDeltaT()
{
    for (Int_t IdBar = 0; IdBar < NUMBEROFTWBARS; ++IdBar)
    {
        _DeltaT_AB_Bar[IdBar] = new TGraphErrors();
        _DeltaT_AB_Bar[IdBar]->GetXaxis()->SetTitle("Distance from center [cm]");
        _DeltaT_AB_Bar[IdBar]->GetYaxis()->SetTitle("#Delta t_{AB} [ns]");
        _DeltaT_AB_Bar[IdBar]->SetTitle(Form("Bar %d", IdBar));
        
    }
    
    for (Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
    {
    fOut->cd("DeltaT_AB calibration");
    TF1* FitFunc_Front = FitGauss(_hist_DeltaT_AB_Front[PosID]);
    TF1* FitFunc_Rear = FitGauss(_hist_DeltaT_AB_Rear[PosID]);
    RearBar = PosID % 20;
    FrontBar = (PosID / 20) + 20;
    Double_t PosX_Front = (2 * RearBar + 1) - 20;
    Double_t PosX_Rear =  (2 * (FrontBar-20) + 1) -20;
    _DeltaT_AB_Bar[FrontBar]->SetPoint(_DeltaT_AB_Bar[FrontBar]->GetN(), PosX_Front, FitFunc_Front->GetParameter(1));
    _DeltaT_AB_Bar[RearBar]->SetPoint(_DeltaT_AB_Bar[RearBar]->GetN(), PosX_Rear, FitFunc_Rear->GetParameter(1));
    _DeltaT_AB_Bar[FrontBar]->SetPointError(_DeltaT_AB_Bar[FrontBar]->GetN()-1, 0, FitFunc_Front->GetParError(1));
    _DeltaT_AB_Bar[RearBar]->SetPointError(_DeltaT_AB_Bar[RearBar]->GetN()-1, 0, FitFunc_Rear->GetParError(1));

    _hitmap_DeltaT_Front->SetBinContent(RearBar+1, FrontBar-19, FitFunc_Front->GetParameter(2));
    _hitmap_DeltaT_Rear->SetBinContent(RearBar+1, FrontBar-19, FitFunc_Rear->GetParameter(2));
    }
    TF1* Line = new TF1("", "[0]+[1]*x", -3, 3);
    Line->SetLineWidth(2);
    Line->SetLineColor(kRed);  
    
    for (Int_t IdBar = 0; IdBar < NUMBEROFTWBARS; ++IdBar)
    {
        _DeltaT_AB_Bar[IdBar]->SetTitle(Form("Bar %d", IdBar));
        _DeltaT_AB_Bar[IdBar]->SetMarkerStyle(7);
        _DeltaT_AB_Bar[IdBar]->Fit(Line, "q");
        _DeltaT_AB_Bar[IdBar]->Write("Bar ");
        delete _DeltaT_AB_Bar[IdBar];
        
    }
}


void DataAnalysis::DoAll(TString InputFileName, TString OutputFileName)
{
    TFile *inputFile = TFile::Open(InputFileName.Data(), "r");
    if (inputFile == nullptr || inputFile->IsZombie())
    {
        Error("DataAnalysis()", "Can not open input file");
        throw -1;
    }

    //TString fOutName = "/home/marco/Desktop/datacosm/Prova_Class.root";
    std::cout << Form("Analysing data from %s", InputFileName.Data()) << std::endl;
    fOut = new TFile(OutputFileName.Data(), "RECREATE");
    gDirectory->mkdir("Charges Front");
    gDirectory->mkdir("Charges Rear");
    gDirectory->mkdir("Amplitudes Rear/Up");
    gDirectory->mkdir("Amplitudes Rear/Down");
    gDirectory->mkdir("Amplitudes Front/Left");
    gDirectory->mkdir("Amplitudes Front/Right");
    gDirectory->mkdir("DeltaT_AB Front");
    gDirectory->mkdir("DeltaT_AB Rear");
    gDirectory->mkdir("DeltaT_AB calibration");
    gDirectory->mkdir("Hitmap channels");

    TTree *t;
    inputFile->GetObject("rec_tree", t);
    SetOutputStructures(t);
    InitHistos();
    
    std::cout << "Analysis running" << std::endl;
    for (Int_t i = 0; i < t->GetEntries(); ++i)
    {
        t->GetEntry(i);
        /*        
        if (!CheckTriggeredBars()) 
        {
    
            
            ++_NumberOfGhosts;
            continue;
        }
        */
        FillHistograms();
    }
    TCanvas* c = new TCanvas();
    _hitmap_Channels_A->GetYaxis()->SetLimits(6500, 10500);
    _hitmap_Channels_B->GetYaxis()->SetLimits(6500, 10500);
    _hitmap_Channels_A->Draw("bar");
    _hitmap_Channels_B->Draw("bar, same");
    TLegend* l = new TLegend(0.9, 0.7, 0.6, 0.9);
    l->AddEntry(_hitmap_Channels_A, "Channel A (left/up)");
    l->AddEntry(_hitmap_Channels_B, "Channel B (right/down)");
    l->Draw("same");
    fOut->cd("Hitmap channels");
    c->Write();
    delete c;
    delete _hitmap_Channels_A;
    delete _hitmap_Channels_B;
    AnalyzeDeltaT();
    std::cout << Form("Saving results in %s", OutputFileName.Data()) << std::endl;
    fOut->Write();
    fOut->Close();
}
```


-------------------------------

Updated on 2022-03-05 at 18:47:21 +0000
