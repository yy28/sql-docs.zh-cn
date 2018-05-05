---
title: 在 XSD 架构 (SQLXML 4.0) 中使用批注 |Microsoft 文档
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f3e44d91a958441e421259b7257df49f14883eb0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>在 XSD 架构中使用批注 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 架构语言对批注的支持方式与在 XML 数据简化 (XDR) 架构语言中引入的批注支持方式相似。 XSD 中还引入了 XDR 不支持的其他批注。  
  
 这些批注可在 XSD 架构中用于指定 XML 到关系映射。 这包括 XSD 架构中的元素和属性到数据库中表（视图）和列之间的映射。  
  
 如果未指定批注，则进行默认映射。 默认情况下，复杂类型的 XSD 元素映射为指定数据库中的表（视图）名称，而简单类型的元素或属性映射为与该元素或属性同名的列。  
  
 由于 XSD 架构只是关系数据的 XML 视图，这些批注也可用于指定 XML 中的层次结构关系，从而表示数据库中的关系。  
  
 此部分提供了可用于 XSD 架构的批注的描述及其用法的示例。  
  
> [!NOTE]  
>  此部分中的所有示例针对每个示例中描述的带有批注的 XSD 架构指定了简单的 XPath 查询。 本部分假定您熟悉 XPath 语言。  
  
## <a name="in-this-section"></a>本節內容  
 [XSD 批注&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 列出了可用于 XSD 架构的批注、相关描述及等效的 XDR 批注。  
  
 [XSD 元素和属性表和列的默认映射&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 说明默认映射，并提供与默认映射相关的任务示例。  
  
 [XSD 元素和属性表和列的显式映射&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 说明具有显式映射**sql:relation**和**sql:field**批注，并提供了示例。  
  
 [指定关系使用 sql:relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 描述和提供的示例**sql:relationship**批注。  
  
 [指定 sql:inverse 属性上 sql:relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 描述**sql:inverse**批注。  
  
 [创建常量元素使用 sql： 是常量&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 描述和提供的示例**sql： 是常量**批注。  
  
 [从生成的 XML 文档使用 sql 排除架构元素： 映射&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 描述和提供的示例**sql： 映射**批注。  
  
 [筛选值使用 sql:limit-字段和 sql:limit-值&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 描述和提供的示例**sql:limit-字段**和**sql:limit-值**批注。  
  
 [标识键列使用 sql:key-字段&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 描述和提供的示例**sql:key-字段**批注。  
  
 [指定目标 Namespace Using targetNamespace 属性&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 描述和提供的示例**targetNamespace**属性。  
  
 [创建有效的 ID、 IDREF 和 IDREFS 类型属性使用 sql:prefix &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 描述和提供的示例**sql:prefix**批注。  
  
 [数据类型强制和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 描述和提供的示例**sql: datatype**批注。  
  
 [将 XSD 数据类型映射到 XPath 数据类型&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 提供比较 XSD、XDR 和 XPath 数据类型并列出相关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 转换的表。  
  
 [创建 CDATA 部分使用 sql:use-cdata &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 描述和提供的示例**sql:use-数据**批注。  
  
 [请求对 BLOB 数据使用 sql 的 URL 引用： 编码&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 描述和提供的示例**sql： 编码**批注。  
  
 [检索未用完数据使用 sql:overflow-字段&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 描述和提供的示例**sql:overflow-字段**批注。  
  
 [使用 sql:hide 隐藏元素和属性](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 描述和提供的示例**sql:hide**批注。  
  
 [使用 sql:identity 和 sql:guid 批注](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 描述和提供的示例**sql:identity**和**sql:guid**批注。  
  
 [使用 sql:max-depth 指定递归关系中的深度](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 描述和提供的示例**sql:max-深度**批注。  
  
## <a name="see-also"></a>另请参阅  
 [批注架构安全注意事项&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
