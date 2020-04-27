---
title: 在查询中使用带批注的 XSD 架构（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c435ff3bacecb101784695fe42b8b2158625e058
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014469"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查询中使用带批注的 XSD 架构 (SQLXML 4.0)
  通过在模板中针对 XSD 架构指定 XPath 查询，可以针对带批注的架构指定查询以从数据库检索数据。  
  
 通过** \<sql： xpath 查询>** 元素，你可以针对由批注的架构定义的 XML 视图指定 xpath 查询。 `mapping-schema` **使用\<sql： xpath 查询>** 元素的属性标识要对其执行 XPath 查询的批注架构。  
  
 模板是包含一个或多个查询的有效 XML 文档。 FOR XML 和 XPath 查询返回文档片段。 模板用作文档片段的容器；因此，模板提供了一种指定单个顶级元素的方法。  
  
 本主题中的示例使用模板针对带批注的架构指定 XPath 查询以从数据库检索数据。  
  
 例如，请看下面这个带批注的架构：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 为了便于说明，此 XSD 架构存储在一个名为 Schema2.xml 的文件中。 这样，就可以在下面的模板文件 (Schema2T.xml) 中指定针对带批注的架构的 XPath 查询：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 然后，您可以创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以将此查询作为模板文件的一部分执行。 有关详细信息，请参阅[SQLXML 4.0&#41;中 &#40;弃用的带批注 XDR 架构](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用内联映射架构  
 可以在模板中直接包含带批注的架构，这样就可以在模板中针对内联架构指定 XPath 查询。 模板也可以是一个 updategram。  
  
 模板中可包含多个内联架构。 若要使用模板中包含的内联架构，请在** \<xsd： schema>** 元素上指定具有唯一值的**id**属性，然后使用 **#idvalue**引用内联架构。 **Id**属性在行为上与 XDR 架构中使用的**sql： id** （{urn：架构-microsoft com： xml} id）的行为相同。  
  
 例如，下面的模板指定两个带批注的内联架构：  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 该模板还指定了两个 XPath 查询。 每个** \<xpath 查询>** 元素都通过指定`mapping-schema`属性来唯一标识映射架构。  
  
 在模板中指定内联架构时，还必须在`sql:is-mapping-schema` ** \<xsd： schema>** 元素上指定批注。 `sql:is-mapping-schema` 取布尔值（0=false，1=true）。 带有 sql：的内联架构**为-映射-schema = "1"** 被视为内联批注的架构，不在 XML 文档中返回。  
  
 `sql:is-mapping-schema` 批注属于模板命名空间 `urn:schemas-microsoft-com:xml-sql`。  
  
 若要测试该示例，请在本地目录中保存该模板 (InlineSchemaTemplate.xml)，然后创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行该模板。 有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了在模板中的`mapping-schema` ** \<sql： xpath 查询>** 元素上指定属性（在存在 xpath 查询时），或在 updategram 中的** \<updg： sync>** 元素上，你可以执行以下操作：  
  
-   在模板`mapping-schema`的** \<根>** 元素（全局声明）上指定属性。 这样，该映射架构就成为默认架构，并将由无显式 `mapping-schema` 批注的所有 XPath 和 updategram 节点使用。  
  
-   使用 ADO `mapping schema` 对象指定 `Command` 属性。  
  
 Xpath 查询`mapping-schema`>或** \<updg： sync>** 元素上指定的属性具有最高优先级; ** \<** ADO `Command`对象的优先级最低。  
  
 请注意，如果在模板中指定 XPath 查询，但未指定用于执行 XPath 查询的映射架构，则 XPath 查询将被视为**dbobject**类型的查询。 例如，考虑以下模板：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 该模板指定了一个 XPath 查询，但未指定映射架构。 因此，此查询将被视为**dbobject**类型的查询，其中 ProductPhoto 是表名称， @ProductPhotoID= ' 100 ' 是一个谓词，用于查找 ID 值为100的产品照片。 @LargePhoto要从中检索值的列。  
  
  
