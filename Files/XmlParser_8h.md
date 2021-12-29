---
title: src/ChannelMap/XmlParser.h
summary: Header of XmlParser.cxx. 

---

# src/ChannelMap/XmlParser.h

Header of [XmlParser.cxx](/Files/XmlParser_8cxx.md#file-xmlparser.cxx).  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[XmlParser](/Classes/classXmlParser.md)** <br>Class that handles all the decoding of XML configuration files for Channel Maps.  |

## Detailed Description

Header of [XmlParser.cxx](/Files/XmlParser_8cxx.md#file-xmlparser.cxx). 

**Author**: N. Camarlinghi and R. Zarrella 



## Source code

```cpp

#ifndef XMLREADER_H
#define XMLREADER_H
#include "TXMLEngine.h"
#include "Message.h"
#include "TF1.h"


class XmlParser
{
    TXMLEngine *_XMLEngine;     
    XMLDocPointer_t _xmldoc;    

public:
    XmlParser();
    ~XmlParser();

    void ReadFile(std::string FileName);
    void                            PrintXmlContent();
    void                            ExportToFile(std::string Filename,XMLDocPointer_t mainnode);

    std::vector<XMLNodePointer_t>   GetChildNodesByName(XMLNodePointer_t StartingNode, std::string NodeName);
    Int_t                           GetContentAsInt(std::string Name,XMLNodePointer_t Node);
    std::vector<Int_t>              GetContentAsIntVec(std::string Name,XMLNodePointer_t Node);
    std::vector<UShort_t>           GetContentAsShortVec(std::string Name,XMLNodePointer_t Node);
    std::string                     GetContentAsString(std::string Name,XMLNodePointer_t Node);
    Double_t                        GetContentAsDouble(std::string Name,XMLNodePointer_t Node);
    XMLNodePointer_t                GetMainNode();

    XMLNodePointer_t                AddElement(std::string Name, XMLNodePointer_t ParentNode);
    XMLNodePointer_t                CreateMainNode(std::string Name);
    void                            AddElementWithContent(std::string Name, XMLNodePointer_t ParentNode, std::string Value);
};
#endif
```


-------------------------------

Updated on 2021-12-29 at 14:24:53 +0000
