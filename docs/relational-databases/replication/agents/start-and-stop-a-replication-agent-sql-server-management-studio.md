---
title: "启动和停止复制代理 (SQL Server Management Studio) | Microsoft Docs"
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
  - "代理 [SQL Server 复制], 停止"
  - "代理 [SQL Server 复制], 启动"
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 启动和停止复制代理 (SQL Server Management Studio)
  可以从  中的 **“作业”** 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from “作业” Monitor. 可启动和停止以下代理和作业：  
  
-   快照代理，用于所有发布。  
  
-   日志读取器代理，用于所有事务发布。  
  
-   队列读取器代理，用于为排队更新订阅启用的事务发布。  
  
-   分发代理，用于同步对事务发布和快照发布的订阅。  
  
-   合并代理，用于同步对合并发布的订阅。  
  
-   复制维护作业。  
  
 有关启动合并代理和分发代理的详细信息，请参阅 [同步推送订阅](../../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [同步请求订阅](../../../relational-databases/replication/synchronize-a-pull-subscription.md)。 有关维护作业的详细信息，请参阅 [运行复制维护作业 （&) #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)。  
  
 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 从 Management Studio 启动和停止快照代理或日志读取器代理  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点和 **“复制”** 文件夹。  
  
2.  展开 **本地发布** 文件夹，然后再右键单击发布。  
  
3.  单击 **“查看快照代理状态”** 或 **“查看日志读取器代理状态”**。  
  
4.  单击 **“启动”** 或 **“停止”**。  
  
### 从 Management Studio 启动和停止队列读取器代理  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  对于代理，右键单击该作业，然后单击 **作业开始** 或 **停止作业**。 队列读取器代理作业的名称是在窗体 **[\< 分发服务器>]。 \< 整数>**。  
  
### 从复制监视器启动和停止快照代理、日志读取器代理或队列读取器代理  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  右键单击代理，然后单击 **启动代理** 或 **停止代理**。  
  
## 另请参阅  
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [复制代理可执行文件概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [复制代理概述](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  