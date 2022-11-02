User Manual
======

# Software for Live Interactive Plotting and Partial Event Reconstruction (v3.1)
This is the version 3.1 of the stand-alone SW used by the Pisa group of the FOOT experiment. The code is meant to run on data acquired by the WaveDAQ system. The repository contains a folder with source code "src/", one with configuration files "config/" and one for code documentation "docs/".

**N.B.: Each time a new acquisition is processed, the associated configuration files (config/ChannelMap\*.xml, config/MCTable\*.txt and src/Utils/Parameters.h) should be carefully checked and tuned.**

Branches (updated 24/02/2022):
- master
- debora (DEvelopment Branch Of Reconstruction Algorithm)

Tags:
- CNAO2021 -> For processing of CNAO run in 11/2021

## Requirements
In order to be able to compile this SW you will need to install:

* cmake (version >= 3)
* ROOT (version >= 6.14/06)
* gcc (version >= 7)
* Python (version >= 3), with the multiprocessing package

In alternative, from version 3.1, the SW is also available inside a Docker image. The instructions for this type of installation are given in a dedicated section below.

## Compilation
In order to install the SW, clone the repository into your local computer and issue the commands
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
Assuming no error has happened, you should end with two executable files named "Reconstruction" and "Calibration", which are the binary used to process WaveDAQ signals and calibrate the dE-TOF system

N.B.: Tags are automatically added in the output tree if the file names convention (see below) is respected. If the name convention is not respected, Tags are initialized to 0 or None.

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

# Docker image (working on Linux and MacOS)
From version 3.1 on, the software provides also a Docker image for all the updated branches. The software has been successfully installed on Ubuntu, SL7 and some versions of MacOs. However, the Docker image provides a platform-indipendent environment to run the code without issues and with the needed ROOT (6.24) and Python (2 and 3) versions already installed.

The repository were all the images are hosted can be found at [this link](https://hub.docker.com/repository/docker/zarrella/slipper-docker). All images are built from a base version of Ubuntu, which is the OS where the code was tested the most and are continuously updated through GitLab Pipelines. The only requirement to use the image is a working [Docker](https://docs.docker.com/get-docker/) installation. The repository provides an executable that takes care of pulling the "latest" tag of the SLIPPER base image and build the "local" version. To get the images, run:

```
>> ./path/to/slipper/docker/install_docker.sh
```

**N.B.: This step is mandatory since the "latest" tag of the slipper-docker image DOES NOT contain an installation of the software. It is only used as base image for faster build of the "local" version, which is the ONLY ONE that has a functioning SLIPPER installation. After this step is completed, the "latest" image can be removed.**

After the installation is finished, a docker container can be started launching the "run_docker.sh" executable found in the "docker" folder of the repository. This executable launches a container of the "local" tag of the slipper-docker image.

The executable also mounts the **current** local directory in the "/home/footer/data" path inside the container. This feature can be exploited to process data inside the container and make them available in the local host folder. So, to process the data, step into the folder containing all the binary files and launch:

```
>> cd path/to/binary/files/folder
>> ./path/to/slipper/run_docker.sh
>> ...
```

To make the processed files available in the local host folder, save them in the shared folder ("data" inside the container).

**WARNING!! All the changes made to the shared folder from the container WILL be propagated to the local folder in the host system!**

## Running docker containers by hand ([CLICK HERE BEFORE READING](https://tenor.com/view/donald-trump-responsibility-i-dont-take-any-responsibility-at-all-no-responsibility-usa-president-gif-16623875))

After pulling the "latest" image and building the "local" version, it is possible to run a container using the command:

```
>> docker run -it zarrella/slipper-docker:local
```

The "-it" option tells docker to run the container in interactive mode, meaning that it will open a shell with the poperly set environment and the already compiled software. From this shell, it is possible to run SLIPPER immediately.

In Docker, it is also possible to share a local folder with the container. To do so, step into the folder containing the input binary data and launch:

```
>> docker run -it -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

This will mount the local current folder inside the container in "data". At this point, the binary input files can be processed from inside the container and the output can be saved in the "data" folder to make it accessible from outside docker.

With the current docker image, it is also possible to use the ROOT TBrowser from inside the container to check the contents of processed files. To activate this functionality, the DISPLAY variable needs to be passed to docker. This can be done with the following command on Linux:

```
>> docker run -it --net=host -e DISPLAY=$DISPLAY -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

and MacOs:

```
>> docker run -it --net=host -e DISPLAY=host.docker.internal:0.0 -v $PWD:/home/footer/data zarrella/slipper-docker:local
```

For Windows users, the first step is to install an operating system that actually works :)

