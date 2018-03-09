---
title: "订阅 - 同步历史记录（合并订阅，SQL Server 2000）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 0a0deab2-1c08-4371-9681-d9403e0236cc
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0462e11db4e712fb9e0b5b37494dacc0924e60a1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="subscription-synchronization-history-merge-subscription-sql-server-2000"></a>订阅 - 同步历史记录（合并订阅，SQL Server 2000）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]“同步历史记录”选项卡显示有关合并代理的详细信息，包括状态、历史记录、信息性消息和所有错误消息。  
  
## <a name="options"></a>“常规”  
 从“视图”  菜单中选择要查看的合并代理会话，然后在标记为“合并代理的会话” 的网格中选择特定会话。 有关此会话的详细信息显示在标记为 **“所选会话中的操作”**的网格中。 如果所选会话由于出错而结束，则还将显示一个标记为 **“所选会话的错误详细信息或消息”** 的文本区域。  
  
 **“视图”**  
 选择要查看的合并代理会话。 合并代理通常连续运行，因此可能只有一个可供查看的会话。  
  
 **“状态”**  
 合并代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   已完成  
  
-   正在重试  
  
-   正在运行  
  
 **Start Time**  
 会话的开始时间。  
  
 **结束时间**  
 会话的结束时间。 如果代理尚未停止，此字段为空。  
  
 **Duration**  
 合并代理已在此会话中运行的时间。 如果代理当前正在运行，该时间表示已用时间；如果代理会话已经结束，则该时间表示会话的总时间。  
  
 **错误消息**  
 如果某会话由于出错而结束，此字段将会显示合并代理记录的上一条错误消息。 如果某会话未因出错而结束，此字段为空白。  
  
 **操作消息**  
 合并代理在所选会话过程中记录的所有信息性消息和错误消息。  
  
 **操作时间**  
 执行 **“操作消息”** 列中所述操作的时间。  
  
 **“所选会话的错误详细信息或消息”**  
 只有当所选会话在 **“状态”** 列中显示 **“错误”** 值时，才会显示此项。 此文本区域显示详细错误信息以及出错时尝试执行的命令。 另外，还包括指向与该错误相关的其他内容的链接。  
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看与订阅关联的代理的信息和执行其任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
