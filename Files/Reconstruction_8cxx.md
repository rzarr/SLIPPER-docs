---
title: src/Reconstruction.cxx

---

# src/Reconstruction.cxx



## Functions

|                | Name           |
| -------------- | -------------- |
| int | **[main](/Files/Reconstruction_8cxx.md#function-main)**(int argc, char ** argv) |


## Functions Documentation

### function main

```cpp
int main(
    int argc,
    char ** argv
)
```




## Source code

```cpp
#include "cxxopts.hpp"
#include "WaveDaqReconstruction.h"

int main(int argc, char **argv)
{
    cxxopts::Options options(argv[0], "Program info: reconstruct data for WaveDAQ detectors");
    options.add_options()
        ("x, channelmap",   "Channel Map XML file",  cxxopts::value<std::string>())
        ("i, inputfilename","WaveDAQ binary (.bin) input filename", cxxopts::value<std::string>())
        ("o, outputfilename","output filename (should be .root)", cxxopts::value<std::string>())
        ("t, timecalfile", "WaveDAQ time calibration filename", cxxopts::value<std::string>()->default_value(""))
        ("g, gain","(optional) gain set to perform the acquisition", cxxopts::value<float>()->default_value("1"))
        ("nev","(optional) number of events to process",  cxxopts::value<int>()->default_value("-1"))
        ("trig", "(optional) calibration map for trigger amplitudes", cxxopts::value<std::string>()->default_value(""))
        ("neutrons", "(optional) wether to save neutron decoded waveforms in the output (1) or not (0)", cxxopts::value<int>()->default_value("0"))
        ("histo", "(optional) wether to create the histogram directory in the output (1) or not (0)", cxxopts::value<int>()->default_value("0"))
        ("debug", "(optional) wether to run code in debug mode (1) or not (0)", cxxopts::value<int>()->default_value("0"))
        ("first", "(optional) first event to save in Waveform folders", cxxopts::value<int>()->default_value("1"))
        ("last", "(optional) last event to save in Waveform folders", cxxopts::value<int>()->default_value("50"))
        ("h, help", "Print help");

    auto result = options.parse(argc, argv);
    //Some error handling
    if (!result.count("channelmap"))
    {
        Message::DisplayFatalError(TString::Format("Missing Channel Map\n\n %s", options.help().c_str()));
        return 0;
    }
    if (!result.count("inputfilename"))
    {
        Message::DisplayFatalError(TString::Format("Missing Input file Name\n\n %s", options.help().c_str()));
        return 0;
    }
    if (!result.count("outputfilename"))
    {
        Message::DisplayFatalError(TString::Format("Missing Output file name\n\n %s", options.help().c_str()));
        return 0;
    }
    //Declare a WaveDaqReconstruction object and run
    WaveDaqReconstruction t;
    t.SetOutputFileName(result["outputfilename"].as<std::string>());
    t.LoadChannelMap(result["channelmap"].as<std::string>());
    t.SetGain(result["gain"].as<float>());

    if( result["neutrons"].as<int>() == 1 )
        t.SetSaveNeutrons();
    else
    {
        if ( result.count("trig") )
            t.LoadTriggerCalibration(result["trig"].as<std::string>());

        if (result["debug"].as<int>()==1)
            t.SetDebugMode(result["first"].as<int>(), result["last"].as<int>());
        else if (result["histo"].as<int>()==1)
            t.EnableHistograms();
    }


    //If time cal file name is not set, put it to inputfilename -> WDAQ file
    if ( !result.count("timecalfile") || result["timecalfile"].as<std::string>() == result["inputfilename"].as<std::string>() ) 
        t.RunReconstruction(result["inputfilename"].as<std::string>(), result["inputfilename"].as<std::string>(), result["nev"].as<int>());
    //TDAQ files -> tcalib is in a different file
    else
    {
        t.SetTDAQfile();
        t.RunReconstruction(result["inputfilename"].as<std::string>(), result["timecalfile"].as<std::string>(), result["nev"].as<int>());
    }


    return 0;

}
```


-------------------------------

Updated on 2021-12-30 at 11:00:09 +0000
