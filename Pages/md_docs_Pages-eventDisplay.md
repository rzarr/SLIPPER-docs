---
title: Event Display

---

# Event Display




# Event Display

The "EventDisplay" executable can be used to open an event display dedicated to the control of the signals acquired by the SC, TW and CALO detectors. The basic functioning of this executable is straightforward: it opens a canvas for each detector present in the channel map and plots all the waveforms from that detector in the dedicated canvas. There is the possibility to move to the following event via a dedicated input dialog window that opens when the executable is launched.

The parameters needed by the EventDisplay executable can be seen through the help function. To see it, run the code with no options:



```cpp
>> ./EventDisplay [OPTION...]

  -x, --channelmap       Channel Map XML file
  -i, --inputfilename    WaveDAQ binary (.bin) input filename
  -c, --timecalfile      (optional) WaveDAQ time calibration filename
      --clk              (optional) Include clock plots (default: 0)
```

The first three parameters are the same described for the "Reconstruction" executable. By default, the CLK signals are not displayed in the canvases. The "--clk" option can be used to enable the display of the CLK signals by launching



```cpp
>> ./bin/EventDisplay -x config/ChannelMap*.xml -i path/to/InputFile -c path/to/TimeCalibrationFile --clk 1
```

The "EventDisplay" executable is also capable of saving the output canvases and single waveforms for a specific event to a ROOT file. This feature can be exploited via the input dialog box. 

-------------------------------

Updated on 2025-01-29 at 16:15:43 +0000
