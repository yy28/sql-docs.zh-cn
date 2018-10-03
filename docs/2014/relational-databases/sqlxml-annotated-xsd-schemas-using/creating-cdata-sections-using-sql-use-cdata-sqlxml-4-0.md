---
title: '创建 CDATA 部分使用 sql: use-(SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2695448ec0ada1af79348bc67c065123668949dd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48081581"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>使用 sql:use-cdata 创建 CDATA 节 (SQLXML 4.0)
  在 XML 中，CDATA 节用于对那些所含字符不转义则会识别为标记字符的特定文本块进行转义。  
  
 Microsoft 中的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有时会包含被 XML 分析器视为标记字符; 例如，尖括号字符 (\<和 >)，小于-比-或者-等于符号 (< =)，并与号 (&) 是视为标记字符。 但是，可以在 CDATA 节中对这类特殊字符进行包装，使它们不被视为标记字符。 XML 语法分析程序将 CDATA 节中的文本视为纯文本。  
  
 `sql:use-cdata` 批注用于指定应当将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回的数据包含在 CDATA 节中，就是说，它指示是否应当将由 `sql:field` 指定的列中的值包含在 CDATA 节中。 可以仅对映射到数据库列的元素指定 `sql:use-cdata` 批注。  
  
 `sql:use-cdata` 批注接受布尔值（0 = false，1 = true）。 可接受的值为 0、1、true 和 false。  
  
 该批注不能与 `sql:url-encode` 一起使用，也不能对 ID、IDREF、IDREFS、NMTOKEN 和 NMTOKENS 属性类型使用。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. 在元素上指定 sql:use-cdata  
 在以下架构中，`sql:use-cdata`设置为 1 (True)  **\<AddressLine1 >** 内**\<地址 >** 元素。 结果，将在 CDATA 节中返回数据。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 UseCData.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 UseCData.xml 的相同目录中将文件另存为 UseCDataT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (UseCData.xml) 指定的目录路径相对于保存模板的目录。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分结果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
