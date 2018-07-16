---
title: DISCOVER_PARTITION_DIMENSION_STAT 行集 |Microsoft Docs
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
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f4dc209f985cafe804f81fa54fa68c56655d3e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310737"
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT 行集
  返回与分区关联的维度的统计信息  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_PARTITION_DIMENSION_STAT`行集包含以下列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Required|数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Required|多维数据集或表格模型的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Required|度量值组的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Required|分区的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||维度的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||维度中的属性的名称。|  
|`ATTRIBUTE_INDEXED`|`DBTYPE_BOOL`||如果为 true，则表示对该属性创建索引；否则为 false。|  
|`ATTRIBUTE_COUNT_MIN`|`DBTYPE_I8`||最小属性计数。|  
|`ATTRIBUTE_COUNT_MAX`|`DBTYPE_I8`||最大属性计数。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
