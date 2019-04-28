---
title: DISCOVER_XEVENT_TRACE_DEFINITION 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: e1ce2d2d-f994-4318-801a-ee0385aecd84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 826389eafb4fdf6a32e8d3b62ebfc1f333b62d4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731909"
---
# <a name="discoverxeventtracedefinition-rowset"></a>DISCOVER_XEVENT_TRACE_DEFINITION 行集
  提供有关服务器上当前活动的 XEvent 跟踪的信息。  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_XEVENT_TRACE_DEFINITION` 行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||XEvent 跟踪的 XML 定义。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd1c-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_XEVENT_TRACE_DEFINITION|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/xml-for-analysis-schema-rowsets)   
 [使用 SQL Server 扩展事件&#40;XEvents&#41;若要监视 Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)   
 [使用动态管理视图 (DMV) 监视 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
