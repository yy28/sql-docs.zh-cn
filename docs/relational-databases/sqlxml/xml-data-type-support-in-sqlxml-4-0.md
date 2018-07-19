---
title: 在 SQLXML 4.0 中的数据类型支持 xml |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 68cb00ced8f77b5921be07a3f6383d4436f0bade
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38003419"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0 中的 xml 数据类型支持
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持 XML 类型化数据使用**xml**数据类型。 本主题提供有关 SQLXML 4.0 如何识别实例的信息**xml**数据类型和实现对它们的支持。  
  
## <a name="working-with-xml-data-types"></a>使用 xml 数据类型  
 若要了解有关如何使用实现的 SQL 表的详细信息**xml**数据类型列，提供了以下示例：  
  
|任务|示例|主题|  
|----------|-------------|-----------|  
|如何映射和包含**xml** XML 视图中的列|“将 XML 元素映射到 XML 数据类型列”|[XSD 元素和属性到表和列的默认映射&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|如何将数据插入**xml**使用 updategram 的列|“将数据插入到 XML 数据类型列”|[使用 XML Updategram 插入数据&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|大容量加载 XML 数据读入**xml**列|“在 xml 数据类型列中执行大容量加载”|[XML 大容量加载示例&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>准则和限制  
  
-   **\<xsd： 任何 >** 不能映射到列包括**xml**数据类型。 通过提供这种情况下在 SQLXML 中支持**sql:overflow-字段**批注。 另一个解决方法是映射**xml**为元素的数据类型字段**格式 xsd: anytype**。 上表中引用的“将 XML 元素映射到 XML 数据类型列”示例介绍了这种解决办法。  
  
-   内容执行 XPath 查询**xml**不支持数据类型列。  
  
-   使用**xml**不支持的批注中的数据类型列 (如**sql: relationship**并**sql:key-字段**) 或允许的将导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实现 SQLXML 4.0 的中间层组件将不会捕获的错误。 其原因在于 SQLXML 不要求 SQL 类型信息。 这类似于其他数据类型（如 BLOB 和二进制类型）的 SQLXML 的行为。  
  
-   映射**xml**仅对 XSD 架构支持的列。 XDR 架构不支持映射**xml**列。  
  
-   SQLXML 4.0 依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 XML 分析支持。 **Xml**列可以映射为类型化的 XML 或非类型化的 XML。 在任一种情况下，SQLXML 4.0 都不验证输入 XML。  如果输入 XML 无效或格式不正确，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将向 SQLXML 报告此情况，并将服务器返回的任何相关的错误信息传播给用户。  
  
-   SQLXML 4.0 依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的对于 DTD 的有限支持。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许在而内部 dtd **xml**数据类型的数据，可以使用来提供默认值和实体引用替换为其扩展的内容。 SQLXML 将 XML 数据“按原样”（包括内部 DTD）传递到服务器。 可以通过使用第三方工具将 DTD 转换为 XML 架构 (XSD)，然后使用内联 XSD 架构将数据加载到数据库中。  
  
-   SQLXML 4.0 不会保留 XML 声明处理指令 （例如） 根据的行为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 相反，XML 声明视为到指令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 分析器 （版本、 编码和独立版） 及其属性后，将和丢失数据转换为**xml**数据类型。 XML 数据在内部存储为 UCS-2。 将保留 XML 实例中的所有其他处理指令;在中允许他们**xml**列和 SQLXML 支持。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据 (SQL Server)](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
