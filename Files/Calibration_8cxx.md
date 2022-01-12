---
title: src/Calibration.cxx
summary: File containing the main function of the Calibration executable. 

---

# src/Calibration.cxx

File containing the main function of the Calibration executable.  [More...](#detailed-description)

## Functions

|                | Name           |
| -------------- | -------------- |
| int | **[main](/Files/Calibration_8cxx.md#function-main)**(int argc, char ** argv) |

## Detailed Description

File containing the main function of the Calibration executable. 

**Author**: R. Zarrella


This executable calls the [TOFWallCalibration](/Classes/classTOFWallCalibration.md) class to produce the dE and TOF calibration maps for SC-TW measurements. This script has been studied for data samples acquired before the GSI2021 campaign, so the [TOFWallCalibration](/Classes/classTOFWallCalibration.md) class does not work on more recent samples. This stems from the change in the calibration approach which, for the GSI2021 campaign, uses the dE peaks of nuclear fragments instead of different primary beams. 


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
#include "TOFWallCalibration.h"
#include <dirent.h>

int main(int argc, char **argv)
{
  cxxopts::Options options(argv[0], "Program info: calibrate data for dE-TOF detector");
  options.add_options()
      ("i, inputdatadir","input directory containing the reconstructed rec.root files",  cxxopts::value<std::string>())
      ("o, outputdir","output directory to save calibration maps",  cxxopts::value<std::string>())
      ("m, mcrefvalues", "txt file containing the Monte Carlo reference values needed for the calibration", cxxopts::value<std::string>())
      ("debug", "(optional) wether to run code in debug mode (1) or no (0)", cxxopts::value<int>()->default_value("0"))
      ("h, help", "Print help");

  auto result = options.parse(argc, argv);

  //Check input directory
  if (!result.count("inputdatadir"))
  {
    Message::DisplayMessageWithEmphasys(TString::Format("Missing Input data Directory\n\n %s", options.help().c_str()));
    return 0;
  }
  DIR* in_dir = opendir(result["inputdatadir"].as<std::string>().c_str());
  if(!in_dir)
  {
    Message::DisplayMessageWithEmphasys("Input directory does not exist");
    return 0;
  }
  closedir(in_dir);

  //Check output directory
  if (!result.count("outputdir"))
  {
    Message::DisplayMessageWithEmphasys(TString::Format("Missing Output data Directory\n\n %s", options.help().c_str()));
    return 0;
  }
  DIR* out_dir = opendir(result["outputdir"].as<std::string>().c_str());
  if(!out_dir)
  {
    Message::DisplayMessageWithEmphasys("Output directory does not exist");
    return 0;
  }
  closedir(out_dir);

  //Check MC ref table
  if (!result.count("mcrefvalues"))
  {
    Message::DisplayMessageWithEmphasys(TString::Format("Missing MC table file for calibration!\n\n %s", options.help().c_str()));
    return 0;
  }
  //
  TOFWallCalibration t;
  if (result["debug"].as<int>()==1)
  {
    t.SetDebugMode();
  }
  t.LoadMCRefValues(result["mcrefvalues"].as<std::string>());
  t.LoadRecData(result["inputdatadir"].as<std::string>());
  t.RunCalibration(result["outputdir"].as<std::string>());
  return 0;
}
```


-------------------------------

Updated on 2022-01-12 at 10:56:23 +0000
