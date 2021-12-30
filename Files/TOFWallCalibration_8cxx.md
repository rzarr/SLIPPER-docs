---
title: src/TOFWallCalibration.cxx
summary: File containing all methods of TOFWallCalibration class. 

---

# src/TOFWallCalibration.cxx

File containing all methods of [TOFWallCalibration](/Classes/classTOFWallCalibration.md) class.  [More...](#detailed-description)

## Detailed Description

File containing all methods of [TOFWallCalibration](/Classes/classTOFWallCalibration.md) class. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "TOFWallCalibration.h"

TOFWallCalibration::TOFWallCalibration()
{
    _funcdECal = new TF1("funcdECal", "[0]*x/(1 + [1]*x)", DEMIN, DEMAX);
    _funcdECal->SetParLimits(0, 0., 2);
    _funcdECal->SetParLimits(1, 0., .1);

    CalculatePosIDtoBarsMap();
    _Debug = false;
};


void TOFWallCalibration::RunCalibration(TString OutputDir)
{
    EnergyCalibration(OutputDir);
    TOFCalibration(OutputDir);

    Message::DisplayMessageWithEmphasys("Calibration done!");
    Message::DisplayMessageWithEmphasys("Calibration maps written to output directory");

    // if(_Debug)
    // {
    //   Message::DisplayMessageWithEmphasys("Saving Q and TOF histograms in SHOE format");
    //   SaveRawHistograms(OutputDir);
    //   Message::DisplayMessageWithEmphasys("Done");
    // }

    Message::DisplayMessageWithEmphasys("Clearing data");
    ClearData(LayerX);
    ClearData(LayerY);
    Message::DisplayMessageWithEmphasys("Done");
}


void TOFWallCalibration::EnergyCalibration(TString OutputDir)
{
    gStyle->SetOptStat(0);

    Message::DisplayMessageWithEmphasys("Performing Energy calibration");

    //Declare a file where raw histograms and calibration curves are saved in debug mode
    TFile* fOut;
    if(_Debug){fOut = TFile::Open(Form("%s/EnergyCalibrationDEBUG.root",OutputDir.Data()),"RECREATE");}

    std::ofstream* ofsSHOE = new std::ofstream(Form("%s/EnergyCalMapSHOE.txt", OutputDir.Data()));

    (*ofsSHOE) << "#position\tbarId_LayerX\tbarId_LayerY\tP0[V*ns/MeV]\tP1[1/MeV]\tlayer(SHOE)\n";

    CalibrateLayerDeltaE(ofsSHOE, LayerX, OutputDir, fOut);
    CalibrateLayerDeltaE(ofsSHOE, LayerY, OutputDir, fOut);

    //Close all the output files
    if(_Debug){fOut->Close();}
    ofsSHOE->close();

    Message::DisplayMessageWithEmphasys("Done");
}


void TOFWallCalibration::CalibrateLayerDeltaE(std::ofstream *ofsSHOE, TLayer layer, TString OutputDir, TFile* fOut)
{
    //Variables used for the loop on beams and TW positions
    PartEnPairType PartEnPair;
    Float_t mean, sigma;
    Float_t p0, p1; //Birks parameters
    Bool_t gsiFlag; //flags that check if a position has GSI data or not
    Int_t flag, layerSHOE; //flag for calibration reliability

    //Open the files where energy cal maps are stored -> debug mode saves single layer maps
    std::ofstream* ofsLayer;
    if(_Debug)
    {
        ofsLayer = new std::ofstream(Form("%s/EnergyCalMap%s.txt", OutputDir.Data(), LayerName.at(layer).c_str()));
        (*ofsLayer) << "#position\tbarId_LayerX\tbarId_LayerY\tP0[V*ns/MeV]\tP1[1/MeV]\tlayer(SHOE)\tflag\n";
    }

    //Declare a function for gaussian fits
    TF1* histfit = new TF1("histfit", "gaus", QMIN, QMAX);

    //Cycle on TW positions and calibrate the 2 layers
    for(Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
    {
        //Create some directories in the debug file
        if(_Debug)
        {
            if(!fOut->GetDirectory(Form("Pos%d",PosID)))
            {
                fOut->mkdir(Form("Pos%d",PosID));
            }
            if(!fOut->GetDirectory(Form("Pos%d/%s",PosID,LayerName.at(layer).c_str())))
            {
                fOut->mkdir(Form("Pos%d/%s",PosID,LayerName.at(layer).c_str()));
            }

            fOut->cd(Form("Pos%d/%s",PosID,LayerName.at(layer).c_str()));
        }

        //Declare the dE_MC vd Q_raw graphs
        TGraphErrors* grLayer = new TGraphErrors();

        //Initialize the GSI flags to false
        gsiFlag = false;
        for(auto itBeam = _PartEnPairsData.begin(); itBeam != _PartEnPairsData.end(); ++itBeam)
        {
            //Check if the position has enough data for that beam and perform the fit
            //to find the mean value of raw Q
            if(_hQ[layer].at(*itBeam).at(PosID)->GetEntries() > 50)
            {
                //Set the parameters of the gaussian function and fit the Qraw histogram
                mean = _hQ[layer].at(*itBeam).at(PosID)->GetBinCenter(_hQ[layer].at(*itBeam).at(PosID)->GetMaximumBin());
                sigma = _hQ[layer].at(*itBeam).at(PosID)->GetStdDev();

                histfit->SetParameters(_hQ[layer].at(*itBeam).at(PosID)->GetMaximum(), mean, sigma);
                _hQ[layer].at(*itBeam).at(PosID)->Fit(histfit, "Q0", "", mean - 4*sigma, mean + 4*sigma);

                //Increase the number of points and save mean value + error (rn sigma) in the tgraph
                grLayer->Set(grLayer->GetN() + 1);
                grLayer->SetPoint(grLayer->GetN()-1, _MCRef.at(*itBeam).dE_MC.at(layer), histfit->GetParameter(1));
                grLayer->SetPointError(grLayer->GetN()-1, 0., histfit->GetParameter(2));

                //Set GSI flag to true if the beam is found in that position
                if((*itBeam).first == Oxygen){gsiFlag = true;}
            }

            //Save all the Q_{raw} histograms and gaussian fits if debug mode is activated
            if(_Debug)
            {
                TF1* fit = (TF1*) histfit->Clone();
                TCanvas* c1 = new TCanvas("","",1000,800);
                _hQ[layer].at(*itBeam).at(PosID)->SetTitle(Form("Qraw%s_Part%d_En%.1lf;Q_{raw} [V*ns];Entries", LayerName.at(layer).c_str(), (*itBeam).first, (*itBeam).second));
                _hQ[layer].at(*itBeam).at(PosID)->SetMarkerStyle(20);
                _hQ[layer].at(*itBeam).at(PosID)->SetMarkerSize(1.2);
                _hQ[layer].at(*itBeam).at(PosID)->Draw();
                fit->SetLineWidth(2);
                fit->SetLineColor(kRed);
                if(_hQ[layer].at(*itBeam).at(PosID)->GetEntries() > 50) {fit->Draw("same");}

                c1->Write(Form("Qraw_Part%d_En%1.lf", (*itBeam).first, (*itBeam).second));
                delete fit;
                delete c1;
            }
        }

        //Initialize to 0 -> data written if no fit is performed
        flag = 0;
        layerSHOE = int(layer);
        p0 = 0;
        p1 = 0;

        //Sort TGraph data points
        grLayer->Sort();

        //Perform the fit of the light output model for both layers
        //First, check if there's enough points to fit
        if(grLayer->GetN() >= 3)
        {
        //Reset the parameters to likely values and fit
            _funcdECal->SetParameters(.5, 1E-2);
            grLayer->Fit(_funcdECal, "Q0", "", DEMIN, DEMAX);

            //Save the fit parameters
            p0 = _funcdECal->GetParameter(0);
            p1 = _funcdECal->GetParameter(1);

            //Check if the fit was successful
            if(_funcdECal->GetChisquare()/(grLayer->GetN()-2) > 3){flag =  3;}
            //Check if GSI data have been acquired in the position
            else{flag = gsiFlag ? 1 : 2;}
        }

        //Save the canvas with the TGraph and calibration curves if in debug mode
        if(_Debug)
        {
            TF1* fit = (TF1*) _funcdECal->Clone();
            TCanvas* c1 = new TCanvas("","",1000,800);
            TH2D* hist = new TH2D("", "", 10, -1., DEMAX, 10, -1., QMAX);
            hist->SetTitle(Form("EnCalCurve%s_Pos%d_flag%d;#Delta E_{MC} [MeV];Q_{raw} [V*ns]", LayerName.at(layer).c_str(), PosID, flag));
            hist->Draw();
            grLayer->SetMarkerStyle(20);
            grLayer->SetMarkerSize(1.2);
            grLayer->Draw("P same");
            fit->SetLineWidth(2);
            fit->SetLineColor(kRed);
            if(grLayer->GetN() >= 3) {fit->Draw("same");}

            c1->Write(Form("EnCalCurve%s_flag%d", LayerName.at(layer).c_str(), flag));
            delete fit;
            delete c1;
            delete hist;
        }

        //Write to output file(s)
        (*ofsSHOE) << Form("%d\t%d\t%d\t%f\t%f\t%d\n", PosID, _PosIDtoXYBarsMap.at(PosID).first, _PosIDtoXYBarsMap.at(PosID).second, p0, p1, layerSHOE);

        if(_Debug)
        {
            (*ofsLayer) << Form("%d\t%d\t%d\t%f\t%f\t%d\t%d\n", PosID, _PosIDtoXYBarsMap.at(PosID).first, _PosIDtoXYBarsMap.at(PosID).second, p0, p1, layerSHOE, flag);
        }

        //Delete the graphs at the end of the cycle on the position
        delete grLayer;
    }

    if(_Debug){ofsLayer->close();}
}


void TOFWallCalibration::TOFCalibration(TString OutputDir)
{
    gStyle->SetOptStat("neMR");
    Message::DisplayMessageWithEmphasys("Performing TOF calibration");

    //Declare pointer to file where debug histograms are saved
    TFile* fOut;
    if(_Debug){fOut = TFile::Open(Form("%s/TOFCalibrationDEBUG.root",OutputDir.Data()),"RECREATE");}

    //Cycle on each beam found in data -> TOF calibration is beam-dependent
    for(auto itBeam = _PartEnPairsData.begin(); itBeam != _PartEnPairsData.end(); ++itBeam)
    {
        std::ofstream* ofsSHOE = new std::ofstream(Form("%s/TOFCalMapSHOEPart%dEn%.1lf.txt", OutputDir.Data(), (*itBeam).first, (*itBeam).second));
        (*ofsSHOE) << "#position\tbarId_LayerX\tbarId_LayerY\tdeltaT[ns]\tdeltaT2[ns]\tlayer(SHOE)\n";

        CalibrateLayerTOF(ofsSHOE, *itBeam, LayerX, OutputDir, fOut);
        CalibrateLayerTOF(ofsSHOE, *itBeam, LayerY, OutputDir, fOut);

        ofsSHOE->close();
    }

    //Close the debug file
    if(_Debug){fOut->Close();}

    Message::DisplayMessageWithEmphasys("Done");
}


void TOFWallCalibration::CalibrateLayerTOF(std::ofstream *ofsSHOE, PartEnPairType PartEn, TLayer layer, TString OutputDir, TFile* fOut)
{
    //Initialize the function used to find the mean TOF_raw values and some
    //Useful variables for the cycle
    TF1* funcTOFCal = new TF1("funcTOFcal", "gaus", TOFMIN, TOFMAX);
    funcTOFCal->SetParLimits(1, TOFMIN, TOFMAX);
    funcTOFCal->SetParLimits(2, 0., 0.4); //Sigma of the gaussian from 0 to 400 ps
    Int_t flag, layerSHOE;
    Float_t mean, sigma, TOFcorrection, DeltaT2;

    //Create a debug ofstream for single layer calibration maps
    //and make histograms directories in the debug file
    std::ofstream* ofsLayer;
    if(_Debug)
    {
        ofsLayer = new std::ofstream(Form("%s/TOFCalMap%sPart%dEn%.1lf.txt", OutputDir.Data(), LayerName.at(layer).c_str(), PartEn.first, PartEn.second));
        (*ofsLayer) << "#position\tbarId_LayerX\tbarId_LayerY\tdeltaT[ns]\tdeltaT2[ns]\tlayer(SHOE)\tflag\n";

        if(!fOut->GetDirectory(Form("Part%dEn%.1lf", PartEn.first, PartEn.second)))
        {
            fOut->mkdir(Form("Part%dEn%.1lf", PartEn.first, PartEn.second));
        }
        if(!fOut->GetDirectory(Form("Part%dEn%.1lf/%s", PartEn.first, PartEn.second, LayerName.at(layer).c_str())))
        {
            fOut->mkdir(Form("Part%dEn%.1lf/%s", PartEn.first, PartEn.second, LayerName.at(layer).c_str()));
        }

        fOut->cd(Form("Part%dEn%.1lf/%s", PartEn.first, PartEn.second, LayerName.at(layer).c_str()));
    }

    //Cycle on the TW positions
    for(Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
    {
        //Set flag and TOFcorrection to 0
        flag = 0;
        layerSHOE = int(layer);
        TOFcorrection = 0.;
        DeltaT2 = 0.;

        //Check if the position has enough statistics to perform the calibration
        if(_hTOF[layer].at(PartEn).at(PosID)->GetEntries() > 50)
        {
            //Get the initial values for the fit
            mean = _hTOF[layer].at(PartEn).at(PosID)->GetBinCenter(_hTOF[layer].at(PartEn).at(PosID)->GetMaximumBin());
            sigma = _hTOF[layer].at(PartEn).at(PosID)->GetStdDev();

            //Set the initial values and fit TOF_raw distribution
            funcTOFCal->SetParameters(_hTOF[layer].at(PartEn).at(PosID)->GetMaximum(), mean, sigma);
            _hTOF[layer].at(PartEn).at(PosID)->Fit(funcTOFCal, "Q0", "", mean - 4*sigma, mean + 4*sigma);

            //Calculate the TOF correction as the difference between raw and MC mean values and set the flag
            TOFcorrection = funcTOFCal->GetParameter(1) - _MCRef.at(PartEn).TOF_MC.at(layer);
            flag = 1;
        }

        //Save histograms and gaussian fits if in debug mode
        if(_Debug)
        {
            TF1* fit = (TF1*) funcTOFCal->Clone();
            TCanvas* c1 = new TCanvas("","",1000,800);
            _hTOF[layer].at(PartEn).at(PosID)->SetTitle(Form("TOFraw%s_Pos%d_flag%d;TOF_{raw} [ns];Entries", LayerName.at(layer).c_str(), PosID, flag));
            _hTOF[layer].at(PartEn).at(PosID)->SetMarkerStyle(20);
            _hTOF[layer].at(PartEn).at(PosID)->SetMarkerSize(1.2);
            _hTOF[layer].at(PartEn).at(PosID)->Draw();
            fit->SetLineWidth(2);
            fit->SetLineColor(kRed);
            if(flag){fit->Draw("same");}

            c1->Write(Form("TOFrawPos%d_flag%d", PosID, flag));
            delete fit;
            delete c1;
        }

        //Write to output file
        (*ofsSHOE) << Form("%d\t%d\t%d\t%f\t%f\t%d\n", PosID, _PosIDtoXYBarsMap.at(PosID).first, _PosIDtoXYBarsMap.at(PosID).second, TOFcorrection, DeltaT2, layerSHOE);

        if(_Debug)
        {
            (*ofsLayer) << Form("%d\t%d\t%d\t%f\t%f\t%d\t%d\n", PosID, _PosIDtoXYBarsMap.at(PosID).first, _PosIDtoXYBarsMap.at(PosID).second, TOFcorrection, DeltaT2, layerSHOE, flag);
        }
    }

    //Close TOF calibration maps for the current beam
    if(_Debug){ofsLayer->close();}
}


void TOFWallCalibration::LoadRecData(TString InputDataDir)
{
    //Initialize the histograms here using the list of beams found in the MC table
    InitHists(LayerX);
    InitHists(LayerY);

    //Get the list of .rec.root files in InputDataDir and read them one by one
    if(InputDataDir.EndsWith("/")){InputDataDir.Remove(TString::kTrailing, '/');}
    Int_t FileCount = 0;
    TString ext = ".rec.root";
    TSystemDirectory dir(InputDataDir, InputDataDir);
    TList *files = dir.GetListOfFiles();
    if(files)
    {
        TSystemFile *file;
        TString fname;
        TIter next(files);
        while((file=(TSystemFile*)next()))
        {
            fname = Form("%s/%s",dir.GetName(), file->GetName());
            if (!file->IsDirectory() && fname.EndsWith(ext))
            {
                //If the file is found, read it and increase counter
                FileCount++;
                LoadSingleFileData(fname);
            }
        }
    }

    //Throw an error if no data was found, otherwise print some information
    if(!FileCount)
    {
        Error("LoadRecData()", "No ROOT (*.rec.root) file found in %s", dir.GetName());
        throw -1;
    }

    Message::DisplayMessageWithEmphasys("Found data for the beams:");
    for(auto itBeam = _PartEnPairsData.begin(); itBeam != _PartEnPairsData.end(); ++itBeam)
    {
        Message::DisplayMessage(Form("Primary: %s\tEnergy: %.3lf GeV/u", ParticleName.at((*itBeam).first).c_str(), (*itBeam).second));
    }
}


void TOFWallCalibration::LoadSingleFileData(TString FileName)
{
    //Open file
    TFile* InputFile = TFile::Open(FileName);
    if(InputFile->IsZombie() || !InputFile->IsOpen())
    {
        Error("LoadSingleFileData()", "Cannot open input file %s", FileName.Data());
        throw -1;
    }

    //Get data tree
    TTree* InputTree;
    InputFile->GetObject("rec_tree", InputTree);
    if(InputTree==nullptr)
    {
        Error("LoadSingleFileData()", "Error opening file: %s", FileName.Data());
        throw -1;
    }

    //Activate only the needed branches
    InputTree->SetBranchStatus("*",0);
    InputTree->SetBranchStatus("BAR_Charge",1);
    InputTree->SetBranchStatus("BAR_TOF_Uncal",1);
    InputTree->SetBranchStatus("Tags",1);

    //Set the address for some variables
    Float_t Qtree[NUMBEROFTWBARS], TOFtree[NUMBEROFTWBARS];
    WDTag Tags;
    InputTree->SetBranchAddress("BAR_Charge", &Qtree[0]);
    InputTree->SetBranchAddress("BAR_TOF_Uncal", &TOFtree[0]);
    InputTree->SetBranchAddress("Tags", &Tags);

    //Variabes used to save the data in the correct histogram
    Int_t XBar, YBar, PosID, NHits;
    PartEnPairType PartEnPair;

    Message::DisplayMessage(Form("Found %lld events in file %s", InputTree->GetEntries(), FileName.Data()));

    //Set the beam type for the opened file and check if it was found in the MC table
    //If not, throw an error
    InputTree->GetEntry(0);
    PartEnPair = std::make_pair(Tags.PrimaryParticle, Tags.BeamEnergy);
    if(std::find(_PartEnPairsMC.begin(), _PartEnPairsMC.end(), PartEnPair) == _PartEnPairsMC.end())
    {
        Error("LoadSingleFileData()","Found data for beam missing in the MC table: PartID %d\t En = %.3lf GeV/u", PartEnPair.first, PartEnPair.second);
        throw -1;
    }

    //Store the beam type in the _PartEnPairsData if it was not found before
    //Used only to print out the beams found in data at run time
    if(std::find(_PartEnPairsData.begin(), _PartEnPairsData.end(), PartEnPair) == _PartEnPairsData.end())
    {
        _PartEnPairsData.push_back(PartEnPair);
    }

    for(Int_t entry=0; entry < InputTree->GetEntries(); ++entry)
    {
        InputTree->GetEntry(entry);

        NHits = 0;
        for(Int_t xb = LAYERXBARMIN; xb <= LAYERXBARMAX; ++xb)
        {
            //Skip if either the x or y bar was not hit
            if(Qtree[xb] <= .5 || TOFtree[xb] <= 0){continue;}
            for(Int_t yb = LAYERYBARMIN; yb <= LAYERYBARMAX; ++yb)
            {
                if(Qtree[yb] <= .5 || TOFtree[yb] <= 0){continue;}

                //The position has been hit -> store bar number and increase number of hits
                NHits ++;
                XBar = xb;
                YBar = yb;
            }
        }

        //Save data to histograms if one position was hit -> clean events only!
        if(NHits == 1)
        {
            PosID = CalculatePositionID(XBar, YBar);
            _hQ[LayerX].at(PartEnPair).at(PosID)->Fill(Qtree[XBar]);
            _hQ[LayerY].at(PartEnPair).at(PosID)->Fill(Qtree[YBar]);
            _hTOF[LayerX].at(PartEnPair).at(PosID)->Fill(TOFtree[XBar]);
            _hTOF[LayerY].at(PartEnPair).at(PosID)->Fill(TOFtree[YBar]);
        }
    }

    InputFile->Close();
}


void TOFWallCalibration::InitHists(TLayer layer)
{
    //Cycle on the beams found in the MC table
    for(auto itBeam = _PartEnPairsMC.begin(); itBeam != _PartEnPairsMC.end(); ++itBeam)
    {
        //Cycle on the TW positions
        for(Int_t PosID=0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
        {
            //Allocate memory for all the histograms
            _hQ[layer][*itBeam].push_back(new TH1F(Form("hQ%s-PartID%d-En%.3lf-Pos%d", LayerName.at(layer).c_str(), (*itBeam).first, (*itBeam).second, PosID), Form("hQ%s-PartID%d-En%.3lf-Pos%d", LayerName.at(layer).c_str(), (*itBeam).first, (*itBeam).second, PosID), QBINS, QMIN, QMAX));

            _hTOF[layer][*itBeam].push_back(new TH1F(Form("hTOF%s-PartID%d-En%.3lf-Pos%d", LayerName.at(layer).c_str(), (*itBeam).first, (*itBeam).second, PosID), Form("hTOF%s-PartID%d-En%.3lf-Pos%d", LayerName.at(layer).c_str(), (*itBeam).first, (*itBeam).second, PosID), TOFBINS, TOFMIN, TOFMAX));
        }
    }
}


void TOFWallCalibration::LoadMCRefValues(TString MCRefValuesFile)
{
    Int_t partType;
    Float_t BeamEn, dEx, dEy, TOFx, TOFy;

    //Open the MC table
    FILE* fMCRefValues = fopen(MCRefValuesFile, "r");
    if(fMCRefValues == NULL)
    {
        Error("LoadMCRefValues()", "MC Table not found! Path given %s", MCRefValuesFile.Data());
        throw -1;
    }

    Message::DisplayMessageWithEmphasys("MC reference values for Calibration");
    Message::DisplayMessage("pID\tBeamEn\tdEx\tdEy\tTOFx\tTOFy");
    Message::DisplayMessage(" \t[GeV/u]\t[MeV]\t[MeV]\t[ns]\t[ns]");
    Message::DisplayMessage("----------------------------------------------------");

    Char_t line[100];
    PartEnPairType PartEnPair;
    while(fgets(line, sizeof(line), fMCRefValues))
    {
        if(line[0] == '#' || line[0] == '\n'){continue;}
        std::sscanf(line, "%d %f %f %f %f %f", &partType, &BeamEn, &dEx, &dEy, &TOFx, &TOFy);
        PartEnPair = std::make_pair(static_cast<ParticleType>(partType), BeamEn);
        _PartEnPairsMC.push_back(PartEnPair);

        _MCRef[PartEnPair].dE_MC[LayerX] = dEx;
        _MCRef[PartEnPair].dE_MC[LayerY] = dEy;
        _MCRef[PartEnPair].TOF_MC[LayerX] = TOFx;
        _MCRef[PartEnPair].TOF_MC[LayerY] = TOFy;

        //Print out the info from MC table
        std::cout << PartEnPair.first << "\t" << PartEnPair.second << "\t" << _MCRef.at(PartEnPair).dE_MC.at(LayerX) << "\t" << _MCRef.at(PartEnPair).dE_MC.at(LayerY) << "\t" << _MCRef.at(PartEnPair).TOF_MC.at(LayerX) << "\t" << _MCRef.at(PartEnPair).TOF_MC.at(LayerY) << std::endl;
    }

    fclose(fMCRefValues);
}


void TOFWallCalibration::SaveRawHistograms(TString OutputDir)
{
    Int_t PosID;
    PartEnPairType PartEnPair;
    TString Exp, run;
    for(auto itBeam = _PartEnPairsData.begin(); itBeam != _PartEnPairsData.end(); ++itBeam)
    {
        switch((*itBeam).first)
        {
            case Proton:
                Exp = "CNAO";
                run = "0001";
                break;
            case Carbon:
                Exp = "CNAO";
                if((*itBeam).second == 0.115) run = "0002";
                else if((*itBeam).second == 0.260) run = "0003";
                else if((*itBeam).second == 0.400) run = "0004";
                else
                {
                Error("SaveRawHistograms()", "Unrecognized carbon run, Energy is %.3lf", (*itBeam).second);
                throw -1;
                }
                break;
            case Oxygen:
                Exp = "GSI";
                run = "2242";
                break;

            default:
                Error("SaveRawHistograms()", "Run not recognized! PartID %d, Energy %.3lf", (*itBeam).first, (*itBeam).second);
                throw -1;
                break;
        }

        TString FileName = Form("%s/dE-TOF_Calib_%s_run%s.root", OutputDir.Data(), Exp.Data(), run.Data());
        TFile* fOut = TFile::Open(FileName,"RECREATE");
        fOut->mkdir("TW");
        fOut->cd("TW");
        for(PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
        {
            _hQ[LayerX].at(*itBeam).at(PosID)->SetTitle(Form("hQ%s-PartID%d-En%.3lf-Pos%d;Q [V*ns];Entries", LayerName.at(LayerX).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hQ[LayerY].at(*itBeam).at(PosID)->SetTitle(Form("hQ%s-PartID%d-En%.3lf-Pos%d;Q [V*ns];Entries", LayerName.at(LayerY).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hTOF[LayerX].at(*itBeam).at(PosID)->SetTitle(Form("hTOF%s-PartID%d-En%.3lf-Pos%d;TOF_{raw} [ns];Entries", LayerName.at(LayerX).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hTOF[LayerX].at(*itBeam).at(PosID)->SetTitle(Form("hTOF%s-PartID%d-En%.3lf-Pos%d;TOF_{raw} [ns];Entries", LayerName.at(LayerX).c_str(), (*itBeam).first, (*itBeam).second, PosID));

            _hQ[LayerX].at(*itBeam).at(PosID)->Write(Form("hQ%s-PartID%d-En%.3lf-Pos%d", LayerName.at(LayerX).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hQ[LayerY].at(*itBeam).at(PosID)->Write(Form("hQ%s-PartID%d-En%.3lf-Pos%d", LayerName.at(LayerY).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hTOF[LayerX].at(*itBeam).at(PosID)->Write(Form("hTOF%s-PartID%d-En%.3lf-Pos%d", LayerName.at(LayerX).c_str(), (*itBeam).first, (*itBeam).second, PosID));
            _hTOF[LayerY].at(*itBeam).at(PosID)->Write(Form("hTOF%s-PartID%d-En%.3lf-Pos%d", LayerName.at(LayerY).c_str(), (*itBeam).first, (*itBeam).second, PosID));
        }
        fOut->cd("..");
        fOut->Close();
    }
}


Int_t TOFWallCalibration::CalculatePositionID(Int_t XBar, Int_t YBar)
{
    if(XBar < LAYERXBARMIN || XBar > LAYERXBARMAX)
    {
        Error("CalculatePositionID()", "XBar index out of bounds (%d, %d)", LAYERXBARMIN, LAYERXBARMAX);
        throw -1;
    }
    if(YBar < LAYERYBARMIN || YBar > LAYERYBARMAX)
    {
        Error("CalculatePositionID()", "YBar index out of bounds (%d, %d)", LAYERYBARMIN, LAYERYBARMAX);
        throw -1;
    }
    return (XBar - 20)*20 + YBar;
}


void TOFWallCalibration::CalculatePosIDtoBarsMap()
{
    //Cycle on the X-Y bars and calculate the PosID
    for(Int_t XBar = LAYERXBARMIN; XBar <= LAYERXBARMAX; ++XBar)
    {
        for(Int_t YBar = LAYERYBARMIN; YBar <= LAYERYBARMAX; ++YBar)
        {
            _PosIDtoXYBarsMap[CalculatePositionID(XBar, YBar)] = std::make_pair(XBar, YBar);
        }
    }
}


void TOFWallCalibration::ClearData(TLayer layer)
{
    for(auto itBeam = _PartEnPairsMC.begin(); itBeam != _PartEnPairsMC.end(); ++itBeam)
    {
        for(Int_t PosID = 0; PosID < NUMBEROFTWPOSITIONS; ++PosID)
        {
            delete _hQ[layer].at(*itBeam).at(PosID);
            delete _hTOF[layer].at(*itBeam).at(PosID);
        }

        _hQ[layer].at(*itBeam).clear();
        _hTOF[layer].at(*itBeam).clear();
    }

    _hQ[layer].clear();
    _hTOF[layer].clear();
}


void TOFWallCalibration::SetDebugMode()
{
    _Debug = true;
}
```


-------------------------------

Updated on 2021-12-30 at 11:00:09 +0000
