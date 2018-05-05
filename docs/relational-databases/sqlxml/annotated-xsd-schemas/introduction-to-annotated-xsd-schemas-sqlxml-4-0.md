---
title: 批注的 XSD 架构 (SQLXML 4.0) 简介 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8b771edea6a71767e05e9d24c3ddd542bae2930c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>带批注的 XSD 架构简介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以通过使用 XML 架构定义 (XSD) 语言创建关系数据的 XML 视图。 然后可通过使用 XML Path 语言 (XPath) 查询对这些视图进行查询。 这是类似于通过使用 CREATE VIEW 语句，然后指定针对视图的 SQL 查询创建视图。  
  
 XML 架构描述了 XML 文档的结构并且还描述了对文档中数据的各种约束。 针对该架构指定 XPath 查询时，返回的 XML 文档的结构由对其执行 XPath 查询的架构确定。  
  
 在 XSD 架构中，  **\<xsd:schema >** 元素包含整个架构; 所有元素声明必须都包含在 **\<xsd:schema >** 元素。 你可以描述这些特性定义中的命名空间架构驻留和在架构中使用的属性作为命名空间 **\<xsd:schema >** 元素。  
  
 必须包含有效的 XSD 架构 **\<xsd:schema >** 元素定义，如下所示：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 **\<Xsd:schema >** 元素派生自的 XML 架构命名空间规范http://www.w3.org/2001/XMLSchema。  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD 架构的批注  
 您可以对 XSD 架构使用批注来描述数据库映射、查询数据库并返回 XML 文档形式的结果。 使用批注可将 XSD 架构映射到数据库表和列。 可以对 XSD 架构创建的 XML 视图指定 XPath 查询来查询数据库并获取 XML 形式的结果。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 架构语言支持随 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 中带批注的 XML-Data Reduced (XDR) 架构语言引入的批注。 SQLXML 4.0 中不推荐使用带批注的 XDR。  
  
 在关系数据库上下文中，将任意 XSD 架构映射到关系存储区很有用。 实现这种映射的一种方法是对 XSD 架构进行批注。 将批注 XSD 架构称为*映射架构*，它提供有关如何将 XML 数据映射到关系存储的信息。 实际上，映射架构是关系数据的 XML 视图。 使用这些映射能够以 XML 文档形式检索关系数据。  
  
## <a name="namespace-for-annotations"></a>批注的命名空间  
 在 XSD 架构中，使用命名空间指定批注**urn： 架构-microsoft-com:mapping-架构**。 下面的示例中所示，指定的命名空间的最简单方法是指定在 **\<xsd:schema >** 标记。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 命名空间可采用任意前缀。 在本文档中， **sql**前缀用于表示批注命名空间并将此命名空间中的批注与其他命名空间中的那些区分开来。  
  
## <a name="example-of-an-annotated-xsd-schema"></a>带批注的 XSD 架构的示例  
 以下示例中，在 XSD 架构组成 **\<Person.Contact >** 元素。 **\<员工 >** 元素具有**ContactID**属性和 **\<FirstName >** 和 **\<姓氏 >** 子元素：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 向该 XSD 架构添加批注以将其元素和属性映射到数据库表和列：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在映射架构中， **\<联系人 >** 元素映射到示例 AdventureWorks 数据库中的 Person.Contact 表上，通过使用**sql:relation**批注。 ConID、 FName 和 LName 属性映射到 Person.Contact 表中的 ContactID、 FirstName 和 LastName 列使用**sql:field**批注。  
  
 此带有批注的 XSD 架构提供了关系数据的 XML 视图。 可使用 XPath 语言查询此 XML 视图。 XPath 查询返回的结果是一个 XML 文档，而 SQL 查询返回的结果是行集。  
  
> [!NOTE]  
>  在映射架构中，指定关系值（如表名和列名）是否区分大小写取决于 SQL Server 是否使用区分大小写的排序规则设置。 有关详细信息，请参阅 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="other-resources"></a>其他资源  
 有关 XML 架构定义语言 (XSD)、XML Path 语言 (XPath) 和可扩展样式表语言转换 (XSLT) 的详细信息，请访问以下网站：  
  
-   XML 架构第 0 部分： 入门，W3C 建议 (http://www.w3.org/TR/xmlschema-0/)  
  
-   XML 架构第 1 部分： 结构，W3C 建议 (http://www.w3.org/TR/xmlschema-1/)  
  
-   XML 架构第部分 2:Datatypes，W3C 建议 (http://www.w3.org/TR/xmlschema-2/)  
  
-   XML 路径语言 (XPath) (http://www.w3.org/TR/xpath)  
  
-   XSL 转换 (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>另请参阅  
 [批注架构安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [批注 XDR 架构&#40;在 SQLXML 4.0 中已过时&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
