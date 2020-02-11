---
title: 将 RAW 模式与 FOR XML 一起使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aec0ec20c9bd46a06560f5ce6ebd374e937f0343
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63193247"
---
# <a name="use-raw-mode-with-for-xml"></a>将 RAW 模式与 FOR XML 一起使用
  RAW 模式可将查询结果集中的每一行转换为带有通用标识符 \<row> 或可能提供元素名称的 XML 元素。 默认情况下，非 NULL 行集中的每列值都将映射到 \<row> 元素的一个属性。 如果将 ELEMENTS 指令添加到 FOR XML 子句，则每列值都将映射到 \<row> 元素的子元素。 指定 ELEMENTS 指令之后，您还可以选择性地指定 XSINIL 选项以将结果集中的 NULL 列值映射到具有 xsi:nil=`"`true`"` 属性的元素。  
  
 您可以请求返回所产生的 XML 的架构。 指定 XMLDATA 选项将返回内联 XDR 架构。 指定 XMLSCHEMA 选项将返回内联 XSD 架构。 该架构显示在数据的开头。 在结果中，每个顶级元素都引用架构命名空间。  
  
 必须在 FOR XML 子句中指定 BINARY BASE64 选项以使用 base64 编码格式返回二进制数据。 在 RAW 模式下，如果不指定 BINARY BASE64 选项就检索二进制数据，将导致错误。  
  
## <a name="in-this-section"></a>本节内容  
 本部分包含以下示例：  
  
-   [示例：以 XML 形式检索产品型号信息](example-retrieving-product-model-information-as-xml.md)  
  
-   [示例：指定带有 ELEMENTS 指令的 XSINIL](example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [示例：使用 XMLDATA 和 XMLSCHEMA 选项作为结果请求架构](example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [示例：检索二进制数据](example-retrieving-binary-data.md)  
  
-   [示例：重命名 <row> 元素](example-renaming-the-row-element.md)  
  
-   [示例：为 FOR XML 生成的 XML 指定根元素](example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [示例：查询 XMLType 列](example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [将 AUTO 模式与 FOR XML 一起使用](use-auto-mode-with-for-xml.md)   
 [将 EXPLICIT 模式与 FOR XML 一起使用](use-explicit-mode-with-for-xml.md)   
 [将 PATH 模式与 FOR XML 一起使用](use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML (SQL Server)](../xml/for-xml-sql-server.md)  
  
  
