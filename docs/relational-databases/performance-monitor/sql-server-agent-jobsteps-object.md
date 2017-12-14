---
title: "SQL Server 代理 - JobSteps 对象 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d6953a342ab24540da33464962712ea43579f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server 代理中的 JobSteps 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理中的 JobSteps 性能对象包含用于报告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤相关信息的性能计数器。 下表列出了此对象包含的计数器。  
  
 下表列出了 **SQLAgent:JobSteps** 计数器。  
  
|名称|说明|  
|----------|-----------------|  
|**Active steps**|此计数器报告当前运行的作业步骤数。|  
|**Queued steps**|此计数器报告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理准备运行但尚未开始运行的作业步骤数。|  
|**Total step retries**|此计数器报告自上次服务器重新启动以来 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重试某作业步骤的总次数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|实例|说明|  
|--------------|-----------------|  
|**_Total**|有关所有作业步骤的信息。|  
|**ActiveScripting**|有关使用 **ActiveScripting** 子系统的作业步骤的信息。|  
|**ANALYSISCOMMAND**|有关使用 ANALYSISCOMMAND 子系统的作业步骤的信息。|  
|**ANALYSISQUERY**|有关使用 ANALYSISQUERY 子系统的作业步骤的信息。|  
|**CmdExec**|有关使用 **CmdExec** 子系统的作业步骤的信息。|  
|**Distribution**|有关使用 **Distribution** 子系统的作业步骤的信息。|  
|**Dts**|有关使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 子系统的作业步骤的信息。|  
|**LogReader**|有关使用 **LogReader** 子系统的作业步骤的信息。|  
|**合并**|有关使用 **Merge** 子系统的作业步骤的信息。|  
|**PowerShell**|有关使用 **PowerShell** 子系统的作业步骤的信息。|  
|**QueueReader**|有关使用 **QueueReader** 子系统的作业步骤的信息。|  
|**快照**|有关使用 **Snapshot** 子系统的作业步骤的信息。|  
|**TSQL**|有关执行 [!INCLUDE[tsql](../../includes/tsql-md.md)]的作业步骤的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [管理作业步骤](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31)   
 [使用性能对象](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
