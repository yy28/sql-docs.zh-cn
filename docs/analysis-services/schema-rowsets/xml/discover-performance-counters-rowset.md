---
title: "DISCOVER_PERFORMANCE_COUNTERS 行集 |Microsoft 文档"
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
ms.assetid: 62b1e967-af67-4915-a305-727bffd61fe4
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 66f501e406ff428ee6c901e122b3ec222124a345
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discoverperformancecounters-rowset"></a>DISCOVER_PERFORMANCE_COUNTERS 行集
  返回一个或多个性能计数器的值。 不支持返回有关一段时间内的使用情况的信息（如每秒的磁盘读取数和 CPU 使用率的百分比）的计数器。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_PERFORMANCE_COUNTERS**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**PERF_COUNTER_NAME**|**DBTYPE_WSTR**|必需|性能计数器的名称。|  
|**PERF_COUNTER_VALUE**|**DBTYPE_DOUBLE**||性能计数器的值。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd2e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PerformanceCounters|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