# Doxygen documentation for developers
From version 3.0, the code has also been conceived to produce a developer documentation and update it each time a new push to the master branch is preformed. The developer documentation is currently hosted on GitBook at the following link: [https://roberto-zarrella2.gitbook.io/slipper-developer-manual/](https://roberto-zarrella2.gitbook.io/slipper-developer-manual/).

Alternatively, the documentation can be produced locally by the developer using the **[Doxygen](https://www.doxygen.nl/index.html)** toolkit. Once Doxygen is installed, the documentation can be created by running the following command in the "slipper" directory:
```
>> path/to/doxygen docs/Doxyfile
```
This command will create a folder named "docs_temp/" containing all the documentation. To access the documentation, open the file "docs_temp/html/index.html" using any browser.

# XML configuration file: Channel Map

These files (available in the "config/" folder) contain the mapping between channels and SC, BARS and MODULES (wiring) for each campaign currently supported by the code. **This file is MANDATORY to run the Reconstrucion executable.**
The Channel map should look like this:
```
<CHANNEL_MAP>
<DATE>03/06/2021</DATE>
<DESCRIPTION>Channel map template</DESCRIPTION>

<SC>
  <BOARD_ID>157</BOARD_ID>
  <CHANNELS>0,1,2,3,4,5,6,7</CHANNELS>
</SC>

<BAR>
  <GLOBAL_CHANNEL_IDA>0</GLOBAL_CHANNEL_IDA>
  <GLOBAL_CHANNEL_IDB>1</GLOBAL_CHANNEL_IDB>
  <BAR_ID>0</BAR_ID>
  <BOARD_ID>78</BOARD_ID>
  <CHANNEL_A>1</CHANNEL_A>
  <CHANNEL_B>2</CHANNEL_B>
  <LAYER>0</LAYER>
  <PHYS_COORD_X></PHYS_COORD_X>
  <PHYS_COORD_Y></PHYS_COORD_Y>
  <PHYS_COORD_Z></PHYS_COORD_Z>
</BAR>

...

<MODULE>
  <MODULE_ID>0</MODULE_ID>
  <BOARD_ID>164, 165</BOARD_ID>
  <CHANNELS>13,14,15,0,1,2,3,4,5</CHANNELS>
  <CRYSTALS>0,1,2,3,4,5,6,7,8</CRYSTALS>
  <CRYSTAL_X>-1,0,1,-1,0,1,-1,0,1</CRYSTAL_X>
  <CRYSTAL_Y>1,1,1,0,0,0,-1,-1,-1</CRYSTAL_Y>
</MODULE>

...

<NEUTRON>
  <NAME>BACCO1</NAME>
  <BOARD_FAST>131</BOARD_FAST>
  <CHANNELS_FAST>0,1</CHANNELS_FAST>
  <GLOBAL_CH_FAST>0,1</GLOBAL_CH_FAST>
  <BOARD_SLOW>11</BOARD_SLOW>
  <CHANNELS_SLOW>7</CHANNELS_SLOW>
  <GLOBAL_CH_SLOW>0</GLOBAL_CH_SLOW>
</NEUTRON>


```
Each channel map MUST contain <DATE> and <DESCRIPITON> elements as parent of the main node (they can be empty). The elements of the channel map are:

### SC ---> Start Counter
This field must contain:

* BOARD_ID: serial number of the SC board
* CHANNELS: list of the SC channels in the above board

### BAR ---> TW bars

The channel map MUST contain at least one <BAR> element, and each bar MUST contain the following attributes:

* BAR_ID: the id of the bar (must be unique)
* BOARD_ID: the WaveDream board id
* GLOBAL_CHANNEL_IDA: the global id of the first channel
* GLOBAL_CHANNEL_IDB: the global id of the second channel
* CHANNEL_A: the channel id   
* CHANNEL_B: the channel id
* LAYER: Could be 1 (LayerX) or 0 (LayerY)
* PHYS_COORD_X: to be implemented
* PHYS_COORD_Y: to be implemented
* PHYS_COORD_Z: to be implemented

### MODULE ---> Calorimeter modules

The channel map can also contain some calorimeter <MODULE> elements in the format shown above:

* MODULE_ID: the id of the module (must be unique)
* BOARD_ID: The WaveDREAM board(s) associated to the module. If two boards are indicated, the first channels up to number 15 are associated to the first board and the rest are linked to the second board
* CHANNELS: the Id of each WaveDREAM channel used for the Module
* CRYSTALS: the global Id of all the crystals of the module. Channels and crystals values have to be ordered in the same way because they are associated one-by-one.
* CRYSTAL_X/Y: Physical X/Y coordinates o the CALO crystals in the SHOE reference frame \[OPTIONAL\]

### NEUTRON ---> Neutron detectors

Neutron detectors can be added to the channel map as above with fields:
* NAME: Name of the detector
* BOARD_FAST: WaveDREAM board used for fast signals
* CHANNELS_FAST: List of channels for fast signals
* GLOBAL_CH_FAST: Global channel Ids for fast channels
* BOARD_SLOW: WaveDREAM board used for slow signals
* CHANNELS_SLOW: List of channels for slow signals
* GLOBAL_CH_SLOW: Global channel Ids for slow channels

Note that the combination of (BOARD_ID,CHANNEL) should not appear more than once in the in the ChannelMap file. Moreover, crystal IDs MUST be numbered from 0 to NUMBEROFCRYSTALS - 1 (set in src/Parameters.h). The same applies to global channel Ids for the neutron detectors.

# MC Table
This is a .txt file (available in the "config/" folder) that contains the Monte Carlo dE and TOF reference values needed to perform the calibrations. **This file is MANDATORY to run the Calibration executable.**
The current version (>= 2.2) of the software needs an MC table file containing, in each line, the quantities:

* ParticleID: ID of the beam particle (0 = Proton, 1 = Helium, 2 = Carbon, 3 = Oxygen)
* Beam energy [GeV/u]
* dEx: mean value of the MC energy loss in the LayerX of the TW [MeV]
* dEy: mean value of the MC energy loss in the LayerY of the TW [MeV]
* TOFx: mean value of the MC Time-Of-Flight measured in the LayerX of the TW [ns]
* TOFy: mean value of the MC Time-Of-Flight measured in the LayerY of the TW [ns]

More flags could be added in future (e.g. a "campaign" string, errors on MC values). Each line starting with a "#" is ignored by the reader, so comments can be freely added to the file. An example of the MC table containing the CNAO03-2019 and GSI04-2019 MC values is reported below

```
#MC Table with the CNAO03-2019 and GSI04-2019 reference values
#ParticleID En [GeV/u]  dEx [MeV]   dEy [MeV]  TOFx [ns]   TOFy [ns]
0  0.060  3.47  3.65  4.19  4.22
2  0.115  78.6  82.6  3.19  3.22
2  0.260  42.7  43.0  2.28  2.30
2  0.400  33.5  33.6  1.99  2.00
3  0.400  59.7  60.0  10.43  10.45
```

# Reconstruction
The Reconstruction executable transforms the binary WaveDAQ or TDAQ files into root files containing simple variables representing events detected by the SC (only the 1st branch), TW, CALO and Neutron detectors. All the quantities calculated for single TW channels are marked with A/B in the branches of the final tree.
The data saved in this version are:

#### Start Counter
* SC_Timestamp -> the timestamp [ns] of the event measured by the Start Counter.
* SC_TotCharge -> the integral of the summed Start Counter Waveform \[V\*ns\].

#### TOF-Wall
* BAR_Ped* -> baseline [V] of the waveform.
* BAR_PedRMS* -> root mean square of the baseline [V] of the waveform.
* BAR_Amp* -> amplitude [V] of the waveform.
* BAR_Time* -> timestamp [ns] of the waveform determined with the Constant Fraction Discriminator (CFD) method. This quantity already contains the CLK jitter correction.
* BAR_Charge\* -> integral of the waveform [V\*ns]. 
* BAR_RiseTime* -> rise time [ns] of the waveform calculated with the 10%-90% method.
* BAR_Timestamp -> the timestamp [ns] of the event measured by each bar of the TW.
* BAR_Charge -> the total charge detected [V\*ns] calculated as sqrt( BAR_ChargeA\*BAR_ChargeB )
* BAR_DeltaT_AB -> the difference in the timestamp [ns] of the waveforms detected by the two channels of the same bar ( BAR_TimeA - BAR_TimeB )
* BAR_LogCratio_AB -> the log of the charge ratio between the charges collected by the two channels of the same bar ( log(BAR_ChargeA/BAR_ChargeB) )
* BAR_TOF_Uncal -> the uncalibrated Time Of Flight [ns] measured in each bar. This variable already contains the clock jitter correction.

#### Calorimeter
* CRY_Ped -> baseline [V] of the waveform.
* CRY_PedRMS -> root mean square of the baseline [V] of the waveform.
* CRY_Amp -> amplitude [V] of the waveform.
* CRY_Time -> timestamp [ns] of the waveform determined with the Constant Fraction Discriminator (CFD) method. This quantity already contains the CLK jitter correction.
* CRY_Charge -> integral of the waveform [V\*ns].
* CRY_RiseTime -> rise time [ns] of the waveform calculated with the 10%-90% method.

#### Neutrons
* N*_Ped -> baseline [V] of the waveform.
* N*_PedRMS -> root mean square of the baseline [V] of the waveform.
* N*_Amp -> amplitude [V] of the waveform.
* N*_Time -> timestamp [ns] of the waveform determined with the Constant Fraction Discriminator (CFD) method. This quantity already contains the CLK jitter correction.
* N*_Charge -> integral of the waveform [V\*ns].
* N*_RiseTime -> rise time [ns] of the waveform calculated with the 10%-90% method.

where the '*' stands for S/F for Slow and Fast channels.

#### Trigger/TCB information
* WD_TriggerType: the event trigger Id, such as 40 for Minimum Bias and 1 for fragmentation events. 
* WD_FragTrigger: a boolean value that signals if the fragmentation trigger was activated in the event -> FIRMWARE 
* WD_BeamRate: beam rate \[Hz\] measured by the WaveDAQ as rate of MB events.
* WD_TotalTime: total time of the acquisition \[s\].
* WD_FragTriggerSW: boolean flag that checks if the fragmentation trigger was switched on -> SOFTWARE
* WD_FragTriggerCALO: boolean flag that performs a logical and of the firmware fragmentation trigger and a CALO or (IMPLEMENTED FOR HIT2022)

There are also branches dedicated to:

* EventNumber: Number of the saved event.
* Tags: this quantity depends on the files processed. For WaveDAQ files, the quantities saved are Gain, BeamEnergy [GeV/u], ParticleType, BeamPosition (PosX, PosY). The ParticleType tag is an integer indicating the primary particle as indicated in the "Parameters.h" file. For TDAQ files, the Tags contain RunNumber and FileNumber.

More quantities, and waveform plots, are included in debug mode. In particular, the final root tree in debug mode has:

* A folder containing SC WFs plots. In particular, the WF of each SC channel is saved together with the total SC signal (sum of the channels) and a visualization of the corresponding CFD application.
* A folder containing TW WFs plots, which displays the WFs and CFDs for the TW channels involved in the event.
* A folder containing CALO WFs plots, which displays the WFs and CFDs for the CALO channels involved in the event.
* A folder containing Neutron WFs plots, which displays the WFs and CFDs for the Neutron channels involved in the event.
* A folder containing CLK WFs plots, which shows all the CLKs involved and the linear fits used to calculate the corresponding phases.
* A branch containing all the information of SC signals, for each channel of the detector.
* An additional branch for each of the quantities listed above, but with the possibility of displaying one channel/bar/crystal at a time.
* A branch dedicated to the CLK phase jitter of each TW channel with respect to the SC CLK.
* A branch containing the timestamps of TW signals without CLK jitter correction.

## Running Reconstruction
Each executable compiled provides an help function, run the executable without any parameter to display it.
E.g.,
```
>> ./Reconstruction

-x, --channelmap arg        Channel Map XML file,
-i, --inputfilename arg     WaveDAQ binary (.bin) input filename,
-o, --outputfilename arg    output filename (should be .root),
-t, --timecalfile arg       (optional) WaveDAQ time calibration (.dat) filename,
-g, --gain arg              (optional default=1) gain set to perform the acquisition (default: 1),
    --nev arg               (optional) how many events to process (default: 1E6),
    --trig arg              (optional) calibration map for trigger amplitudes (default: ""),
    --neutrons arg          (optional) wethet to save neutron decoded waveforms in the output (1) or not (0) (default: 0)
    --histo arg             (optional) wether to create the histogram directory in the output (1) or not (0) (default: 0),
    --debug arg             (optional) wether to run code in debug mode (1) or no (0) (default: 0),
    --first arg             (optional) first event to save in Waveform folders (default: 0),
    --last arg              (optional) last event to save in Waveform folders (default: 50),
-h, --help                  Print help

```

For example, (starting in the slipper directory) the command
```
>> ./bin/Reconstruction -x config/ChannelMap*.xml -i InputFile.data -t tcalibIn.dat -o OutputFile.root --histo 1 --debug 1 --first 100 --last 200
```
analyzes the binary file InputFile.data with time calibration tcalibIn.dat in debug mode and saves the WFs of events from 100 to 200 in the file OutputFile.root. Moreover, it saves a series of histograms we can construct for fast-feedback on the acquisition in a folder named "Histos" in the output file. The argument "histo" is always set to 1 if "debug" is 1. The "*" in the channel map name indicates the corresponding campaign.

**N.B.: the current version of the code can run on either WaveDAQ stand-alone files and TDAQ global files. Since the time calibration is in a separate file only when running on TDAQ acquisitions, whenever this parameter is indicated the program WILL expect a TDAQ file. Otherwise the input is treated as a WaveDAQ file.**

As an example, if we want to run as above on a WaveDAQ file, the command to issue is:
```
>> ./bin/Reconstruction -x config/ChannelMap*.xml -i InputFile.bin -o OutputFile.root --debug 1 --first 100 --last 200
```
which is exactly the same, but without specifying the time calibration file. Note also that the histo flag is not needed since the debug flag is active. 

The Reconstruction executable can also provide useful histograms to check the fragmentation trigger amplitudes. To obtain these plots, the "trig" flag needs to be used:
```
>> ./bin/Reconstruction -x config/ChannelMap*.xml -i InputFile.bin -o OutputFile.root --debug 1 --first 100 --last 200 --trig config/TriggerAmpMap.txt
```
The "TriggerAmpMap.txt" file contains the calibration that links DRS amplitudes to triger amplitudes. When this flag is utilized, the trigger amplitudes for central bars are saved in the "Histos" folder and a comparison between Firmware-Software trigger efficiency is provided.

The "neutrons" flag needs to be used ONLY if the user wants to save the decoded waveforms of all neutron detectors in the output. The usage of this flag superseeds everything else, meaning that almost no reconstruction will be performed and almost only neutron WFs will be available in the output. The "neutrons" tree will contain:

* SC_Timestamp, TriggerType, IsFragTriggerOn, EventNumber and Tags as defined above
* A branch with WFs from neutron slow channels
* A branch with WFs from neutron fast channels

For each WF, the quantities saved are:

* V: array of 1024 float values containing the amplitudes of the WF
* T: array of 1024 float values containing the time bins of the WF
* IsOn: A boolean flag signaling if the channel was activated or not

#### Tags

In order to also provide automatic tagging for different data acquisitions, a name convention is established for different campaigns. For example, for WaveDAQ files of the CNAO03-2019 campaign, the following name convention was used:

* One letter of the primary particle (P = proton, H = helium, C = carbon, O = oxygen)
* E followed by a number for the kinetic energy per nucleon of the primary particle in GeV
* POSX/POSY followed by a number for the X/Y coordinates of the beam on the TW (to be implemented)
* G followed by a float number for the gain used to acquire the data contained in the file
* Other comments can be added after this fields
* Each Field is separated by the other using an underscore.

For example the file C_E0.259_G0.5.bin contains binary data acquired using a Carbon beam with kinetic energy of 0.259 GeV per nucleon and Gain equal to 0.5.

Different name conventions can be implemented for different campaigns containing come dedicated relevant parameters. For example, TDAQ files of the GSI2021 campaign contain the RunNumber and FileNumber of the events saved.

##  File name convention and Running in batch
If needed, it is possible to run in batch the reconstruction of several files using the RunReconstruction.py script found in the "src/PyRoutines" folder.
If the code is run in batch with the .py script, the needed parameters are

```
>> python src/PyRoutines/RunReconstruction.py [OPTION]

-x, --channelmap      ChannelMap xml file
-d, --datadir         path to directory containing input files
-o, --outputdir       path to directory of destination for output files
-w, --wdaq            wether the input files are in WaveDAQ (1) or TDAQ (0) format
-r, --run             (optional) number of the run to be analyzed    -> REQUIRED FOR TDAQ FILES (default=-1)
-t, --numthreads      (optional) number of threads to use to process the files in datadir (default=1)
-f, --mergedfilename  (optional) name of the output file obtained from merging all the *.rec.root objects in the outputdir (default="Merge_{run}.root")
-h, --help            show this help message and exit
```

An example of bash command to run in batch on WaveDAQ files from the "slipper" directory is:

```
>> python src/PyRoutines/RunReconstruction.py -x config/ChannelMap*.xml -d path/to/input/directory -o path/to/output/directory -w 1 -t 6 -f test.root
```

This command will process all the *.bin files in the input directory using 6 threads and save both the single *.rec.root files and the merged one with name "test.root" in the output directory. Note that in batch-mode the writing of histograms is currently forced to 1, and the merging works for both the tree and the histos. Debug is forced to 0.

When processing TDAQ files, the python script requires an additional argument, i.e. the run number. For example, the command:
```
>> python src/PyRoutines/RunReconstruction.py -x config/ChannelMap*.xml -d path/to/input/directory -o path/to/output/directory -w 0 -r xxxx -t 6
```
will process all the files from run "xxxx" (with name "\*xxxx\*data\*") in the input directory and save the merged output into a single file (default name: "Merge_xxxx.root") in the output directory. The time calibration file for the run needs to be saved in the input directory. This file should have extension \*.dat and contain the run number. If the time calibration file for the indicated run is not indicated, the script will look for corresponding files from previous runs.

**N.B.: The Python package "multiprocessing" is mandatory to run with multiple threads. Debug mode is not available when running in batch.**

**N.B.: To run on the Bologna Tier3, it is mandatory to call the right version of python, i.e. "python3"**

From this version, it is also possible to reconstruct different runs acquired with the TDAQ in parallel using the python script src/PyRoutines/ReconstructMultipleRuns.py

```
>> python src/PyRoutines/ReconstructMultipleRuns.py [OPTION]

-x, --channelmap      ChannelMap xml file
-d, --datadir         path to directory containing input files
-o, --outputdir       path to directory of destination for output files
-f, --firstrun        number of the first run to be analyzed
-l, --lastrun         number of the last run to be analyzed
-t, --numthreads      (optional) number of threads to use to process the files in datadir (default=1)
-h, --help            show this help message and exit
```

If this script is used, the single runs are reconstructed with 1 thread each. The number of threads tells the script how many runs it can reconstruct in parallel.

# Calibration (WORK IN PROGRESS!)
The Calibration executable takes the output ROOT files created with the Reconstruction binary and produces the calibration maps needed to convert raw Energy and Time-Of-Flight data from the dE-TOF system in physical units. This executable requires:

* Reconstruction output files with extension ".rec.root" and properly tagged PrimaryParticle and BeamEnergy
* An MC table containing the reference values for each beam. If ANY of the beams found in data is missing from the MC table, the executable will throw an error.

The parameters needed by the Calibration executable can be seen through the help function. Again, to display it, run the code with no options:

```
>> ./Calibration [OPTION...]

  -i, --inputdatadir      input directory containing the reconstructed .rec.root files
  -o, --outputdir         output directory to save calibration maps
  -m, --mcrefvalues       file containing the Monte Carlo reference values needed for the calibration
      --debug             (optional) wether to run code in debug mode (1) or not (0) (default: 0)
  -h, --help              Print help


```

The debug mode saves additional txt and ROOT files in the output directory containing single layer calibration maps, raw histograms and energy calibration curves.
An example of command line could be (from the slipper directory):

```
>> ./bin/Calibration -m config/MCTable.txt -i path/to/input/dir -o path/to/output/dir --debug 1
```

## Output: Energy and TOF calibration maps
The code produces an energy calibration map in the format currently accepted by SHOE. Since the current model implemented is the Birks light output function, the Energy calibration maps are produced as .txt files containing, in each line, the quantities:

* ID of the TW position (defined in the TOFWallCalibration class)
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


# Analysis
From version 2.5, a first analysis script has been implemented. This is meant to provide some fast information on the output of the Reconstruction executable and it's used as a run control routine. The parameters required by the executable are:
```
>> ./Analysis [OPTION...]

  -i, --inputfilename     Pre-processed input filename (.root)
  -o, --ouputfilename     Output filename (.root)
  -h, --help              Print help
```
As of today, the script produces a series of histograms to quickly check the correct functioning of TOF-Wall detector (channels/bars), as well as some preliminary time resolution studies.


# LivePlotter (WORK IN PROGRESS)
From version 3.1, a LivePlotter executable is available. This executable is called by the src/PyRoutines/Plotter.py routine in a dedicated thread and its purpose is to provide some online information during data takings. The only argument needed by the LivePlotter is the directory containing output files from the Reconstruction executable. The routine will then check the directory continuously and update the online plots as soon as a new ".root" file is added. Right now the plots implemented in the LivePlotter are:
* TW hitmaps with MB and Fragmentation trigger
* Calibrated trigger amplitude seen by the TCB discriminators for all the channels involved in the fragmentation trigger logic. 
* Raw Fragmentation dE spectra for all the TW bars involved in the fragmentation trigger, for the chosen trigger thresholds (set via the TriggerAmpMap.txt file )
* Pile-Up percentage in each file
* Total number of counts in the A-B channels of the TW
* Total number of "saturated" counts (amplitude > 1V) in the A-B channels of the TW
* Raw energy loss vs TOF at the center of the TW
* Raw Energy deposition in all the CALO crystals
* TW bars - CALO crystals multiplicity
* _\[preliminary\]_ Comparison between raw CALO energy and TW raw energy loss

The best way to run the LivePlotter is to call it through the dedicated Python routine:

```
python3 src/PyRoutines/Plotter.py -x config/ChannelMap*.xml -i InputDir -o OutputDir -w 1 -b 1 -t config/TriggerAmpMap*.txt
```
where '*' indicates the acquisition campaign.

This command will launch a 3-thread process, with each of the involved threads dedicated to a specific task:
* Online processing of data
* Beam rate monitoring (updated and plotted online)
* Online plotting (LivePlotter)

**The Plotter.py routine calls the RecoMonitor.py routine, which has not been completely tested on TDAQ files!! To run with this file format, the time calibration of WaveDAQ has to be saved somewhere!**

**This tool is intended for online monitoring during data acquisitions ONLY!!**