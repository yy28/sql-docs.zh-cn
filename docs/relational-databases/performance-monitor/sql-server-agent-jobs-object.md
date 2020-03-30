---
title: SQL Server 代理 - Jobs 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 63c2638f6b6f58d3c3cafd8e8dd601a5a467b210
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67987330"
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server 代理中的 Jobs 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 代理的 **Jobs** 性能对象包含的性能计数器可报告有关 SQL Server 代理作业的信息。 下表列出了此对象包含的计数器。  
  
 下表介绍了 **SQLAgent:Jobs** 计数器。  
  
|名称|说明|  
|----------|-----------------|  
|**Active Jobs**|该计数器报告当前运行的作业数。|  
|**Failed jobs**|该计数器报告失败退出的作业数。|  
|**Job success rate**|该计数器报告所执行的作业中成功完成的百分比。|  
|**Jobs activated/minute**|该计数器报告最后一分钟内启动的作业数。|  
|**Queued jobs**|该计数器报告已准备好供 SQL Server 代理准备运行但尚未开始运行的作业数。|  
|**Successful jobs**|该计数器报告成功退出的作业数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|实例|说明|  
|--------------|-----------------|  
|**_Total**|所有作业的信息。|  
|**警报**|由警报启动的作业的信息。|  
|**其他**|不是由警报或计划启动的作业的信息。 通常这些作业是使用 **sp_start_job**手动启动的作业。|  
|**计划**|由计划启动的作业的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [执行作业](../../ssms/agent/implement-jobs.md)   
 [使用性能对象](../../ssms/agent/use-performance-objects.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
