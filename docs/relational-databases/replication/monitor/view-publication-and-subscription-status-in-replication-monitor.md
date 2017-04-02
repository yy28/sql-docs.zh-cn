---
title: "在复制监视器中查看发布和订阅状态 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "日志读取器代理, 监视"
  - "合并代理, 监视"
  - "队列读取器代理, 监视"
  - "发布 [SQL Server 复制], 查看信息"
  - "快照代理, 监视"
  - "分发代理, 监视"
  - "监视性能 [SQL Server 复制], 发布状态"
  - "监视性能 [SQL Server 复制], 订阅状态"
  - "订阅 [SQL Server 复制], 查看状态"
  - "复制监视器、发布和订阅状态"
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 在复制监视器中查看发布和订阅状态
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制监视器显示发布和订阅的状态信息：  
  
-   发布的状态由其订阅的最高优先级状态决定。 例如，如果对发布的一个订阅有错误，另一个订阅有性能问题，则显示发布的错误状态。  
  
-   订阅的状态由处理该订阅的代理的状态决定。 对于合并复制，由合并代理的状态决定。 对于事务复制，由日志读取器代理或分发代理（显示较高优先级状态；如果使用的是排队更新订阅，则状态还可以由队列读取器代理的状态决定）的状态决定。 对于快照复制，由快照代理或分发代理（显示较高优先级状态）的状态决定。  
  
 下列表列出了发布和订阅的可能状态值。 只有在达到或超过阈值时，才显示三个状态值。  
  
-   过期订阅  
  
     本状态值适用于所有类型的复制。 有关详细信息，请参阅 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
-   “严重”状态下的性能  
  
     此状态值适用于事务复制和合并复制。 有关详细信息，请参阅 [用复制监视器监视性能](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
-   长时间运行的合并  
  
     此状态值适用于合并复制。 有关详细信息，请参阅 [用复制监视器监视性能](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 除提供发布和订阅状态外，合并复制还提供项目级统计信息，其中包括关于以下内容的详细信息：完成某个合并阶段还需要多长时间；处理某个给定项目花费的时间；订阅服务器正在使用的连接类型以及其他重要信息。 统计信息显示在复制监视器的合并代理窗口中。 快照复制和事务复制提供有关分发代理处理的详细信息。  
  
 **查看发布和订阅状态**  
  
-   复制监视器︰ [查看信息并执行任务发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) 和 [查看信息并为订阅 & #40; 执行任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
  
 **查看代理的详细信息**  
  
-   复制监视器︰ [查看信息并执行与发布 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md) 和 [查看信息并执行与订阅 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 发布状态值  
 下表按优先级顺序显示了发布状态值及其对应的图标。  
  
|状态|图标|  
|------------|----------|  
|错误|![UI 图标：error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI 图标：error")|  
|“严重”状态下的性能|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|正在重试失败的命令|![UI 图标：复制代理重试](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI 图标：复制代理重试")|  
|确定|none|  
  
## 订阅状态值  
 下列表按优先级顺序显示了订阅状态值及其对应的图标。 可以为一个订阅可以处于两种状态在同一时间，如 **即将过期/已过期** 和 **正在重试失败的命令**; 最高优先级状态显示。  
  
 对 status 值 **性能关键**, ，**即将过期/已过期**, ，和 **未初始化** 都是警告。 显示警告时，复制监视器还显示是否有代理在运行。 例如，状态可能为 **“正在运行，‘严重’状态下的性能”**。  
  
### 事务订阅  
  
|状态|图标|  
|------------|----------|  
|错误|![UI 图标：error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI 图标：error")|  
|“严重”状态下的性能|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|即将过期/已过期|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|未初始化的订阅 |![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|正在重试失败的命令|![UI 图标：复制代理重试](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI 图标：复制代理重试")|  
|未运行|![UI 图标：复制代理已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI 图标：复制代理已停止")|  
|正在运行|![UI 图标：复制代理运行](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI 图标：复制代理运行")|  
  
### 合并订阅  
  
|状态|图标|  
|------------|----------|  
|错误|![UI 图标：error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI 图标：error")|  
|“严重”状态下的性能|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|长时间运行的合并|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|即将过期/已过期|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|未初始化的订阅 |![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|正在重试失败的命令|![UI 图标：复制代理重试](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI 图标：复制代理重试")|  
|同步|![UI 图标：复制代理运行](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI 图标：复制代理运行")|  
|未同步|![UI 图标：复制代理已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI 图标：复制代理已停止")|  
  
### 快照订阅  
  
|状态|图标|  
|------------|----------|  
|错误|![UI 图标：error](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI 图标：error")|  
|即将过期/已过期|![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|未初始化的订阅 |![UI 图标：warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI 图标：warning")|  
|正在重试失败的命令|![UI 图标：复制代理重试](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI 图标：复制代理重试")|  
|同步|![UI 图标：复制代理运行](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI 图标：复制代理运行")|  
|未同步|![UI 图标：复制代理已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI 图标：复制代理已停止")|  
  
## 另请参阅  
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  