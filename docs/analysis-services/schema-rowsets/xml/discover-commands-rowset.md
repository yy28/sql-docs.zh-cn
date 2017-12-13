---
title: "DISCOVER_COMMANDS 行集 |Microsoft 文档"
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
helpviewer_keywords: DISCOVER_COMMANDS rowset
ms.assetid: d228f265-05d9-4d2c-a622-44c73eab7a71
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 973ab21d67c0d9c58a4733e84821024fe7558348
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="discovercommands-rowset"></a>DISCOVER_COMMANDS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]在服务器上提供有关中打开的连接的当前正在执行或最后一个的执行命令的资源使用情况和活动信息。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_COMMANDS**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**SESSION_SPID**|**DBTYPE_I4**|是|会话 ID。|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||自会话开始后已执行的命令数。|  
|**COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||上次命令开始的日期和时间，以服务器上的 UTC 时间表示。|  
|**COMMAND_ELAPSED_TIME_MS**|**是 DBTYPE_I8**||自命令开始起经过的时间（毫秒）。|  
|**COMMAND_CPU_TIME_MS**|**是 DBTYPE_I8**||自命令执行开始后该命令占用的 CPU 时间（毫秒）。|  
|**COMMAND_READS**|**是 DBTYPE_I8**||自命令开始后的累计磁盘读取次数。|  
|**COMMAND_READ_KB**|**是 DBTYPE_I8**||自命令开始后从磁盘读取的数据的累计值 (KB)。|  
|**COMMAND_WRITES**|**是 DBTYPE_I8**||自命令开始后的累计磁盘写入次数。|  
|**COMMAND_WRITE_KB**|**是 DBTYPE_I8**||自命令开始后写入磁盘的数据的累计值 (KB)。|  
|**COMMAND_TEXT**|**DBTYPE_WSTR**||命令文本。|  
|**COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||命令执行结束时的服务器 UTC 日期和时间。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd34-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|命令|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
