---
title: Event Display

---

# Event Display



The **EventDisplay** executable can be used to open an event display dedicated to the control of the signals acquired by the SC, TW and CALO detectors. The basic functioning of this executable is straightforward: it opens a canvas for each detector present in the channel map and plots all the waveforms from that detector in the dedicated canvas. There is the possibility to move to the following event via a dedicated input dialog window that opens when the executable is launched.

The parameters needed by the EventDisplay executable can be seen through the help function. To see it, run the code with no options:



```cpp
>> ./EventDisplay [OPTION...]

  -x, --channelmap       Channel Map XML file
  -i, --inputfilename    WaveDAQ binary (.bin) or TDAQ raw data (.data) input filename
  -c, --timecalfile      (optional) WaveDAQ time calibration filename
      --board            (optional) WaveDAQ specific board to check
      --channel          (optional) WaveDAQ specific channel to check
      --clk              (optional) Include clock plots (default: 0)
```

The first three parameters are the same described for the "Reconstruction" executable. By default, the CLK signals are not displayed in the canvases. The "--clk" option can be used to enable the display of the CLK signals by launching



```cpp
>> ./bin/EventDisplay -x config/ChannelMap*.xml -i path/to/InputFile -c path/to/TimeCalibrationFile --clk 1
```

The "EventDisplay" executable is also capable of saving the output canvases and single waveforms for a specific event to a ROOT file. This feature can be exploited via the input dialog box.

The default behavior of this executable shows the waveforms for all detectors in the Channel Map in each event acquired. There is the possibility to only look at events where a specific WaveDAQ board-channel pair has been fired. This feature can be activated by specifying the "--board" and "--channel" parameters. 

-------------------------------

Updated on 2025-02-26 at 13:36:50 +0000
