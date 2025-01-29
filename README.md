Installation
======

# Software for Live Interactive Plotting and Partial Event Reconstruction (v3.1)
This is the version 3.1 of the stand-alone SW of the FOOT experiment. The code is meant to run on data acquired by the WaveDAQ system. The repository contains a folder with source code "src/", one with configuration files "config/" and one for code documentation "docs/".

**N.B.: Each time a new acquisition is processed, the associated configuration files (config/ChannelMap\*.xml, config/MCTable\*.txt and src/Utils/Parameters.h) should be carefully checked and tuned.**

Branches (updated 24/02/2022):
- master
- debora (DEvelopment Branch Of Reconstruction Algorithm)

Tags:
- CNAO2021 -> For processing of CNAO run in 11/2021
- hit2022 -> For processing of HIT run in 07/2022

## Requirements
In order to be able to compile this SW you will need to install:

* cmake (version >= 3)
* ROOT (version >= 6.14/06)
* gcc (version >= 7)
* Python (version >= 3), with the multiprocessing package

In alternative, from version 3.1, the SW is also available inside a Docker image. The instructions for this type of installation are given in a dedicated section below.

## Installation
In order to install the SW, clone the repository into your local machine and issue the commands
```
>> cd slipper/
>> mkdir bin
>> cd bin/
```
then configure the build typing
```
>> cmake ../src
>> make
```
Assuming no error has happened, you should end with a set of executable files named:
- "Reconstruction", for WaveDAQ signal processing
- "LivePlotter", for the online plotting used during data takings
- "EventDisplay", for the waveform event display
- "CalibratePosition", for the TW time-position calibration
- "Calibration", for TW dE and TOF calibration
- "Analysis", for offline analysis of processed data

N.B.: Tags are automatically added in the output tree if the file names convention (see below) is respected. If the name convention is not respected, Tags are initialized to 0 or None.

## Tier1 setup and install
SLIPPER can be installed and run on the Bologna Tier1. The procedure is similar to the one described above, with the addtion of a few steps to set the environment. To do this, a common file has been created and the environment can be set just by typing:
```
>> source /opt/exp_software/foot/root_shoe_foot.sh
```
On the Tier1, the software files have to be stored under the "/opt/exp_software/foot/\${USER}" folder, where "\${USER}" is you username on the machine. Clone the repository inside this folder, step inside it and issue:
```
>> mkdir bin
>> cd bin/
>> cmake3 ../src
>> make
```
At this point, the SW should be compiled and ready to be used.


## Tier3 setup and install
SLIPPER can be easily installed and run on the Bologna Tier3. The procedure is similar to the one described above, with the addtion of a few steps. First, the bash and ROOT configurations have to be loaded. To do this, type:
```
>> scl enable devtoolset-9 bash
>> source /opt/exp_software/foot/root4foot.sh
```
Then, move to the "slipper" directory and type:
```
>> mkdir bin
>> cd bin/
>> cmake3 ../src
>> make
```
At this point, the SW should be compiled and ready to be used. The Tier3 also supports multithreading with the python script as described below.

## Release vs Debug build of the software
The above instructions for installation create executable files with the intent of directly running on data. The default type of build ("Release") is way faster (~3x) then a "Debug" build, which should only be used when developing the code. To obtain a "Debug" build of SLIPPER, the build type can be forced in the compiler option via the command:
```
>> cmake ../src -DCMAKE_BUILD_TYPE=Debug
```
This type of build creates more verbose outputs, useful for code testing and bug solving.


# Doxygen documentation for developers
From version 3.0, the code has also been conceived to produce a developer documentation and update it each time a new push to the master branch is preformed. The developer documentation is currently hosted on [Gitbook](https://roberto-zarrella2.gitbook.io/slipper-developer-manual/) and [Baltig pages](https://zarrella.baltig-pages.infn.it/slipper).

Alternatively, the documentation can be produced locally by the developer using the **[Doxygen](https://www.doxygen.nl/index.html)** toolkit. Once Doxygen is installed, the documentation can be created by running the following command in the "slipper" directory:
```
>> path/to/doxygen docs/Doxyfile
```
This command will create a folder named "docs_temp/" containing all the documentation. To access the documentation, open the file "docs_temp/html/index.html" using any browser.

# Analysis
From version 2.5, a first analysis script has been implemented. This is meant to provide some fast information on the output of the Reconstruction executable and it's used as a run control routine. The parameters required by the executable are:
```
>> ./Analysis [OPTION...]

  -i, --inputfilename     Pre-processed input filename (.root)
  -o, --ouputfilename     Output filename (.root)
  -h, --help              Print help
```
As of today, the script produces a series of histograms to quickly check the correct functioning of TOF-Wall detector (channels/bars), as well as some preliminary time resolution studies.
