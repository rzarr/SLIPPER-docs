---
title: src/Utilities/Message.h
summary: Header of Message.cxx. 

---

# src/Utilities/Message.h

Header of [Message.cxx](/Files/Message_8cxx.md#file-message.cxx).  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[Message](/Namespaces/namespaceMessage.md)** <br>Namespace that handles some os-independent output.  |

## Detailed Description

Header of [Message.cxx](/Files/Message_8cxx.md#file-message.cxx). 

**Author**: R. Zarrella 



## Source code

```cpp

#ifndef MESSAGE_H
#define MESSAGE_H
#include <iostream>
#include "TString.h"

namespace Message {
  void DisplayWarning(TString Message,std::ostream &os=std::cout);
  void DisplayFatalError(TString Message,std::ostream &os=std::cout);
  void DisplayMessage(TString Message,std::ostream &os=std::cout);
  void DisplayMessageWithEmphasys(TString Message,std::ostream &os=std::cout);
};
#endif
```


-------------------------------

Updated on 2021-12-29 at 14:24:53 +0000
