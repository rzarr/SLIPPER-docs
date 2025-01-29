Position Calibration
======

# Position Calibration
The "CalibratePosition" executable takes the output ROOT files created with the Reconstruction binary and produces the maps needed to correlate the hit position of particles along TW bars and the time difference between its A-B channels. This executable requires a Reconstruction output rootfile containing an homogenous scan of the TW with the same particle beam. An example of such runs are the so-called "Screensaver" runs tested at CNAO2022 or the TW scans of GSI2021 campaign.

The parameters needed by the CalibratePosition executable can be seen through the help function. Again, to display it, run the code with no options:

```
>> ./CalibratePosition [OPTION...]

  -i, --inputdatadir      input directory containing the reconstructed .rec.root files
  -s, --saveplots         (optional) Decide wether to save (1) or not (0) the debug plots (default=0)
```
The "-s" option saves additional plots in a ROOT file in the current directory. An example of command line could be (from the slipper directory):

```
>> ./bin/CalibratePosition -i path/to/input/file -s 1
```
The normal output of this executable is a position calibration map already in a format readable by SHOE. The information contained in this file are:

* barId -> Index of the TW bar
* v \[cm/ns\] -> light proagation velocity inside the TW bar
* dx|y_AB \[cm\] -> offset for position calculation
* layer(SHOE) -> index of the TW layer (1=X, 0=Y)