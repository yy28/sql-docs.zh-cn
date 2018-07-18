---
title: 批注解释 (SQLXML 4.0) |Microsoft 文档
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
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 67d586555fa81a456c87cc94379740e71c982696
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32969902"
---
# <a name="annotation-interpretation-sqlxml-40"></a>批注解释 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本节中的主题介绍 XML 大容量加载如何解释 XSD 架构中的批注。 这里描述的行为也适用于 XDR 架构中的批注。  
  
> [!NOTE]  
>  这些主题中的信息仅说明了 XML 大容量加载在其处理过程中使用的批注。 SQLXML 4.0 支持的 XSD 架构的批注的完整列表，请参阅[XSD 架构中使用批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。 对于 XDR 架构支持批注的列表，请参阅[批注 XDR 架构&#40;SQLXML 4.0 中弃用&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [sql:relationship 和键排序规则&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 描述如何**sql:relationship**批注解释在 XML 大容量加载。  
  
 [sql： 映射&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 描述如何**sql： 映射**批注解释在 XML 大容量加载。  
  
 [sql:limit-字段和 sql:limit-值&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述如何**sql:limit-字段**和**sql:limit-值**批注解释在 XML 大容量加载。  
  
 [sql:overflow-字段&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 描述如何**sql:overflow**批注解释在 XML 大容量加载。  
  
 [其他批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 描述如何在 XML 大容量加载解释的以下批注： **sql:id-前缀**， **sql:use-cdata**， **sql:url-编码**， **sql:是映射架构**， **sql:key-字段**。  
  
  
