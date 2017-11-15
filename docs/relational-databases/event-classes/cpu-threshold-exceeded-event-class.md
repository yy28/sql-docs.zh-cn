---
title: "CPU Threshold Exceeded 事件类 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7944d918b0aff15106e89551e3a0272691097083
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="cpu-threshold-exceeded-event-class"></a>CPU Threshold Exceeded 事件类
  CPU Threshold Exceeded 事件类指示资源调控器检测到超出为 REQUEST_MAX_CPU_TIME_SEC 指定的 CPU 阈值的查询。  
  
> [!NOTE]  
>  此事件的检测时间间隔为五秒。 这就保证如果查询超出指定的限制至少五秒，将生成事件。 然而，如果查询超出指定的阈值少于五秒，则其检测可能会丢失，具体取决于查询计时和上次检测清扫的时间。  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>CPU Threshold Exceeded 数据列  
  
|数据列名称|数据类型|说明|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|CPU 使用率，以毫秒为单位。|18|是|  
|EventClass|**int**|214|27|是|  
|EventSubClass|**int**|CPU 限制冲突。|21|是|  
|GroupID|**int**|发生冲突的组 ID。|66|是|  
|OwnerID|**int**|导致冲突的进程的 SPID。|58|是|  
|SPID|**int**|激发此事件的服务器进程的 ID。<br /><br /> 注意：如果系统线程将验证 CPU 使用率作为后台任务，则此 ID 可能与实际用户的 SPID 不同。|12|是|  
|StartTime|**datetime**|此事件的激发时间。|14|是|  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
