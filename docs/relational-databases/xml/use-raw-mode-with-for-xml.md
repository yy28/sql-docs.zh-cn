---
title: "将 RAW 模式与 FOR XML 一起使用 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bb3ece9018927b767e3ae13e5552346bf2a00c91
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="use-raw-mode-with-for-xml"></a>将 RAW 模式与 FOR XML 一起使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]RAW 模式可将查询结果集中的每一行转换为带有通用标识符 \<row> 或可能提供元素名称的 XML 元素。 默认情况下，非 NULL 行集中的每列值都将映射到 \<row> 元素的一个属性。 如果将 ELEMENTS 指令添加到 FOR XML 子句，则每列值都将映射到 \<row> 元素的子元素。 指定 ELEMENTS 指令之后，您还可以选择性地指定 XSINIL 选项以将结果集中的 NULL 列值映射到具有 xsi:nil=`"`true`"`属性的元素。  
  
 您可以请求返回所产生的 XML 的架构。 指定 XMLDATA 选项将返回内联 XDR 架构。 指定 XMLSCHEMA 选项将返回内联 XSD 架构。 该架构显示在数据的开头。 在结果中，每个顶级元素都引用架构命名空间。  
  
 必须在 FOR XML 子句中指定 BINARY BASE64 选项以使用 base64 编码格式返回二进制数据。 在 RAW 模式下，如果不指定 BINARY BASE64 选项就检索二进制数据，将导致错误。  
  
## <a name="in-this-section"></a>本节内容  
 本部分包含以下示例：  
  
-   [示例：以 XML 形式检索产品型号信息](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [示例：指定带有 ELEMENTS 指令的 XSINIL](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [示例：使用 XMLDATA 和 XMLSCHEMA 选项作为结果请求架构](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [示例：检索二进制数据](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [示例：重命名 <row> 元素](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [示例：为 FOR XML 生成的 XML 指定根元素](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [示例：查询 XML 类型的列](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [将 AUTO 模式与 FOR XML 一起使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [将 EXPLICIT 模式与 FOR XML 一起使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [将 PATH 模式与 FOR XML 一起使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
