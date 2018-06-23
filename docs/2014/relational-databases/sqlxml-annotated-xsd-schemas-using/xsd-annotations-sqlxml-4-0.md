---
title: XSD 批注 (SQLXML 4.0) |Microsoft 文档
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
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e7b359f8dfffca6a1b8fbf0f17674275985cf0f0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026960"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 批注 (SQLXML 4.0)
  下表列出在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引入的 XSD 批注，并且将这些批注与已在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中引入的 XDR 批注进行比较。  
  
|XSD 批注|Description|主题链接|XDR 批注|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|在将某一 XML 元素或属性映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 列时，允许请求某一引用 URI。 此 URI 可以在以后使用，以便返回 BLOB 数据。|[请求对 BLOB 数据使用 sql 的 URL 引用： 编码&#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|允许您指定是要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的 GUID 值，还是使用在该列的 updategram 中提供的值。|[使用 sql:identity 和 sql:guid 批注](using-the-sql-identity-and-sql-guid-annotations.md)|不支持|  
|`sql:hide`|隐藏在最终 XML 文档的架构中指定的元素或属性。|[使用 sql:hide 隐藏元素和属性](hiding-elements-and-attributes-by-using-sql-hide.md)|不支持|  
|`sql:identity`|可对映射到 IDENTITY 类型数据库列的任何节点指定。 为此批注指定的值定义如何更新数据库中相应 IDENTITY 类型的列。|[使用 sql:identity 和 sql:guid 批注](using-the-sql-identity-and-sql-guid-annotations.md)|不支持|  
|`sql:inverse`|指示已使用指定的父-子关系其解释的逆属的 updategram 逻辑 **\<sql:relationship >**。|[指定 sql:inverse 属性上 sql:relationship &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|不支持|  
|`sql:is-constant`|创建不映射到任何表的 XML 元素。 该元素出现在查询输出中。|[创建常量元素使用 sql： 是常量&#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|相同|  
|`sql:key-fields`|允许规定唯一标识表中的行的列。|[标识键列使用 sql:key-字段&#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|相同|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|允许限制基于限制值返回的值。|[筛选值使用 sql:limit-字段和 sql:limit-值&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|相同|  
|`sql:mapped`|允许从结果中排除架构项。|[从生成的 XML 文档使用 sql 排除架构元素： 映射&#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|允许您指定在架构中指定的递归关系的深度。|[使用 sql:max-depth 指定递归关系中的深度](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|不支持|  
|`sql:overflow-field`|标识包含溢出数据的数据库列。|[检索未用完数据使用 sql:overflow-字段&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|相同|  
|`sql:prefix`|创建有效的 XML ID、IDREF 和 IDREFS。 将某一字符串置于 ID、IDREF 和 IDREFS 的值之前。|[创建有效的 ID、 IDREF 和 IDREFS 类型属性使用 sql:prefix &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|相同|  
|`sql:relationship`|指定 XML 元素之间的关系。 `parent`、`child`、`parent-key` 和 `child-key` 属性用于建立该关系。|[指定关系使用 sql:relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|属性名称不同：<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|允许指定要用于 XML 文档中的某些元素的 CDATA 部分。|[创建 CDATA 部分使用 sql:use-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|相同|  
  
> [!NOTE]  
>  XSD 本机 `targetNamespace` 属性替换已在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] XDR 映射架构中引入的 `target-namespace` 批注。  
  
## <a name="see-also"></a>请参阅  
 [指定目标 Namespace Using targetNamespace 属性&#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  