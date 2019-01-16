---
title: 带批注的 XSD 架构 (SQLXML 4.0) 简介 |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04e34b343ba92fcd8602f2b296e90de2a147fbba
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255942"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>带批注的 XSD 架构简介 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以通过使用 XML 架构定义 (XSD) 语言创建关系数据的 XML 视图。 然后可通过使用 XML Path 语言 (XPath) 查询对这些视图进行查询。 这是类似于通过使用 CREATE VIEW 语句，然后指定 SQL 查询对视图创建视图。  
  
 XML 架构描述了 XML 文档的结构并且还描述了对文档中数据的各种约束。 针对该架构指定 XPath 查询时，返回的 XML 文档的结构由对其执行 XPath 查询的架构确定。  
  
 在 XSD 架构中，  **\<xsd: schema >** 元素包含整个架构; 所有元素声明必须都包含在 **\<xsd: schema >** 元素。 可以定义中的命名空间的属性来描述该架构所在和属性的形式在架构中使用的命名空间 **\<xsd: schema >** 元素。  
  
 必须包含有效的 XSD 架构 **\<xsd: schema >** 元素定义，如下所示：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 **\<Xsd: schema >** 元素派生自的 XML 架构命名空间规范 http://www.w3.org/2001/XMLSchema 。  
  
## <a name="annotations-to-the-xsd-schema"></a>XSD 架构的批注  
 您可以对 XSD 架构使用批注来描述数据库映射、查询数据库并返回 XML 文档形式的结果。 使用批注可将 XSD 架构映射到数据库表和列。 可以对 XSD 架构创建的 XML 视图指定 XPath 查询来查询数据库并获取 XML 形式的结果。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 架构语言支持随 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 中带批注的 XML-Data Reduced (XDR) 架构语言引入的批注。 SQLXML 4.0 中不推荐使用带批注的 XDR。  
  
 在关系数据库上下文中，将任意 XSD 架构映射到关系存储区很有用。 实现这种映射的一种方法是对 XSD 架构进行批注。 带批注的 XSD 架构称为*映射架构*，其中提供了有关如何将 XML 数据映射到关系存储区的信息。 实际上，映射架构是关系数据的 XML 视图。 使用这些映射能够以 XML 文档形式检索关系数据。  
  
## <a name="namespace-for-annotations"></a>批注的命名空间  
 在 XSD 架构中，使用命名空间指定批注**urn： 架构-microsoft-com:mapping-架构**。 下面的示例中所示，指定的命名空间的最简单方法是指定它在 **\<xsd: schema >** 标记。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 命名空间可采用任意前缀。 在本文档中， **sql**前缀用于表示批注命名空间，并且以区分此命名空间中的批注与其他命名空间中。  
  
## <a name="example-of-an-annotated-xsd-schema"></a>带批注的 XSD 架构的示例  
 在以下示例中，XSD 架构包含的 **\<Person.Contact >** 元素。 **\<员工 >** 元素具有**ContactID**属性和 **\<FirstName >** 并 **\<姓氏 >** 子元素：  
  
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
  
 在映射架构中， **\<联系人 >** 通过将元素映射到 AdventureWorks 示例数据库中的 Person.Contact 表**sql: relation**批注。 将属性 ConID、 FName 和 LName 映射到 Person.Contact 表中的 ContactID、 FirstName 和 LastName 列使用**sql: field**批注。  
  
 此带有批注的 XSD 架构提供了关系数据的 XML 视图。 可使用 XPath 语言查询此 XML 视图。 XPath 查询返回的结果是一个 XML 文档，而 SQL 查询返回的结果是行集。  
  
> [!NOTE]  
>  在映射架构中，指定关系值（如表名和列名）是否区分大小写取决于 SQL Server 是否使用区分大小写的排序规则设置。 有关详细信息，请参阅 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="other-resources"></a>其他资源  
 有关 XML 架构定义语言 (XSD)、XML Path 语言 (XPath) 和可扩展样式表语言转换 (XSLT) 的详细信息，请访问以下网站：  
  
-   XML 架构第 0 部分：入门，W3C 建议 (http://www.w3.org/TR/xmlschema-0/)  
  
-   XML 架构第 1 部分：结构、 W3C 建议 (http://www.w3.org/TR/xmlschema-1/)  
  
-   XML 架构第 2: datatypes，W3C 建议 (http://www.w3.org/TR/xmlschema-2/)  
  
-   XML 路径语言 (XPath) (http://www.w3.org/TR/xpath)  
  
-   XSL 转换 (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>请参阅  
 [带批注的架构的安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [带批注的 XDR 架构&#40;不推荐在 SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
