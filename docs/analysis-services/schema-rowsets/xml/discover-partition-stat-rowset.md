---
title: "DISCOVER_PARTITION_STAT 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0863c2f263cc13ff9673063ab1f49535cd2407a3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 行集
  返回特定分区中的聚合的统计信息。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_PARTITION_STAT**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|必需|包含维度的数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|必需|包含分区的多维数据集或表格模型的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|必需|维度中的度量值组的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|必需|分区的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||聚合的名称。|  
|**AGGREGATION_SIZE**|**是 DBTYPE_I8**||聚合的大小。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

