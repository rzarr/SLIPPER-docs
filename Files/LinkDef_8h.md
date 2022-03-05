---
title: src/LinkDef.h
summary: LinkDef of src folder. 

---

# src/LinkDef.h

LinkDef of src folder.  [More...](#detailed-description)

## Detailed Description

LinkDef of src folder. 

**Author**: R. Zarrella 



## Source code

```cpp

#ifdef __CINT__

#pragma link off all globals;
#pragma link off all classes;
#pragma link off all functions;


#pragma link C++ class CReadBinary+;
#pragma link C++ class WaveDaqReconstruction+;
#pragma link C++ class TOFWallCalibration+;
#pragma link C++ class DataAnalysis+;



#endif
```


-------------------------------

Updated on 2022-03-05 at 18:47:21 +0000
