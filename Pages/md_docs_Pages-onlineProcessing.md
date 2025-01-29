---
title: Online Processing

---

# Online Processing



From version 3.1, a **LivePlotter** executable is available. This executable is called by the src/PyRoutines/Plotter.py routine in a dedicated thread and its purpose is to provide some online information during data takings. The only argument needed by the LivePlotter is the directory containing output files from the Reconstruction executable. The routine will then check the directory continuously and update the online plots as soon as a new ".root" file is added. Right now the plots implemented in the LivePlotter are:

* TW hitmaps with MB and Fragmentation trigger
* Calibrated trigger amplitude seen by the TCB discriminators for all the channels involved in the fragmentation trigger logic.
* Raw Fragmentation dE spectra for all the TW bars involved in the fragmentation trigger, for the chosen trigger thresholds (set via the TriggerAmpMap.txt file )
* Pile-Up percentage in each file
* Total number of counts in the A-B channels of the TW
* Total number of "saturated" counts (amplitude > 1V) in the A-B channels of the TW
* Raw energy loss vs TOF at the center of the TW
* Raw Energy deposition in all the CALO crystals
* TW bars - CALO crystals multiplicity
* _[preliminary]_ Comparison between raw CALO energy and TW raw energy loss
The best way to run the LivePlotter is to call it through the dedicated Python routine src/PyRoutines/Plotter.py. The options available for this routine are listed below:



```cpp
>> python3 src/PyRoutines/Plotter.py [OPTION...]

  -x, --channelmap      Channel Map of the acquisition
  -i, --inputdir        Input files directory
  -o, --outputdir       Output files directory
  -c, --timecal         (optional) WaveDAQ time calibration file (.dat)
  -b, --beam            (optional) Wether to activate (1) or not (0) the online plot of beam rate (default=0)
  -t, --trig            (optional) Trigger calibration file (default="")
  -p, --plots           (optional) Wether to activate (1) or not (0) the online plots (default=1)
```

A typical command line for the Plotter.py routine is: 

```cpp
python3 src/PyRoutines/Plotter.py -x config/ChannelMap*.xml -i InputDir -o OutputDir -c tcalib*.dat -b 1 -t config/TriggerAmpMap*.txt
```

where '*' indicates the acquisition campaign.

This command will launch a 3-thread process, with each of the involved threads dedicated to a specific task:

* Online processing of data: this thread is handled propagating the options to the "src/PyRoutines/RecoMonitor.py" routine. This program continuously checks the input folder and runs the reconstruction on all the new files found.
* Beam rate monitoring (updated and plotted online): this thread can be switched off with the option "-b 0".
* Online plotting (LivePlotter): this thread takes care of handling all the configured online plots. It can be switched off with the option "-p 0".
The online monitoring of data can be performed on both WaveDAQ and TDAQ files. The difference, as for the other executables, is given by the need of a WaveDAQ time calibration file in the latter case. If no time calibration file is specified, the executable expects WaveDAQ binary files as input.

**This tool is intended for online monitoring during data acquisitions ONLY!!**

-------------------------------

Updated on 2025-01-29 at 16:37:30 +0000
