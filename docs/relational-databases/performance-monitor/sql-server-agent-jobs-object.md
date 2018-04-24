---
title: SQL Server 代理 - Jobs 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ada7be71515d2b5df0a8af7762289f24aec4249
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server 代理中的 Jobs 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 代理的 **Jobs** 性能对象包含的性能计数器可报告有关 SQL Server 代理作业的信息。 下表列出了此对象包含的计数器。  
  
 下表介绍了 **SQLAgent:Jobs** 计数器。  
  
|“属性”|Description|  
|----------|-----------------|  
|**Active Jobs**|该计数器报告当前运行的作业数。|  
|**Failed jobs**|该计数器报告失败退出的作业数。|  
|**Job success rate**|该计数器报告所执行的作业中成功完成的百分比。|  
|**Jobs activated/minute**|该计数器报告最后一分钟内启动的作业数。|  
|**Queued jobs**|该计数器报告已准备好供 SQL Server 代理准备运行但尚未开始运行的作业数。|  
|**Successful jobs**|该计数器报告成功退出的作业数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|实例|Description|  
|--------------|-----------------|  
|**_Total**|所有作业的信息。|  
|**警报**|由警报启动的作业的信息。|  
|**其他**|不是由警报或计划启动的作业的信息。 通常这些作业是使用 **sp_start_job**手动启动的作业。|  
|**计划**|由计划启动的作业的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [执行作业](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [使用性能对象](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
