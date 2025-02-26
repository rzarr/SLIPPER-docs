Reconstruction
======

The **Reconstruction** executable transforms the binary WaveDAQ or TDAQ files into root files containing simple variables representing events detected by the SC (only the 1st branch), TW, CALO and Neutron detectors. All the quantities calculated for single TW channels are marked with A/B in the branches of the final tree.

## Running Reconstruction
Each executable compiled provides an help function, run the executable without any parameter to display it.
E.g.,
```
>> ./Reconstruction

-x, --channelmap arg        Channel Map XML file,
-i, --inputfilename arg     WaveDAQ binary (.bin) or TDAQ raw data (.data) input filename,
-o, --outputfilename arg    output filename (should be .root),
-t, --timecalfile arg       (optional) WaveDAQ time calibration (.dat) filename,
-g, --gain arg              (optional) gain set to perform the acquisition (default: 1),
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

* SC_Timestamp, TriggerType, IsFragTriggerOn, EventNumber and Tags as defined below
* A branch with WFs from neutron slow channels
* A branch with WFs from neutron fast channels

For each WF, the quantities saved are:

* V: array of 1024 float values containing the amplitudes of the WF
* T: array of 1024 float values containing the time bins of the WF
* IsOn: A boolean flag signaling if the channel was activated or not

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

## Batch running on the Tier1 HTCondor resources
A bash script to run the SLIPPER "Reconstruction" executable in batch on the HTCondor resources of Tier1, called "runSlipperBatchT1.sh", is now available in the repository. The detailed usage instructions are written at the beginning of the file, here only a summary of the possible options is reported:

```
>> ./runSlipperBatch.sh

-i      path to directory containing the input files
-o      path to directosy where to write the output files
-x      channel map XML file
-f      first run to process
-l      last run to process (optional)
```

The script creates a ".sh" and a ".sub" file for each run you want to process and submits the corresponding job. These files are stored in an auxiliarry directory "HTCfiles" created inside the chosen output folder.

The only real requirement for the script is the presence of the WaveDAQ time calibration file inside the output folder.

**N.B.: Carefully read the instructions written inside the script before running it**

## Output ROOTfile
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
