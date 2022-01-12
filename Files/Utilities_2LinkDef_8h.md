---
title: src/Utilities/LinkDef.h
summary: LinkDef of Utilities folder. 

---

# src/Utilities/LinkDef.h

LinkDef of Utilities folder.  [More...](#detailed-description)

## Detailed Description

LinkDef of Utilities folder. 

**Author**: R. Zarrella 



## Source code

```cpp

#ifdef __CINT__

#pragma link off all globals;
#pragma link off all classes;
#pragma link off all functions;


#pragma link C++ class Message+;
#pragma link C++ class WDTag+;
#pragma link C++ class TDAQTag+;
#pragma link C++ class WDBDATA+;
#pragma link C++ class TCBDATA+;
#pragma link C++ class NeutronWF+;



#endif
```


-------------------------------

Updated on 2022-01-12 at 10:56:23 +0000
