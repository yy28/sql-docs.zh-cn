---
title: 请求 URL 引用 BLOB 数据使用 sql： 进行编码 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1ac063a644bf9d7be7cc55b3b413d81cf2ae5974
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254702"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>使用 sql:encode 请求 BLOB 数据的 URL 引用 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在带批注的 XSD 架构中，将属性（或元素）映射为 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 BLOB 列时，将在 XML 中以 Base 64 编码格式返回数据。  
  
 如果你想对数据的引用 (URI) 要返回的可用于更高版本中检索二进制格式的 BLOB 数据，指定**sql： 编码**批注。 您可以指定**sql： 编码**上的属性或元素的简单类型。  
  
 指定**sql： 编码**批注以指示应而不是字段的值返回给字段的 URL。 **sql： 编码**取决于要在 URL 中生成单一选择的主键。 可以使用指定的主键**sql:key-字段**批注。  
  
 **Sql： 编码**"url"或"default"值，可以分配批注。 值为“default”将返回 Base 64 编码格式的数据。  
  
 **Sql： 编码**批注不能用于**sql: use-cdata**或 ID、 IDREF、 IDREFS、 NMTOKEN 或 NMTOKENS 属性类型。 它还不能使用与 XSD**修复**属性。  
  
> [!NOTE]  
>  BLOB 类型的列不能用作键或外键的一部分。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. 指定 sql:encode 以获取对 BLOB 数据的 URL 引用  
 在此示例中，指定映射架构**sql： 编码**上**LargePhoto**要检索 （而不是检索二进制数据在 Base 64-特定产品照片的 URI 引用特性编码格式）。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 sqlEncode.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 sqlEncode.xml 的相同目录中将该文件另存为 sqlEncodeT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (sqlEncode.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是结果：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
