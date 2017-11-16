---
title: "MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81a5287d38def196a54e6053dd80af6190b34b4a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasuregroupdimensions-rowset"></a>MDSCHEMA_MEASUREGROUP_DIMENSIONS 行集
  枚举度量值组的维度。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此度量值组所属的目录的名称。 **NULL**如果提供程序不支持目录。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此度量值组所属的多维数据集的名称。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||度量值组的名称。|  
|**MEASUREGROUP_CARDINALITY**|**DBTYPE_WSTR**||度量值组中的度量值可以具有的一个维度成员的实例数。 可能的值包括：<br /><br /> **其中一个**<br /><br /> **许多**|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||维度的唯一名称。|  
|**DIMENSION_CARDINALITY**|**DBTYPE_WSTR**||维度成员可以具有的度量值组度量值的实例数。 可能的值包括：<br /><br /> **其中一个**<br /><br /> **许多**|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**||指示维度中的层次结构是否可见的布尔值。<br /><br /> 返回**TRUE**维度中的一个或多个层次结构是否可见; 否则为**FALSE**。|  
|**DIMENSION_IS_FACT_DIMENSION**|**DBTYPE_BOOL**||指示维度是否为事实维度的布尔值。<br /><br /> 返回**TRUE**如果维度是事实维度; 否则为**FALSE**。|  
|**DIMENSION_PATH**|**DBTYPE_HCHAPTER**||引用维度的维度列表。|  
|**DIMENSION_GRANULARITY**|**DBTYPE_WSTR**||粒度层次结构的唯一名称。|  
  
 行集支持排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **MEASUREGROUP_NAME**， **DIMENSION_UNIQUE_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|可选。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|可选。|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|（可选）位图，并使用以下有效的值之一：<br /><br /> 1 可见<br /><br /> 2 不可见<br /><br /> 默认限制的值为 1。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

