---
title: Channel Map

---

# Channel Map




# XML configuration file: Channel Map

These files (available in the "config/" folder) contain the mapping between channels and SC, BARS and MODULES (wiring) for each campaign currently supported by the code. **This file is MANDATORY to run the Reconstrucion, EventDisplay and LivePlotter executables.** The Channel map should look like this: 

```cpp
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


### SC —> Start Counter

This field must contain:



* BOARD_ID: serial number of the SC board
* CHANNELS: list of the SC channels in the above board

### BAR —> TW bars

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

### MODULE —> Calorimeter modules

The channel map can also contain some calorimeter <MODULE> elements in the format shown above:



* MODULE_ID: the id of the module (must be unique)
* BOARD_ID: The WaveDREAM board(s) associated to the module. If two boards are indicated, the first channels up to number 15 are associated to the first board and the rest are linked to the second board
* CHANNELS: the Id of each WaveDREAM channel used for the Module
* CRYSTALS: the global Id of all the crystals of the module. Channels and crystals values have to be ordered in the same way because they are associated one-by-one.
* CRYSTAL_X/Y: Physical X/Y coordinates of the CALO crystals in the SHOE reference frame [OPTIONAL]

### NEUTRON —> Neutron detectors

Neutron detectors can be added to the channel map as above with fields:

* NAME: Name of the detector
* BOARD_FAST: WaveDREAM board used for fast signals
* CHANNELS_FAST: List of channels for fast signals
* GLOBAL_CH_FAST: Global channel Ids for fast channels
* BOARD_SLOW: WaveDREAM board used for slow signals
* CHANNELS_SLOW: List of channels for slow signals
* GLOBAL_CH_SLOW: Global channel Ids for slow channels
Note that the combination of (BOARD_ID,CHANNEL) should not appear more than once in the in the ChannelMap file. Moreover, crystal IDs MUST be numbered from 0 to NUMBEROFCRYSTALS - 1 (set in src/Parameters.h). The same applies to global channel Ids for the neutron detectors. 

-------------------------------

Updated on 2025-01-29 at 16:15:43 +0000
