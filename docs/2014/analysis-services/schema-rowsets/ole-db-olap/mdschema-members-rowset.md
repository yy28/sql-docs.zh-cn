---
title: MDSCHEMA_MEMBERS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_MEMBERS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2473797ef34c0fd204c878da8c6044a307cc1ee3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129785"
---
# <a name="mdschemamembers-rowset"></a>MDSCHEMA_MEMBERS 行集
  介绍数据库中的成员。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_MEMBERS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此成员所属的数据库的名称。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||此成员所属的架构的名称。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此成员所属的多维数据集的名称。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||此成员所属的维度的唯一名称。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||此成员所属的层次结构的唯一名称。|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||此成员所属的级别的唯一名称。|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||成员距层次结构的根的距离。 根级别为零 (0)。|  
|`MEMBER_ORDINAL`|`DBTYPE_UI4`||（不推荐使用）始终返回 `0`。|  
|`MEMBER_NAME`|`DBTYPE_WSTR`||成员的名称。|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||成员的唯一名称。|  
|`MEMBER_TYPE`|`DBTYPE_I4`||成员的类型：<br /><br /> -   `MDMEMBER_TYPE_REGULAR` (`1`)<br />-   `MDMEMBER_TYPE_ALL` (`2`)<br />-   `MDMEMBER_TYPE_MEASURE` (`3`)<br />-   `MDMEMBER_TYPE_FORMULA` (`4`)<br />-   `MDMEMBER_TYPE_UNKNOWN` (`0`)<br />-   `MDMEMBER_TYPE_FORMULA` 将优先于`MDMEMBER_TYPE_MEASURE`。 例如，如果度量值维度上有一个公式（计算）成员，则作为 `MDMEMBER_TYPE_FORMULA` 列出。|  
|`MEMBER_GUID`|`DBTYPE_GUID`||成员的 GUID。 如果 GUID 不存在，则为 `NULL`。|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`||与成员相关的标签或标题。 主要用于显示目的。 如果标题不存在，`MEMBER_NAME`返回。|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||成员具有的子级的个数。 它可以是一个估计值，所以使用者不应依赖它作为确切计数。 访问接口应尽可能返回最精确的估计值。|  
|`PARENT_LEVEL`|`DBTYPE_UI4`||成员的父级距层次结构的根级别的距离。 根级别为零 (0)。|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||成员的父成员的唯一名称。 对于根级别上的任何成员，均返回 `NULL`。|  
|`PARENT_COUNT`|`DBTYPE_UI4`||此成员具有的父级的个数。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||此列始终返回 `NULL` 值。<br /><br /> 存在此列是为了向后兼容。|  
|`EXPRESSION`|`DBTYPE_WSTR`||当成员类型为 `MDMEMBER_TYPE_FORMULA` 时，用于计算的表达式。|  
|`MEMBER_KEY`|`DBTYPE_WSTR`||成员的键列的值。 如果成员具有组合键，则返回 `NULL`。|  
|`IS_PLACEHOLDERMEMBER`|`DBTYPE_BOOL`||一个指示成员是否为维度层次结构中空位置的占位符成员的布尔值。<br /><br /> 仅当 `MDX Compatibility` 属性设置为 2 时，此值才有效。|  
|`IS_DATAMEMBER`|`DBTYPE_BOOL`||一个指示成员是否为数据成员的布尔值。<br /><br /> 如果成员是数据成员，则返回 True。|  
|`SCOPE`|`DBTYPE_I4`||成员的作用域。 成员可以是会话计算成员，也可以是全局计算成员。 对于非计算成员，此列返回 `NULL`。<br /><br /> 此列可以为下列值之一：<br /><br /> -MDMEMBER_SCOPE_GLOBAL = 1<br />-MDMEMBER_SCOPE_SESSION = 2|  
|`Zero or more additional columns`|`DBTYPE_UI2`||如果成员可从多个级别返回，则不会返回属性。 例如，如果树运算符为 `PARENT`，而对于非父子层次结构为 `SELF`，则不会返回成员属性。<br /><br /> 这适用于树运算符能够从不同级别返回成员的不规则层次结构（例如，如果上一个级别包含漏洞，并且请求了成员的父级）。|  
  
 行集按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`DIMENSION_UNIQUE_NAME`、`HIERARCHY_UNIQUE_NAME`、`LEVEL_UNIQUE_NAME`、`LEVEL_NUMBER`、`MEMBER_ORDINAL` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_MEMBERS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`|可选。|  
|`MEMBER_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`|可选。|  
|`MEMBER_TYPE`|`DBTYPE_I4`|可选。|  
|`TREE_OP`|`DBTYPE_I4`|（可选）仅适用于单个成员：<br /><br /> -   `MDTREEOP_ANCESTORS` (`0x20`) 返回所有上级。<br />-   `MDTREEOP_CHILDREN` (`0x01`) 返回仅的直属子级。<br />-   `MDTREEOP_SIBLINGS` (`0x02`) 返回相同的级别上的成员。<br />-   `MDTREEOP_PARENT` (`0x04`) 返回仅的直接父。<br />-   `MDTREEOP_SELF` (`0x08`) 在列表中返回的行返回它自身。<br />-   `MDTREEOP_DESCENDANTS` (`0x10`) 返回所有子代。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|（可选）位图，并使用以下有效的值之一：<br /><br /> -1 的多维数据集<br />-2 的维度<br /><br /> 默认限制的值为 1。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  