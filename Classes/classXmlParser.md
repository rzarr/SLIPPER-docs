---
title: XmlParser
summary: Class that handles all the decoding of XML configuration files for Channel Maps. 

---

# XmlParser



Class that handles all the decoding of XML configuration files for Channel Maps. 

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[XmlParser](/Classes/classXmlParser.md#function-xmlparser)**()<br>Default constructor.  |
| | **[~XmlParser](/Classes/classXmlParser.md#function-~xmlparser)**()<br>Default destructor.  |
| void | **[ReadFile](/Classes/classXmlParser.md#function-readfile)**(std::string FileName)<br>Open the xml file.  |
| void | **[PrintXmlContent](/Classes/classXmlParser.md#function-printxmlcontent)**()<br>Show the content of the xml file.  |
| void | **[ExportToFile](/Classes/classXmlParser.md#function-exporttofile)**(std::string Filename, XMLDocPointer_t mainnode)<br>Export a main node to file.  |
| std::vector< XMLNodePointer_t > | **[GetChildNodesByName](/Classes/classXmlParser.md#function-getchildnodesbyname)**(XMLNodePointer_t StartingNode, std::string NodeName)<br>Get all the first generation child of a node (StartingNode) whose name is (NodeName)  |
| Int_t | **[GetContentAsInt](/Classes/classXmlParser.md#function-getcontentasint)**(std::string Name, XMLNodePointer_t Node)<br>Return the content of a node as Int_t.  |
| std::vector< Int_t > | **[GetContentAsIntVec](/Classes/classXmlParser.md#function-getcontentasintvec)**(std::string Name, XMLNodePointer_t Node)<br>Return the content of a node as a vector of Int_t.  |
| std::vector< UShort_t > | **[GetContentAsShortVec](/Classes/classXmlParser.md#function-getcontentasshortvec)**(std::string Name, XMLNodePointer_t Node)<br>Return the content of a node as a vector of UShort_t.  |
| std::string | **[GetContentAsString](/Classes/classXmlParser.md#function-getcontentasstring)**(std::string Name, XMLNodePointer_t Node)<br>Return the content of a node as std::string.  |
| Double_t | **[GetContentAsDouble](/Classes/classXmlParser.md#function-getcontentasdouble)**(std::string Name, XMLNodePointer_t Node)<br>Return the content of a node as a double.  |
| XMLNodePointer_t | **[GetMainNode](/Classes/classXmlParser.md#function-getmainnode)**()<br>Get the document main node.  |
| XMLNodePointer_t | **[AddElement](/Classes/classXmlParser.md#function-addelement)**(std::string Name, XMLNodePointer_t ParentNode)<br>Add an element to an xml Node.  |
| XMLNodePointer_t | **[CreateMainNode](/Classes/classXmlParser.md#function-createmainnode)**(std::string Name)<br>Create a new main Node in the xml.  |
| void | **[AddElementWithContent](/Classes/classXmlParser.md#function-addelementwithcontent)**(std::string Name, XMLNodePointer_t ParentNode, std::string Value)<br>Add an element with content to and xml Node.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| TXMLEngine * | **[_XMLEngine](/Classes/classXmlParser.md#variable--xmlengine)** <br>Object to handle xml parsing engine.  |
| XMLDocPointer_t | **[_xmldoc](/Classes/classXmlParser.md#variable--xmldoc)** <br>Pointer to the actual xmlfile.  |

## Public Functions Documentation

### function XmlParser

```cpp
XmlParser()
```

Default constructor. 

Create the TXMLEngine 


### function ~XmlParser

```cpp
~XmlParser()
```

Default destructor. 

Desctructor takes care of destroying the _XMLEngine and _xmldoc 


### function ReadFile

```cpp
void ReadFile(
    std::string FileName
)
```

Open the xml file. 

**Parameters**: 

  * **FileName** Name of the input file 


### function PrintXmlContent

```cpp
void PrintXmlContent()
```

Show the content of the xml file. 

### function ExportToFile

```cpp
void ExportToFile(
    std::string Filename,
    XMLDocPointer_t mainnode
)
```

Export a main node to file. 

**Parameters**: 

  * **Filename** Name of the output file 
  * **mainnode** Main node to export 


### function GetChildNodesByName

```cpp
std::vector< XMLNodePointer_t > GetChildNodesByName(
    XMLNodePointer_t StartingNode,
    std::string NodeName
)
```

Get all the first generation child of a node (StartingNode) whose name is (NodeName) 

**Parameters**: 

  * **StartingNode** Main xml node for research 
  * **NodeName** Name of the child nodes to find 


**Return**: Vector of the child nodes of StartingNode with the wanted name 

Get the all the child node of StartingNode named NodeName 


### function GetContentAsInt

```cpp
Int_t GetContentAsInt(
    std::string Name,
    XMLNodePointer_t Node
)
```

Return the content of a node as Int_t. 

**Parameters**: 

  * **Name** Name of the child node where the content is stored 
  * **Node** Pointer to parent node 


**Return**: Content of the node as Int_t 

Get content of a node as Int_t. In case a node has no content an exception is thrown If there are none or multiple nodes named Name and exception is thrown 


### function GetContentAsIntVec

```cpp
std::vector< Int_t > GetContentAsIntVec(
    std::string Name,
    XMLNodePointer_t Node
)
```

Return the content of a node as a vector of Int_t. 

**Parameters**: 

  * **Name** Name of the child node where the content is stored 
  * **Node** Pointer to parent node 


**Return**: Content of the node as vector of Int_t 

Get content of a node as vector of Int_t. In case a node has no content an exception is thrown If there are none or multiple nodes named Name and exception is thrown 


### function GetContentAsShortVec

```cpp
std::vector< UShort_t > GetContentAsShortVec(
    std::string Name,
    XMLNodePointer_t Node
)
```

Return the content of a node as a vector of UShort_t. 

**Parameters**: 

  * **Name** Name of the child node where the content is stored 
  * **Node** Pointer to parent node 


**Return**: Content of the node as vector of UShort_t 

Get content of a node as vector of UShort_t. In case a node has no content an exception is thrown If there are none or multiple nodes named Name and exception is thrown 


### function GetContentAsString

```cpp
std::string GetContentAsString(
    std::string Name,
    XMLNodePointer_t Node
)
```

Return the content of a node as std::string. 

**Parameters**: 

  * **Name** Name of the child node where the content is stored 
  * **Node** Pointer to parent node 


**Return**: Content of the node as std::string 

Get content of a node as string. In case a node has no content an exception is thrown If there are none or multiple nodes named Name and exception is thrown 


### function GetContentAsDouble

```cpp
Double_t GetContentAsDouble(
    std::string Name,
    XMLNodePointer_t Node
)
```

Return the content of a node as a double. 

**Parameters**: 

  * **Name** Name of the child node where the content is stored 
  * **Node** Pointer to parent node 


**Return**: Content of the node as double 

Get content of a nodeas Float_t. In case a node has no content an exception is thrown If there are none or multiple nodes named Name and exception is thrown 


### function GetMainNode

```cpp
XMLNodePointer_t GetMainNode()
```

Get the document main node. 

**Return**: Pointer to the main node of the file 

### function AddElement

```cpp
XMLNodePointer_t AddElement(
    std::string Name,
    XMLNodePointer_t ParentNode
)
```

Add an element to an xml Node. 

**Parameters**: 

  * **Name** Name of the element to add 
  * **ParentNode** Pointer to the parent node 


**Return**: Pointer to the new element 

### function CreateMainNode

```cpp
XMLNodePointer_t CreateMainNode(
    std::string Name
)
```

Create a new main Node in the xml. 

**Parameters**: 

  * **Name** Name of the new main node 


**Return**: Pointer to the new node 

### function AddElementWithContent

```cpp
void AddElementWithContent(
    std::string Name,
    XMLNodePointer_t ParentNode,
    std::string Value
)
```

Add an element with content to and xml Node. 

**Parameters**: 

  * **Name** Name of the element to add 
  * **ParentNode** Pointer to the parent node 
  * **Content** Content of the new element 


## Protected Attributes Documentation

### variable _XMLEngine

```cpp
TXMLEngine * _XMLEngine;
```

Object to handle xml parsing engine. 

### variable _xmldoc

```cpp
XMLDocPointer_t _xmldoc;
```

Pointer to the actual xmlfile. 

-------------------------------

Updated on 2022-03-08 at 18:54:39 +0000