---
title: 使用批注查询 (SQLXML 4.0) 中的 XSD 架构 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 47d16a95d65a6a155c906f81ba324bac684704af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>在查询中使用带批注的 XSD 架构 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  通过在模板中针对 XSD 架构指定 XPath 查询，可以针对带批注的架构指定查询以从数据库检索数据。  
  
  **\<Sql:xpath-查询 >**元素允许你指定 XPath 查询 XML 视图中定义的带批注的架构。 通过使用识别带批注的架构对其执行 XPath 查询是**映射架构**属性 **\<sql:xpath-查询 >**元素。  
  
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
  
 然后，您可以创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以将此查询作为模板文件的一部分执行。 有关详细信息，请参阅[批注 XDR 架构&#40;SQLXML 4.0 中弃用&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="using-inline-mapping-schemas"></a>使用内联映射架构  
 可以在模板中直接包含带批注的架构，这样就可以在模板中针对内联架构指定 XPath 查询。 模板也可以是一个 updategram。  
  
 模板中可包含多个内联架构。 若要使用模板中包含内联架构时，指定**id**属性具有一个唯一值 **\<xsd:schema >**元素，，然后使用**#idvalue**来引用内联架构。 **Id**属性是相同的行为到**sql:id** ({urn： 架构-microsoft-com:xml-sql} id) XDR 架构中使用。  
  
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
  
 该模板还指定了两个 XPath 查询。 每个 **\<xpath 查询 >**元素唯一标识映射架构通过指定**映射架构**属性。  
  
 当你在模板中，指定内联架构时**sql： 是映射架构**还必须在指定批注 **\<xsd:schema >**元素。 **Sql： 是映射架构**采用布尔值 (0 = false、 1 = true)。 使用内联架构**sql： 是映射架构 ="1"**视为内联带批注的架构，则不返回 XML 文档中。  
  
 **Sql： 是映射架构**批注属于模板命名空间**urn： 架构-microsoft-com:xml-sql**。  
  
 若要测试该示例，请在本地目录中保存该模板 (InlineSchemaTemplate.xml)，然后创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行该模板。 有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 除了指定**映射架构**属性 **\<sql:xpath-查询 >**元素在模板中 （当 XPath 查询），或在 **\<updg:sync >**元素中属的 updategram，你可以执行以下操作:  
  
-   指定**映射架构**属性**\<根 >**模板中的元素 （全局声明）。 此映射架构随后将成为中具有不明确的所有 XPath 和属的 updategram 的节点将都使用的默认架构**映射架构**批注。  
  
-   指定**映射架构**属性使用 ADO**命令**对象。  
  
 **映射架构**指定的属性 **\<xpath 查询 >**或 **\<updg:sync >**元素具有最高优先;ADO**命令**对象具有最低的优先级。  
  
 请注意，是否你在模板中指定 XPath 查询，并不指定对其执行 XPath 查询的映射架构，则 XPath 查询作为处理**dbobject**类型查询。 例如，考虑以下模板：  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 该模板指定了一个 XPath 查询，但未指定映射架构。 因此，此查询将被视为**dbobject** Production.ProductPhoto 处于表名称的类型查询和@ProductPhotoID="100"是一个谓词，查找具有的 ID 值为 100 的产品照片。 @LargePhoto 是要从中检索值的列。  
  
  
