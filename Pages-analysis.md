Analysis
======

From version 2.5, a first analysis script has been implemented. This is meant to provide some fast information on the output of the Reconstruction executable and it's used as a run control routine. The parameters required by the executable are:
```
>> ./Analysis [OPTION...]

  -i, --inputfilename     Pre-processed input filename (.root)
  -o, --ouputfilename     Output filename (.root)
  -h, --help              Print help
```
As of today, the script produces a series of histograms to quickly check the correct functioning of TOF-Wall detector (channels/bars), as well as some preliminary time resolution studies.
