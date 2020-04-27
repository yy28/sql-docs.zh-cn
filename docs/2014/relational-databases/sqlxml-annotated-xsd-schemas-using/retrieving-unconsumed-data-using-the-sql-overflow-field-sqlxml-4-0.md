---
title: 使用 sql：溢出字段检索未用完的数据（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18651b91ee2a47819360eae4c57c18ac3eae672b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013779"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>使用 sql:overflow-field 检索未用完的数据 (SQLXML 4.0)
  使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML 函数将 XML 文档中的记录插入数据库时，源 XML 文档中所有未用完的数据可以存储在列中。 使用带批注的架构从数据库检索数据时，可指定 `sql:overflow-field` 属性以标识表中存储溢出数据的列。 可`sql:overflow-field`在** \<元素>** 上指定属性。  
  
 然后，可以通过以下方式检索此数据：  
  
-   将在溢出列中存储的属性添加到包含 `sql:overflow-field` 批注的元素。  
  
-   存储在数据库的溢出列中的子元素及其后代作为子元素添加在架构中显式指定的内容之后。 （顺序被打乱。）  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. 为元素指定 sql:overflow-field  
 本示例假定已运行了以下脚本，以便 tempdb 数据库中存在名为 Customers2 的表：  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 此外，必须为 tempdb 数据库创建虚拟目录，并创建名为 "template" 的`template`模板虚拟名称。  
  
 在以下示例中，映射架构检索 Customers2 表的 AddressOverflow 列中存储的未用完数据：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>针对架构测试示例 XPath 查询  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 Overflow.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 Overflow.xml 的相同目录中将该文件另存为 OverflowT.xml。 模板中的查询选择 Customers2 表中的记录。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (Overflow.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  
