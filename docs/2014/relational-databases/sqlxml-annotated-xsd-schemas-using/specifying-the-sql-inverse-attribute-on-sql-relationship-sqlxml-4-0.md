---
title: 'Relationship (SQLXML 4.0) 上指定 sql: inverse 属性 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf8d5dee0d72800c5b6250d83106cda552004536
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800789"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>在 sql:relationship 上指定 sql:inverse 属性 (SQLXML 4.0)
  `sql:inverse` 属性只有在 XSD 架构用于大容量加载或用于 updategram 时才有用。 `sql:inverse`可以对指定属性 **\<sql: relationship >** 元素。 在 updategram 中，updategram 逻辑在确定由 updategram 操作更新的表和列时会解释架构。 架构中所指定的父子关系决定了修改（插入或删除）记录的顺序。  
  
 如果在 XSD 架构中指定的父子关系与相应数据库列之间的主键/外键关系顺序相反，则插入或删除 updategram 操作将因主键/外键冲突而失败。 在这种情况下，`sql:inverse`指定属性 (`sql:inverse="true"`) 中 **\<sql: relationship >** 元素，并且 updategram 逻辑会反转其指定的父-子关系的解释在架构中。  
  
 `sql:inverse` 属性采用布尔值（0 = FALSE，1 = TRUE）。 可接受的值为 0、1、true 和 false。  
  
 有关工作示例使用`sql:inverse`批注，请参阅[在 Updategram 中指定带批注的映射架构](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>请参阅  
 [关系使用 sql: relationship 指定&#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
