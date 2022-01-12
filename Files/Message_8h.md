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

## Functions

|                | Name           |
| -------------- | -------------- |
| void | **[DisplayWarning](/Files/Message_8h.md#function-displaywarning)**(TString Message, std::ostream & os =std::cout)<br>Display a Warning.  |
| void | **[DisplayFatalError](/Files/Message_8h.md#function-displayfatalerror)**(TString Message, std::ostream & os =std::cout)<br>Throw a Fatal Error.  |
| void | **[DisplayMessage](/Files/Message_8h.md#function-displaymessage)**(TString Message, std::ostream & os =std::cout)<br>Display a [Message](/Namespaces/namespaceMessage.md).  |
| void | **[DisplayMessageWithEmphasys](/Files/Message_8h.md#function-displaymessagewithemphasys)**(TString Message, std::ostream & os =std::cout)<br>Display an emphsized message.  |

## Detailed Description

Header of [Message.cxx](/Files/Message_8cxx.md#file-message.cxx). 

**Author**: R. Zarrella 

## Functions Documentation

### function DisplayWarning

```cpp
void DisplayWarning(
    TString Message,
    std::ostream & os =std::cout
)
```

Display a Warning. 

**Parameters**: 

  * **[Message](/Namespaces/namespaceMessage.md)** Text of the warning 
  * **os** ostream object 


### function DisplayFatalError

```cpp
void DisplayFatalError(
    TString Message,
    std::ostream & os =std::cout
)
```

Throw a Fatal Error. 

**Parameters**: 

  * **[Message](/Namespaces/namespaceMessage.md)** text of the error 
  * **os** ostream object 


### function DisplayMessage

```cpp
void DisplayMessage(
    TString Message,
    std::ostream & os =std::cout
)
```

Display a [Message](/Namespaces/namespaceMessage.md). 

**Parameters**: 

  * **[Message](/Namespaces/namespaceMessage.md)** text of the [Message](/Namespaces/namespaceMessage.md)
  * **os** ostream object 


### function DisplayMessageWithEmphasys

```cpp
void DisplayMessageWithEmphasys(
    TString Message,
    std::ostream & os =std::cout
)
```

Display an emphsized message. 

**Parameters**: 

  * **[Message](/Namespaces/namespaceMessage.md)** Text of the message 
  * **os** ostream object 




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

Updated on 2022-01-12 at 10:56:23 +0000
