---
title: Calibration

---

# Calibration




# Energy and TOF Calibration (WORK IN PROGRESS!)

The Calibration executable takes the output ROOT files created with the Reconstruction binary and produces the calibration maps needed to convert raw Energy and Time-Of-Flight data from the dE-TOF system in physical units. This executable requires:



* Reconstruction output files with extension ".rec.root" and properly tagged PrimaryParticle and BeamEnergy
* An MC table containing the reference values for each beam. If ANY of the beams found in data is missing from the MC table, the executable will throw an error.
The parameters needed by the Calibration executable can be seen through the help function. Again, to display it, run the code with no options:



```cpp
>> ./Calibration [OPTION...]

  -i, --inputdatadir      input directory containing the reconstructed .rec.root files
  -o, --outputdir         output directory to save calibration maps
  -m, --mcrefvalues       file containing the Monte Carlo reference values needed for the calibration
      --debug             (optional) wether to run code in debug mode (1) or not (0) (default: 0)
  -h, --help              Print help
```

The debug mode saves additional txt and ROOT files in the output directory containing single layer calibration maps, raw histograms and energy calibration curves. An example of command line could be (from the slipper directory):



```cpp
>> ./bin/Calibration -m config/MCTable.txt -i path/to/input/dir -o path/to/output/dir --debug 1
```


## MC Table

This is a .txt file (available in the "config/" folder) that contains the Monte Carlo dE and TOF reference values needed to perform the calibrations. **This file is MANDATORY to run the Calibration executable.** The current version (>= 2.2) of the software needs an MC table file containing, in each line, the quantities:



* ParticleID: ID of the beam particle (0 = Proton, 1 = Helium, 2 = Carbon, 3 = Oxygen)
* Beam energy [GeV/u]
* dEx: mean value of the MC energy loss in the LayerX of the TW [MeV]
* dEy: mean value of the MC energy loss in the LayerY of the TW [MeV]
* TOFx: mean value of the MC Time-Of-Flight measured in the LayerX of the TW [ns]
* TOFy: mean value of the MC Time-Of-Flight measured in the LayerY of the TW [ns]
More flags could be added in future (e.g. a "campaign" string, errors on MC values). Each line starting with a "#" is ignored by the reader, so comments can be freely added to the file. An example of the MC table containing the CNAO03-2019 and GSI04-2019 MC values is reported below



```cpp
#MC Table with the CNAO03-2019 and GSI04-2019 reference values
#ParticleID En [GeV/u]  dEx [MeV]   dEy [MeV]  TOFx [ns]   TOFy [ns]
0  0.060  3.47  3.65  4.19  4.22
2  0.115  78.6  82.6  3.19  3.22
2  0.260  42.7  43.0  2.28  2.30
2  0.400  33.5  33.6  1.99  2.00
3  0.400  59.7  60.0  10.43  10.45
```


## Output: Energy and TOF calibration maps

The code produces an energy calibration map in the format currently accepted by SHOE. Since the current model implemented is the Birks light output function, the Energy calibration maps are produced as .txt files containing, in each line, the quantities:



* ID of the TW position (defined in the [TOFWallCalibration](/Classes/classTOFWallCalibration.md) class)
* ID of the bar in LayerX of the TW
* ID of the bar in LayerY of the TW
* p0, gain factor of the model [V*ns/MeV]
* p1, saturation parameter of the model [1/MeV]
* ID of the TW layer in SHOE
The energy calibration maps are saved in the output directory. If the code is run in debug mode, additional calibration maps are saved for single TW layers. These maps contain an additional flag indicating if the calibration procedure was successful.

The executable also produces the .txt files containing the Time-Of-Flight calibration (in a SHOE-compatible format) of the dE-TOF system. The matching of raw and MC values is done separately for each beam, meaning that one map is produced for each of the beams found in the input files. Each TOF calibration map contains:



* ID of the TW position
* ID of the bar in LayerX of the TW
* ID of the bar in LayerY of the TW
* DeltaT: Difference between the mean raw and MC TOF values [ns]
* DeltaT2: to be implemented, set to 0
* ID of the TW layer in SHOE
The TOF calibration maps are saved in the output directory with names indicating the beam they refer to. If the code is run in debug mode, additional maps for each TW layer are saved. These maps also contain a flag indicating if the calibration procedure was successful. 

-------------------------------

Updated on 2025-02-26 at 13:36:50 +0000
