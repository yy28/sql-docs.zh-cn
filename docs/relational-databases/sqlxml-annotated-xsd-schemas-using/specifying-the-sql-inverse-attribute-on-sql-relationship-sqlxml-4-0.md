---
title: 'Relationship (SQLXML 4.0) 上指定 sql: inverse 属性 |Microsoft Docs'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0141818b93db939f90f89faee7c396dfadb05853
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066923"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>在 sql:relationship 上指定 sql:inverse 属性 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Sql: inverse**特性仅在 XSD 架构用于大容量加载或用于 updategram 会非常有用。 **Sql: inverse**上，可以指定特性 **\<sql: relationship >** 元素。 在 updategram 中，updategram 逻辑在确定由 updategram 操作更新的表和列时会解释架构。 架构中所指定的父子关系决定了修改（插入或删除）记录的顺序。  
  
 如果在 XSD 架构中指定的父子关系与相应数据库列之间的主键/外键关系顺序相反，则插入或删除 updategram 操作将因主键/外键冲突而失败。 在这种情况下， **sql: inverse**指定属性 (**sql: inverse ="true"** ) 中 **\<sql: relationship >** 元素和 updategram 逻辑逆方法在架构中指定其父-子关系的解释。  
  
 **Sql: inverse**属性采用布尔值 (0 = false,1 = true)。 可接受的值为 0、1、true 和 false。  
  
 有关工作示例使用**sql: inverse**批注，请参阅[在 Updategram 中指定带批注的映射架构](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>请参阅  
 [关系使用 sql: relationship 指定&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
