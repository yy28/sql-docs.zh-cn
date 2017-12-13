---
title: "DISCOVER_PARTITION_DIMENSION_STAT 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fe9721a2653f962865b6d5b180bff99d4043b306
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]返回与分区相关联的维度上的统计信息  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_PARTITION_DIMENSION_STAT**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|必需|数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|必需|多维数据集或表格模型的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|必需|度量值组的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|必需|分区的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||维度的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||维度中的属性的名称。|  
|**ATTRIBUTE_INDEXED**|**DBTYPE_BOOL**||如果为 true，则表示对该属性创建索引；否则为 false。|  
|**ATTRIBUTE_COUNT_MIN**|**是 DBTYPE_I8**||最小属性计数。|  
|**ATTRIBUTE_COUNT_MAX**|**是 DBTYPE_I8**||最大属性计数。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
