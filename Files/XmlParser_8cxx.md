---
title: src/ChannelMap/XmlParser.cxx
summary: File containing all methods of XmlParser class. 

---

# src/ChannelMap/XmlParser.cxx

File containing all methods of [XmlParser](/Classes/classXmlParser.md) class.  [More...](#detailed-description)

## Detailed Description

File containing all methods of [XmlParser](/Classes/classXmlParser.md) class. 

**Author**: R. Zarrella 



## Source code

```cpp

#include "XmlParser.h"

XmlParser::XmlParser()
{
    _xmldoc=nullptr;
    //  create engine
    _XMLEngine= new TXMLEngine;
}


XmlParser::~XmlParser()
{
    // take care of the document
    if (_xmldoc!=nullptr)
    {
        _XMLEngine->FreeDoc(_xmldoc);
    }
    delete _XMLEngine;
}



void XmlParser::ReadFile(std::string FileName)
{
    // Only file with restricted xml syntax are supported
    _xmldoc = _XMLEngine->ParseFile(FileName.c_str());
    if (_xmldoc==0)
    {
        Error("ReadFile()", "Cannot open file %s", FileName.c_str());
        return;
    }
}


std::vector<XMLNodePointer_t> XmlParser::GetChildNodesByName(XMLNodePointer_t StartingNode, std::string NodeName)
{
    // get first child
    XMLNodePointer_t child = _XMLEngine->GetChild(StartingNode);
    std::vector<XMLNodePointer_t> NodeVec;
    // navigate all the first generation node
    while (child!=0)
    {
        // if current node name is equal to
        if (strcmp(_XMLEngine->GetNodeName(child), NodeName.c_str())==0)
        {
        NodeVec.push_back(child);
        }
        child = _XMLEngine->GetNext(child);
    }
    // return a vector containing all the selected nodes
    return NodeVec;
}


Int_t XmlParser::GetContentAsInt(std::string Name, XMLNodePointer_t Node)
{
    std::vector<XMLNodePointer_t> tmp= this->GetChildNodesByName(Node,Name);
    if (tmp.size()!=1)
    {
        throw -1;
    }
    const char* content=_XMLEngine->GetNodeContent(tmp[0]);
    if (content!=0)
    {
        return TString(content).Atoi();
    }
    throw -1;
}


std::string XmlParser::GetContentAsString(std::string Name,XMLNodePointer_t Node)
{
    std::vector<XMLNodePointer_t> tmp= this->GetChildNodesByName(Node,Name);
    if (tmp.size()!=1)
    {
        throw -1;
    }
    const char* content=_XMLEngine->GetNodeContent(tmp[0]);
    if (content!=0)
    {
        return std::string(content);
    }
    throw -1;
}

Double_t XmlParser::GetContentAsDouble(std::string Name,XMLNodePointer_t Node)
{
    std::vector<XMLNodePointer_t> tmp= this->GetChildNodesByName(Node,Name);
    if (tmp.size()!=1)
    {
        throw -1;
    }
    const char* content=_XMLEngine->GetNodeContent(tmp[0]);
    if (content!=0)
    {
        return TString(content).Atof();
    }
    throw -1;
}


std::vector<Int_t> XmlParser::GetContentAsIntVec(std::string Name, XMLNodePointer_t Node)
{
    std::vector<XMLNodePointer_t> tmp= this->GetChildNodesByName(Node,Name);
    if (tmp.size()<1)
    {
        throw -1;
    }

    std::string content = std::string(_XMLEngine->GetNodeContent(tmp[0]));
    std::vector<Int_t> values;

    // Skip delimiters at beginning.
    std::string::size_type lastPos = content.find_first_not_of(",", 0);
    // Find first "non-delimiter".
    std::string::size_type pos = content.find(",", lastPos);

    while (std::string::npos != pos || std::string::npos != lastPos)
    {
        // Found a token, add it to the vector.
        values.push_back(TString(content.substr(lastPos, pos - lastPos)).Atoi());
        // Skip delimiters.  Note the "not_of"
        lastPos = content.find_first_not_of(",", pos);
        // Find next "non-delimiter"
        pos = content.find(",", lastPos);

    }
    return values;
}


std::vector<UShort_t> XmlParser::GetContentAsShortVec(std::string Name, XMLNodePointer_t Node)
{
    std::vector<XMLNodePointer_t> tmp= this->GetChildNodesByName(Node,Name);
    if (tmp.size()<1)
    {
        throw -1;
    }

    std::string content = std::string(_XMLEngine->GetNodeContent(tmp[0]));
    std::vector<UShort_t> values;

    // Skip delimiters at beginning.
    std::string::size_type lastPos = content.find_first_not_of(",", 0);
    // Find first "non-delimiter".
    std::string::size_type pos = content.find(",", lastPos);

    while (std::string::npos != pos || std::string::npos != lastPos)
    {
        // Found a token, add it to the vector.
        values.push_back(TString(content.substr(lastPos, pos - lastPos)).Atoi());
        // Skip delimiters.  Note the "not_of"
        lastPos = content.find_first_not_of(",", pos);
        // Find next "non-delimiter"
        pos = content.find(",", lastPos);

    }
    return values;
}


XMLNodePointer_t XmlParser::GetMainNode()
{
  return _XMLEngine->DocGetRootElement(_xmldoc);
}


XMLNodePointer_t XmlParser::AddElement(std::string Name, XMLNodePointer_t ParentNode)
{
    return _XMLEngine->NewChild(ParentNode, 0, Name.c_str(),0);
}


void XmlParser::AddElementWithContent(std::string Name, XMLNodePointer_t ParentNode, std::string Content)
{
    _XMLEngine->NewChild(ParentNode, 0, Name.c_str(), Content.c_str());
}


XMLNodePointer_t XmlParser::CreateMainNode(std::string Name)
{
    return _XMLEngine->NewChild(0, 0, Name.c_str());
}


void XmlParser::ExportToFile(std::string Filename,XMLDocPointer_t mainnode)
{
    XMLDocPointer_t xmldoc = _XMLEngine->NewDoc();
    _XMLEngine->DocSetRootElement(xmldoc, mainnode);
     // Save document to file
    _XMLEngine->SaveDoc(xmldoc, Filename.c_str());
    _XMLEngine->FreeDoc(xmldoc);
}
```


-------------------------------

Updated on 2022-02-10 at 11:57:31 +0000
