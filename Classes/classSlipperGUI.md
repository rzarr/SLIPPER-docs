---
title: SlipperGUI
summary: Class containing all the methods needed to build the SLIPPER Graphical User Interface. 

---

# SlipperGUI



Class containing all the methods needed to build the SLIPPER Graphical User Interface. 

Inherits from TGMainFrame

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SlipperGUI](/Classes/classSlipperGUI.md#function-slippergui)**(const TGWindow * p, UInt_t w, UInt_t h)<br>Default constructor of the Graphical User Interface.  |
| virtual | **[~SlipperGUI](/Classes/classSlipperGUI.md#function-~slippergui)**()<br>Default destructor.  |
| void | **[AddPlotToGUI](/Classes/classSlipperGUI.md#function-addplottogui)**(TObject * h, std::string detector, Bool_t enableDividedCanvasDraw =false)<br>Add an object to those accessible by the GUI.  |
| | **[ClassDef](/Classes/classSlipperGUI.md#function-classdef)**([SlipperGUI](/Classes/classSlipperGUI.md) , 0 ) |
| void | **[CloseWindow](/Classes/classSlipperGUI.md#function-closewindow)**()<br>Close the GUI when the window gets closed.  |
| void | **[DrawDividedOnNewCanvas](/Classes/classSlipperGUI.md#function-drawdividedonnewcanvas)**()<br>Draw object on a separate canvas and show all the sub-objects of the container into different pads.  |
| void | **[DrawOnEmbeddedCanvas](/Classes/classSlipperGUI.md#function-drawonembeddedcanvas)**()<br>Draw an object on the canvas embedded in the GUI window.  |
| void | **[DrawOnSeparateCanvas](/Classes/classSlipperGUI.md#function-drawonseparatecanvas)**()<br>Spawn an additional canvas and draw the last selected object onto it.  |
| void | **[ResetCurrentPlot](/Classes/classSlipperGUI.md#function-resetcurrentplot)**()<br>Reset current or last selected plot.  |
| void | **[ResetPlots](/Classes/classSlipperGUI.md#function-resetplots)**()<br>Reset all plots.  |
| void | **[ShowListOfDetectorPlots](/Classes/classSlipperGUI.md#function-showlistofdetectorplots)**()<br>Show the list of plots associated with the chosen detector.  |
| void | **[UpdatePlots](/Classes/classSlipperGUI.md#function-updateplots)**()<br>Update all the pads spawned by the GUI.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AddDetector](/Classes/classSlipperGUI.md#function-adddetector)**(std::string detector)<br>Add a detector the ComboBox in the GUI.  |
| void | **[DrawOnCanvas](/Classes/classSlipperGUI.md#function-drawoncanvas)**(TCanvas * c)<br>Draw object on a canvas.  |
| TGLBEntry * | **[FindCurrentSelectedEntry](/Classes/classSlipperGUI.md#function-findcurrentselectedentry)**()<br>Fin the current selected plot.  |
| std::string | **[GetDetectorExtendedName](/Classes/classSlipperGUI.md#function-getdetectorextendedname)**(std::string detector)<br>Get the extended name of a detector.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< TObject *, bool > | **[_CanDrawOnDividedCanvas](/Classes/classSlipperGUI.md#variable--candrawondividedcanvas)** <br>Boolean flag indicating if an object can be drawn on the divided canvas.  |
| TGComboBox * | **[_DetComboBox](/Classes/classSlipperGUI.md#variable--detcombobox)** <br>ComboBox with list of the detectors.  |
| std::map< Int_t, std::string > | **[_DetIdToNameMap](/Classes/classSlipperGUI.md#variable--detidtonamemap)** <br>Map of the included detectors with their entryId in the ComboBox.  |
| TGButton * | **[_DrawButton](/Classes/classSlipperGUI.md#variable--drawbutton)** <br>Draw Button.  |
| TGButton * | **[_DrawDividedButton](/Classes/classSlipperGUI.md#variable--drawdividedbutton)** <br>Draw divided plots Button.  |
| TRootEmbeddedCanvas * | **[_EmbeddedCanvas](/Classes/classSlipperGUI.md#variable--embeddedcanvas)** <br>GUI Embedded canvas.  |
| TGButton * | **[_ExitButton](/Classes/classSlipperGUI.md#variable--exitbutton)** <br>Exit Button.  |
| TGGroupFrame * | **[_GroupFrameCombo](/Classes/classSlipperGUI.md#variable--groupframecombo)** <br>Group frame for the ComboBox of the detectors.  |
| std::map< std::string, TGGroupFrame * > | **[_GroupFrameDet](/Classes/classSlipperGUI.md#variable--groupframedet)** <br>Map of group frames for singe detectors.  |
| TGVerticalFrame * | **[_LeftFrame](/Classes/classSlipperGUI.md#variable--leftframe)** <br>Left frame of the GUI, containing buttons and frames for plot choice.  |
| std::map< std::string, TGListBox * > | **[_ListBoxDet](/Classes/classSlipperGUI.md#variable--listboxdet)** <br>Map of ListBoxes for detectors.  |
| TGMainFrame * | **[_MainFrame](/Classes/classSlipperGUI.md#variable--mainframe)** <br>GUI main frame.  |
| std::map< TGLBEntry *, TGraph * > | **[_MapOfGraphs](/Classes/classSlipperGUI.md#variable--mapofgraphs)** <br>Map of the TGraph (and derived) objects.  |
| std::map< TGLBEntry *, TH1 * > | **[_MapOfHistos](/Classes/classSlipperGUI.md#variable--mapofhistos)** <br>Map of the TH1 (and derived) objects.  |
| std::map< TGLBEntry *, THStack * > | **[_MapOfHistoStacks](/Classes/classSlipperGUI.md#variable--mapofhistostacks)** <br>Map of the THStack (and derived) objects.  |
| std::map< TGLBEntry *, TMultiGraph * > | **[_MapOfMultiGraphs](/Classes/classSlipperGUI.md#variable--mapofmultigraphs)** <br>Map of the TMultiGraph (and derived) objects.  |
| std::vector< TVirtualPad * > | **[_PadsToUpdate](/Classes/classSlipperGUI.md#variable--padstoupdate)** <br>List of Pads spawned by the GUI, useful for Pad update.  |
| TGButton * | **[_ResetButton](/Classes/classSlipperGUI.md#variable--resetbutton)** <br>Reset Button.  |
| TGButton * | **[_ResetCurrentButton](/Classes/classSlipperGUI.md#variable--resetcurrentbutton)** <br>Reset Button.  |

## Public Functions Documentation

### function SlipperGUI

```cpp
SlipperGUI(
    const TGWindow * p,
    UInt_t w,
    UInt_t h
)
```

Default constructor of the Graphical User Interface. 

**Parameters**: 

  * **p** Pointer to main window containing the GUI 
  * **w** Width of the window 
  * **h** Height of the window 


Build the GUI with all the frames and buttons needed to handle the online monitoring plots. At the moment, a list of plots is implemented for the SC, TW and CALO detectors. The GUI can correctly handle all objects of type "TH1", "THStack", "TGraph" and all inherited classes.

Three buttons are included in the current version:



* "Draw on another canvas": spawns an additional canvas and uses it to plot the selected item
* "Reset Plots": clears all the plots
* "Exit": Closes the GUI window and exits the program


### function ~SlipperGUI

```cpp
virtual ~SlipperGUI()
```

Default destructor. 

Clean up used widgets: frames, buttons, layout hints 


### function AddPlotToGUI

```cpp
void AddPlotToGUI(
    TObject * h,
    std::string detector,
    Bool_t enableDividedCanvasDraw =false
)
```

Add an object to those accessible by the GUI. 

**Parameters**: 

  * **obj** Pointer to the object 
  * **detector** Name of the detector relative to the added object 


### function ClassDef

```cpp
ClassDef(
    SlipperGUI ,
    0 
)
```


### function CloseWindow

```cpp
void CloseWindow()
```

Close the GUI when the window gets closed. 

This function is called by the "Exit" button 


### function DrawDividedOnNewCanvas

```cpp
void DrawDividedOnNewCanvas()
```

Draw object on a separate canvas and show all the sub-objects of the container into different pads. 

This function is called by the "Draw divided plots" button 


### function DrawOnEmbeddedCanvas

```cpp
void DrawOnEmbeddedCanvas()
```

Draw an object on the canvas embedded in the GUI window. 

Function activated by a double-click on the object you want to draw 


### function DrawOnSeparateCanvas

```cpp
void DrawOnSeparateCanvas()
```

Spawn an additional canvas and draw the last selected object onto it. 

This function is called by the "Draw on another canvas" button 


### function ResetCurrentPlot

```cpp
void ResetCurrentPlot()
```

Reset current or last selected plot. 

This function is called by the "Reset current plot" button 


### function ResetPlots

```cpp
void ResetPlots()
```

Reset all plots. 

This function is called by the "Reset plots" button 


### function ShowListOfDetectorPlots

```cpp
void ShowListOfDetectorPlots()
```

Show the list of plots associated with the chosen detector. 

The signal associated to this slot is a selection in the ComboBox 


### function UpdatePlots

```cpp
void UpdatePlots()
```

Update all the pads spawned by the GUI. 

## Protected Functions Documentation

### function AddDetector

```cpp
void AddDetector(
    std::string detector
)
```

Add a detector the ComboBox in the GUI. 

**Parameters**: 

  * **detector** Name of the detector that has to be added 


Allocate all necessary frames/listboxes for the addition of one detector to the GUI 


### function DrawOnCanvas

```cpp
void DrawOnCanvas(
    TCanvas * c
)
```

Draw object on a canvas. 

**Parameters**: 

  * **c** Pointer to canvas where to draw the object 


The function finds the container of the selected objects and automatically sets the draw options. Auxiliary function not callable from outside 


### function FindCurrentSelectedEntry

```cpp
TGLBEntry * FindCurrentSelectedEntry()
```

Fin the current selected plot. 

**Return**: Pointer to the TGLBEntry of the currently selected plot 

### function GetDetectorExtendedName

```cpp
std::string GetDetectorExtendedName(
    std::string detector
)
```

Get the extended name of a detector. 

**Parameters**: 

  * **detector** Name of the selected detector 


**Return**: Extended name of the selected detector 

Auxiliary function used for frame titles. Currently available detector are: "SC", "TW", "CALO", "WD" 


## Protected Attributes Documentation

### variable _CanDrawOnDividedCanvas

```cpp
std::map< TObject *, bool > _CanDrawOnDividedCanvas;
```

Boolean flag indicating if an object can be drawn on the divided canvas. 

### variable _DetComboBox

```cpp
TGComboBox * _DetComboBox;
```

ComboBox with list of the detectors. 

### variable _DetIdToNameMap

```cpp
std::map< Int_t, std::string > _DetIdToNameMap;
```

Map of the included detectors with their entryId in the ComboBox. 

### variable _DrawButton

```cpp
TGButton * _DrawButton;
```

Draw Button. 

### variable _DrawDividedButton

```cpp
TGButton * _DrawDividedButton;
```

Draw divided plots Button. 

### variable _EmbeddedCanvas

```cpp
TRootEmbeddedCanvas * _EmbeddedCanvas;
```

GUI Embedded canvas. 

### variable _ExitButton

```cpp
TGButton * _ExitButton;
```

Exit Button. 

### variable _GroupFrameCombo

```cpp
TGGroupFrame * _GroupFrameCombo;
```

Group frame for the ComboBox of the detectors. 

### variable _GroupFrameDet

```cpp
std::map< std::string, TGGroupFrame * > _GroupFrameDet;
```

Map of group frames for singe detectors. 

### variable _LeftFrame

```cpp
TGVerticalFrame * _LeftFrame;
```

Left frame of the GUI, containing buttons and frames for plot choice. 

### variable _ListBoxDet

```cpp
std::map< std::string, TGListBox * > _ListBoxDet;
```

Map of ListBoxes for detectors. 

### variable _MainFrame

```cpp
TGMainFrame * _MainFrame;
```

GUI main frame. 

### variable _MapOfGraphs

```cpp
std::map< TGLBEntry *, TGraph * > _MapOfGraphs;
```

Map of the TGraph (and derived) objects. 

### variable _MapOfHistos

```cpp
std::map< TGLBEntry *, TH1 * > _MapOfHistos;
```

Map of the TH1 (and derived) objects. 

### variable _MapOfHistoStacks

```cpp
std::map< TGLBEntry *, THStack * > _MapOfHistoStacks;
```

Map of the THStack (and derived) objects. 

### variable _MapOfMultiGraphs

```cpp
std::map< TGLBEntry *, TMultiGraph * > _MapOfMultiGraphs;
```

Map of the TMultiGraph (and derived) objects. 

### variable _PadsToUpdate

```cpp
std::vector< TVirtualPad * > _PadsToUpdate;
```

List of Pads spawned by the GUI, useful for Pad update. 

### variable _ResetButton

```cpp
TGButton * _ResetButton;
```

Reset Button. 

### variable _ResetCurrentButton

```cpp
TGButton * _ResetCurrentButton;
```

Reset Button. 

-------------------------------

Updated on 2025-01-29 at 16:16:32 +0000