---
title: '通过使用 sql: hide 隐藏元素和属性 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- hiding elements
- element mapping [SQLXML], hiding attributes and elements
- hide annotation
- sql:hide
- table/view mapping [SQLXML], hiding attributes and elements
- table mapping [SQLXML], hiding attributes and elements
- hiding attributes
- annotated XSD schemas, hiding attributes and elements
- attribute mapping [SQLXML], hiding attributes and elements
- column mapping [SQLXML]
- element hiding [SQLXML]
- XSD schemas [SQLXML], hiding attributes and elements
- attribute hiding [SQLXML]
ms.assetid: 0978301b-f068-46b6-82b9-dc555161f52e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ce8daf2badb855cbf855031d93e38fb689eab54
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013828"
---
# <a name="hiding-elements-and-attributes-by-using-sqlhide"></a>使用 sql:hide 隐藏元素和属性
  针对 XSD 架构执行 XPath 查询时，生成的 XML 文档具有在架构中指定的元素和属性。 可以使用 `sql:hide` 批注来指定隐藏架构中的某些元素和属性。 当查询的选择条件需要架构中的特定元素或属性，但是不希望在生成的 XML 文档中返回这些元素或属性时，该批注很有用。  
  
 `sql:hide` 批注采用布尔值（0 = FALSE，1 = TRUE）。 可接受的值为 0、1、true 和 false。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlhide-on-an-attribute"></a>A. 对属性指定 sql:hide  
 此示例中的 XSD 架构组成 **\<Person.Contact >** 具有元素**ContactID**， **FirstName**，和**LastName**属性。  
  
 **\<Person.Contact >** 元素属于复杂类型，并因此，将映射到相同的名称 （默认映射） 的表。 所有属性**\<Person.Contact >** 元素均属于简单类型，并将映射到具有在 AdventureWorks 数据库中 Person.Contacttable 相同名称的列。 在架构中，`sql:hide`指定批注**ContactID**属性。 针对此架构指定 XPath 查询时**ContactID**不返回 XML 文档中。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID"  sql:hide="true" />   
       <xsd:attribute name="FirstName"   type="xsd:string" />   
       <xsd:attribute name="LastName"    type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 Hide.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 Hide.xml 的相同目录中将该文件另存为 HideT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Hide.xml">  
            /Person.Contact[@ContactID="1"]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (Hide.xml) 指定的目录路径是保存模板目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\Hide.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <Person.Contact FirstName="Gustavo" LastName="Achong" />   
</ROOT>  
```  
  
 如果对元素指定 `sql:hide`，则该元素及其属性或子元素都不会出现在生成的 XML 文档中。 下面是在其中的另一个 XSD 架构`sql:hide`上指定 **\<OD >** 元素：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:annotation>  
    <xsd:documentation>  
      Sales.Customer-Sales.SalesOrderHeader-Sales.SalesOrderDetail Schema  
      Copyright 2004 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="CustomerOrder"  
         parent="Sales.Customer"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Sales.SalesOrderHeader" />  
       <sql:relationship name="OrderOrderDetails"  
                  parent="Sales.SalesOrderHeader"  
                  parent-key="SalesOrderID"  
                  child-key="SalesOrderID"  
                  child="Sales.SalesOrderDetail"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Sales.Customer">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
                     maxOccurs="unbounded"   
                     sql:relationship="CustomerOrder">  
          <xsd:complexType>  
            <xsd:sequence>  
               <xsd:element name="OD" sql:relation="Sales.SalesOrderDetail"                                       maxOccurs="unbounded"                                       sql:relationship="OrderOrderDetails"                                       sql:hide="1">  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:string"/>  
                    <xsd:attribute name="ProductID" type="xsd:string"/>  
                  </xsd:complexType>  
               </xsd:element>  
            </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string"/>  
          <xsd:attribute name="OID" sql:field="SalesOrderID"   
                                    type="xsd:string"/>  
          <xsd:attribute name="OrderDate" type="xsd:date"/>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CID" sql:field="CustomerID"   
                                type="xsd:string"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在 XPath 查询时 (例如`/Customers[@CID="1"]`) 指定针对此架构生成的 XML 文档不包括 **\<OD >** 元素及其子项，如以下部分结果中所示：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers CID="1">  
    <Order CustomerID="1" OID="43860" OrderDate="2001-08-01" />   
    <Order CustomerID="1" OID="44501" OrderDate="2001-11-01" />   
    <Order CustomerID="1" OID="45283" OrderDate="2002-02-01" />   
    <Order CustomerID="1" OID="46042" OrderDate="2002-05-01" />   
  </Customers>  
</ROOT>  
```  
  
  
