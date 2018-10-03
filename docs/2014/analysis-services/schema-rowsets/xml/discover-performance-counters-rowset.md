---
title: DISCOVER_PERFORMANCE_COUNTERS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 62b1e967-af67-4915-a305-727bffd61fe4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3f4f27d074ff01f02cc05c165e8acb1ea109198
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129237"
---
# <a name="discoverperformancecounters-rowset"></a>DISCOVER_PERFORMANCE_COUNTERS 行集
  返回一个或多个性能计数器的值。 不支持返回有关一段时间内的使用情况的信息（如每秒的磁盘读取数和 CPU 使用率的百分比）的计数器。  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_PERFORMANCE_COUNTERS`行集包含以下列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`PERF_COUNTER_NAME`|`DBTYPE_WSTR`|Required|性能计数器的名称。|  
|`PERF_COUNTER_VALUE`|`DBTYPE_DOUBLE`||性能计数器的值。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd2e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PerformanceCounters|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
