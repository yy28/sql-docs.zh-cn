---
title: XSD 架构 (SQLXML 4.0) 中使用批注 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 26fd2f853697765fda82b869aae7780976753749
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321947"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>在 XSD 架构中使用批注 (SQLXML 4.0)
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 架构语言对批注的支持方式与在 XML 数据简化 (XDR) 架构语言中引入的批注支持方式相似。 XSD 中还引入了 XDR 不支持的其他批注。  
  
 这些批注可在 XSD 架构中用于指定 XML 到关系映射。 这包括 XSD 架构中的元素和属性到数据库中表（视图）和列之间的映射。  
  
 如果未指定批注，则进行默认映射。 默认情况下，复杂类型的 XSD 元素映射为指定数据库中的表（视图）名称，而简单类型的元素或属性映射为与该元素或属性同名的列。  
  
 由于 XSD 架构只是关系数据的 XML 视图，这些批注也可用于指定 XML 中的层次结构关系，从而表示数据库中的关系。  
  
 此部分提供了可用于 XSD 架构的批注的描述及其用法的示例。  
  
> [!NOTE]  
>  此部分中的所有示例针对每个示例中描述的带有批注的 XSD 架构指定了简单的 XPath 查询。 本部分假定您熟悉 XPath 语言。  
  
## <a name="in-this-section"></a>本节内容  
 [XSD 批注&#40;SQLXML 4.0&#41;](xsd-annotations-sqlxml-4-0.md)  
 列出了可用于 XSD 架构的批注、相关描述及等效的 XDR 批注。  
  
 [XSD 元素和属性到表和列的默认映射&#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 说明默认映射，并提供与默认映射相关的任务示例。  
  
 [XSD 元素和属性到表和列的显式映射&#40;SQLXML 4.0&#41;](explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 说明带有 `sql:relation` 和 `sql:field` 批注的显式映射，并提供示例。  
  
 [关系使用 sql: relationship 指定&#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 介绍并提供 `sql:relationship` 批注的示例。  
  
 [Sql: relationship 上指定 sql: inverse 属性&#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 介绍 `sql:inverse` 批注。  
  
 [创建常量元素使用 sql： 是常量&#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 介绍并提供 `sql:is-constant` 批注的示例。  
  
 [从生成 XML 文档中使用 sql 中排除架构元素： 映射&#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 介绍并提供 `sql:mapped` 批注的示例。  
  
 [筛选值使用 sql:-字段和 sql： 的值&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 介绍并提供 `sql:limit-field` 和 `sql:limit-value` 批注的示例。  
  
 [标识键列使用 sql:key-字段&#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 介绍并提供 `sql:key-fields` 批注的示例。  
  
 [使用指定目标 Namespace targetNamespace 属性&#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 介绍并提供的示例**targetNamespace**属性。  
  
 [有效的 ID、 IDREF 和 IDREFS 类型属性使用 sql: prefix 创建&#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 介绍并提供 `sql:prefix` 批注的示例。  
  
 [数据类型强制转换和 sql: datatype 批注&#40;SQLXML 4.0&#41;](data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 介绍并提供 `sql:datatype` 批注的示例。  
  
 [XSD 数据类型映射到 XPath 数据类型&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)  
 提供比较 XSD、XDR 和 XPath 数据类型并列出相关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 转换的表。  
  
 [创建 CDATA 部分使用 sql: use-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 介绍并提供 `sql:use-data` 批注的示例。  
  
 [请求 URL 引用 BLOB 数据使用 sql： 进行编码&#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 介绍并提供 `sql:encode` 批注的示例。  
  
 [检索未用完数据使用 sql:overflow-字段&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 介绍并提供 `sql:overflow-field` 批注的示例。  
  
 [使用 sql:hide 隐藏元素和属性](hiding-elements-and-attributes-by-using-sql-hide.md)  
 介绍并提供 `sql:hide` 批注的示例。  
  
 [使用 sql:identity 和 sql:guid 批注](using-the-sql-identity-and-sql-guid-annotations.md)  
 介绍并提供 `sql:identity` 和 `sql:guid` 批注的示例。  
  
 [使用 sql:max-depth 指定递归关系中的深度](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 介绍并提供 `sql:max-depth` 批注的示例。  
  
## <a name="see-also"></a>请参阅  
 [带批注的架构的安全注意事项&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
