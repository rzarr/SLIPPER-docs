---
title: Software for Live Interactive Plotting and Partial Event Reconstruction

---

# Software for Live Interactive Plotting and Partial Event Reconstruction




# Project     : FOOT (FragmentatiOn Of Target)

![FOOT_logo.png](/images/FOOT_logo.png)
 Software for stand-alone signal processing of the WaveDAQ system. For a detailed user guide, check the dedicated page in this manual or at the [*baltig page*](https://baltig.infn.it/zarrella/slipper/). The previous link can also be used to acces the source code.

At this stage, the code handles signals from the:

* Start Counter (SC)
* TOF-Wall (TW)
* Calorimeter (CALO)
* Neutron detectors

## Authors



* Niccolo' Camarlinghi (NC) -> Development of first Software structure
* Luca Galli (LC) -> First implementation
* Marco Montefiori (MM) -> First implementation of WaveDAQ histograms and [DataAnalysis](/Classes/classDataAnalysis.md) class
* Roberto Zarrella (RZ) -> Inclusion of all detectors, optimization and documentation of the code; Currently main developer

## Current contibutors



* Esther Ciarrocchi (EC)
* Aafke Kraan (AK)
* Roberto Zarrella (RZ, Mantainer)

## Content

This manual contains all the information about classes, files and functions implemented in SLIPPER. The manual is generated using Doxygen and Doxybook2 or Baltig pages.


## Revisions



------------------


| Timestamp  | Author  | Version  | Description   |
|  -------- | -------- | -------- | -------- |
| 01/01/2018  | LG  | 1.00  | Initial creation.   |
| 11/12/2018  | NC  | 1.1  | Developing of new features   |
| 10/10/2019  | RZ  | 2.0+  | Changing code structure and adding SC-CALO   |
| 01/06/2021  | MM  | 2.4+  | First implementation of histos and analysis script   |
| 16/12/2021  | RZ  | 3.0+  | Added Neutron detectors, TDAQ handling and first full documentation   |
| 15/06/2022  | RZ  | 3.1+  | Added LivePlotter and Docker image support   |

-------------------------------

Updated on 2025-01-27 at 18:13:43 +0000
