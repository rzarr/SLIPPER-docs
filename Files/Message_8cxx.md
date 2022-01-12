---
title: src/Utilities/Message.cxx
summary: File containing all methods of Message namespace. 

---

# src/Utilities/Message.cxx

File containing all methods of [Message](/Namespaces/namespaceMessage.md) namespace.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[Message](/Namespaces/namespaceMessage.md)** <br>Namespace that handles some os-independent output.  |

## Detailed Description

File containing all methods of [Message](/Namespaces/namespaceMessage.md) namespace. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "Message.h"

void Message::DisplayWarning(TString Message, std::ostream &os)
{
  os << "WARNING: " << Message <<std::endl;
}


void Message::DisplayFatalError(TString Message,std::ostream &os)
{
  os << "FATAL ERROR: " << Message <<std::endl;
  throw -1;
}


void Message::DisplayMessage(TString Message,std::ostream &os)
{
  os << Message <<std::endl;
}

void Message::DisplayMessageWithEmphasys(TString Message,std::ostream &os)
{
  os << "=> " << Message <<std::endl;
}
```


-------------------------------

Updated on 2022-01-12 at 16:47:44 +0000
