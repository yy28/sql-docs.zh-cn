---
title: 批注解释 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2db54a2bec501c3422cf19b1efab7cdb581420e0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013441"
---
# <a name="annotation-interpretation-sqlxml-40"></a>批注解释 (SQLXML 4.0)
  本节中的主题介绍 XML 大容量加载如何解释 XSD 架构中的批注。 这里描述的行为也适用于 XDR 架构中的批注。  
  
> [!NOTE]  
>  这些主题中的信息仅说明了 XML 大容量加载在其处理过程中使用的批注。 批注的 XSD 架构支持的 SQLXML 4.0 的完整列表，请参阅[XSD 架构中使用批注&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。 有关受支持的 XDR 架构批注的列表，请参阅[带批注的 XDR 架构&#40;在 SQLXML 4.0 中不推荐使用&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [sql: relationship 和键排序规则&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 介绍在 XML 大容量加载中如何解释 `sql:relationship` 批注。  
  
 [sql： 映射&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-mapped.md)  
 介绍在 XML 大容量加载中如何解释 `sql:mapped` 批注。  
  
 [sql:-字段和 sql： 的值&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 介绍在 XML 大容量加载中如何解释 `sql:limit-field` 和 `sql:limit-value` 批注。  
  
 [sql:overflow-字段&#40;SQLXML 4.0&#41;](annotation-interpretation-sql-overflow-field.md)  
 介绍在 XML 大容量加载中如何解释 `sql:overflow` 批注。  
  
 [其他批注&#40;SQLXML 4.0&#41;](annotation-interpretation-other-annotations.md)  
 介绍在 XML 大容量加载中如何解释以下批注：`sql:id-prefix`，`sql:use-cdata`，`sql:url-encode`，`sql:is-mapping-schema`，`sql:key-fields`。  
  
  
