---
title: 在 SQLXML 4.0 中的数据类型支持 xml |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: edf15eb12a2ca994ab178f58e9bcdfd1ccf20075
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157347"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>SQLXML 4.0 中的 xml 数据类型支持
  开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持 XML 类型化数据使用`xml`数据类型。 本主题提供的信息介绍 SQLXML 4.0 如何识别 `xml` 数据类型的实例和如何为它们实现支持。  
  
## <a name="working-with-xml-data-types"></a>使用 xml 数据类型  
 为了解有关如何使用实现 `xml` 数据类型列的 SQL 表的更多信息，提供了以下示例：  
  
|任务|示例|主题|  
|----------|-------------|-----------|  
|如何在 XML 视图中映射和包含 `xml` 列|“将 XML 元素映射到 XML 数据类型列”|[XSD 元素和属性到表和列的默认映射&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|如何使用 updategram 将数据插入到 `xml` 列中|“将数据插入到 XML 数据类型列”|[使用 XML Updategram 插入数据&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|将 XML 数据大容量加载到 `xml` 列中|“在 xml 数据类型列中执行大容量加载”|[XML 大容量加载示例&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>准则和限制  
  
-   **\<xsd： 任何 >** 不能映射到列包括`xml`数据类型。 SQLXML 中对于此应用场景的支持是通过 `sql:overflow-field` 批注提供的。 另一种解决办法是将 `xml` 数据类型字段映射为类型为 `xsd:anyType` 的元素。 上表中引用的“将 XML 元素映射到 XML 数据类型列”示例介绍了这种解决办法。  
  
-   不支持对于 `xml` 数据类型列的内容执行 XPath 查询。  
  
-   在不支持或不允许 `xml` 数据类型列的批注（例如，`sql:relationship` 和 `sql:key-fields`）中使用此数据类型列将导致出现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误，实现 SQLXML 4.0 的中间层组件将不会捕获这些错误。 其原因在于 SQLXML 不要求 SQL 类型信息。 这类似于其他数据类型（如 BLOB 和二进制类型）的 SQLXML 的行为。  
  
-   仅对 XSD 架构支持映射 `xml` 列。 XDR 架构不支持映射 `xml` 列。  
  
-   SQLXML 4.0 依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 XML 分析支持。 `xml` 列可以映射为类型化的 XML 或非类型化的 XML。 在任一种情况下，SQLXML 4.0 都不验证输入 XML。  如果输入 XML 无效或格式不正确，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将向 SQLXML 报告此情况，并将服务器返回的任何相关的错误信息传播给用户。  
  
-   SQLXML 4.0 依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的对于 DTD 的有限支持。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许在 `xml` 数据类型的数据中使用内部 DTD，而内部 DTD 可用来提供默认值和将实体引用替换为其扩展的内容。 SQLXML 将 XML 数据“按原样”（包括内部 DTD）传递到服务器。 可以通过使用第三方工具将 DTD 转换为 XML 架构 (XSD)，然后使用内联 XSD 架构将数据加载到数据库中。  
  
-   SQLXML 4.0 不会保留 XML 声明处理指令 （例如） 根据的行为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 而是将 XML 声明视为针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 分析器的指令，并且，在将数据转换到 `xml` 数据类型之后，此声明的属性（version、encoding 和 standalone）将丢失。 XML 数据在内部存储为 UCS-2。 将保留 XML 实例中的所有其他处理指令；在 `xml` 列中允许使用这些指令，并且 SQLXML 支持它们。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据 (SQL Server)](../xml/xml-data-sql-server.md)  
  
  
