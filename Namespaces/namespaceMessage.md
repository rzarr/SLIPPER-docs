---
title: Message
summary: Namespace that handles some os-independent output. 

---

# Message

Namespace that handles some os-independent output. 

## Functions

|                | Name           |
| -------------- | -------------- |
| void | **[DisplayWarning](/Namespaces/namespaceMessage.md#function-displaywarning)**(TString Message, std::ostream & os =std::cout)<br>Display a Warning.  |
| void | **[DisplayFatalError](/Namespaces/namespaceMessage.md#function-displayfatalerror)**(TString Message, std::ostream & os =std::cout)<br>Print a Fatal Error.  |
| void | **[DisplayMessage](/Namespaces/namespaceMessage.md#function-displaymessage)**(TString Message, std::ostream & os =std::cout)<br>Display a [Message](/Namespaces/namespaceMessage.md).  |
| void | **[DisplayMessageWithEmphasys](/Namespaces/namespaceMessage.md#function-displaymessagewithemphasys)**(TString Message, std::ostream & os =std::cout)<br>Display an emphsized message.  |


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

Print a Fatal Error. 

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






-------------------------------

Updated on 2022-06-10 at 15:57:01 +0000