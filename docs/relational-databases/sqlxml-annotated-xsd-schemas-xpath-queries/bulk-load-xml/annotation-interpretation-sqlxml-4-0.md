---
title: 批注解释 (SQLXML 4.0) |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68d956bb6c35adbf7df32becf539f0965f904955
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43089542"
---
# <a name="annotation-interpretation-sqlxml-40"></a>批注解释 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本节中的主题介绍 XML 大容量加载如何解释 XSD 架构中的批注。 这里描述的行为也适用于 XDR 架构中的批注。  
  
> [!NOTE]  
>  这些主题中的信息仅说明了 XML 大容量加载在其处理过程中使用的批注。 批注的 XSD 架构支持的 SQLXML 4.0 的完整列表，请参阅[XSD 架构中使用批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。 有关受支持的 XDR 架构批注的列表，请参阅[带批注的 XDR 架构&#40;在 SQLXML 4.0 中不推荐使用&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [sql: relationship 和键排序规则&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 介绍如何**sql: relationship**批注解释在 XML 大容量加载。  
  
 [sql： 映射&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 介绍如何**sql： 映射**批注解释在 XML 大容量加载。  
  
 [sql:-字段和 sql： 的值&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 介绍如何**sql:-字段**并**sql:-值**批注解释在 XML 大容量加载。  
  
 [sql:overflow-字段&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 介绍如何**sql:overflow**批注解释在 XML 大容量加载。  
  
 [其他批注&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 介绍 XML 大容量加载中如何解释以下批注： **sql:id-前缀**， **sql: use-cdata**， **sql:url-编码**， **sql:为映射架构**， **sql:key-字段**。  
  
  
