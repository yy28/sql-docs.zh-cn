---
title: "DISCOVER_JOBS 行集 |Microsoft 文档"
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
helpviewer_keywords:
- DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7dc22595beb3870d58aea4e0b98cdb51af92327b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS 行集
  提供有关在服务器上执行的活动作业的信息。 作业是命令的一部分，代表命令执行特定任务。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_JOBS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||创建作业时的服务器 UTC 日期和时间。|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||服务器服务指定的作业说明。|  
|**JOB_EXECUTION_TIME_MS**|**是 DBTYPE_I8**||作业处于活动状态的时间（毫秒）。|  
|**JOB_ID**|**DBTYPE_I4**||作业的唯一标识符。|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||作业开始时的服务器 UTC 日期和时间。|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||从中启动当前作业的线程池。|  
|**JOB_TOTAL_TIME_MS**|**是 DBTYPE_I8**||自作业开始起的时间（毫秒）。|  
|**SPID**|**DBTYPE_I4**||会话 ID。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_JOBS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|可选。|  
|JOB_ID|DBTYPE_I4|可选。|  
|JOB_DESCRIPTION|DBTYPE_WSTR|可选。|  
|JOB_THREADPOOL_ID|DBTYPE_I4|可选。|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
