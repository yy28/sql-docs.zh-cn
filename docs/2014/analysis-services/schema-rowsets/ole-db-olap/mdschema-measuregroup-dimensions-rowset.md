---
title: MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f607b966099f71acee460a5a343c557e2a81857e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018034"
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集
  枚举度量值组的维度。  
  
## <a name="rowset-columns"></a>行集列  
 `MDSCHEMA_MEASUREGROUP_DIMENSIONS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此度量值组所属的目录的名称。 如果提供程序不支持目录，则为 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不提供支持。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此度量值组所属的多维数据集的名称。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||度量值组的名称。|  
|`MEASUREGROUP_CARDINALITY`|`DBTYPE_WSTR`||度量值组中的度量值可以具有的一个维度成员的实例数。 可能的值包括：<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||维度的唯一名称。|  
|`DIMENSION_CARDINALITY`|`DBTYPE_WSTR`||维度成员可以具有的度量值组度量值的实例数。<br /><br /> 可能的值包括：<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||指示维度中的层次结构是否可见的布尔值。<br /><br /> 如果维度中的一个或多个层次结构可见，则返回 `TRUE`，否则返回 `FALSE`。|  
|`DIMENSION_IS_FACT_DIMENSION`|`DBTYPE_BOOL`||指示维度是否为事实维度的布尔值。<br /><br /> 如果维度为事实维度，则返回 `TRUE`，否则返回 `FALSE`。|  
|`DIMENSION_PATH`|`DBTYPE_HCHAPTER`||引用维度的维度列表。|  
|`DIMENSION_GRANULARITY`|`DBTYPE_WSTR`||粒度层次结构的唯一名称。|  
  
 行集支持按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`MEASUREGROUP_NAME`、`DIMENSION_UNIQUE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `MDSCHEMA_MEASUREGROUP_DIMENSIONS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|可选。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|可选。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|可选。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|可选。|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|（可选）位图，并使用以下有效的值之一：<br /><br /> -1 的可见性<br />-2 不可见<br />默认限制是值为 1。|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB for OLAP 架构行集](ole-db-for-olap-schema-rowsets.md)  
  
  