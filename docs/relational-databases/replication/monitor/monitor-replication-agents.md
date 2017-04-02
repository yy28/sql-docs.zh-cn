---
title: "监视复制代理 | Microsoft Docs"
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
  - "监视性能 [SQL Server 复制], 代理"
  - "日志读取器代理, 监视"
  - "复制监视器, 代理"
  - "合并代理, 监视"
  - "队列读取器代理, 监视"
  - "快照代理, 监视"
  - "代理 [SQL Server 复制], 监视"
  - "分发代理, 监视"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 监视复制代理
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制监视器提供复制活动的系统视图，并且还可以直观地查找有关特定代理的信息。 以下列表列出了每个代理、可以在其中找到代理的选项卡（位于复制监视器中）以及指向说明如何访问这些选项卡的主题的链接：  
  
-   以下代理与复制监视器中的发布相关联：  
  
    -   快照代理  
  
    -   日志读取器代理  
  
    -   队列读取器代理  
  
     访问信息和与这些代理通过下列选项卡相关联的任务︰ **代理** （适用于每个发布服务器和发布） 和 **警告** （适用于每个发布）。 有关详细信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
-   以下代理与复制监视器中的订阅相关联：  
  
    -   分发代理  
  
    -   合并代理  
  
     访问信息和与这些代理通过下列选项卡相关联的任务︰ **订阅监视列表** （适用于每个发布服务器） 或 **所有订阅** （适用于每个发布） 选项卡。 有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 使用 SQL Server Management Studio 监视复制代理  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 为监视复制代理提供下列对话框：  
  
-   **查看快照代理状态** （对于所有发布）  
  
-   **查看日志读取器代理状态** （对于所有事务性发布）  
  
-   **查看同步状态** （针对所有订阅; 此对话框中，对分发代理和合并代理的访问）  
  
 复制监视器提供有关每个代理的补充信息，并且如果使用了队列读取器代理，它还会对其进行监视。 有关详细信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), ，[查看信息并执行与发布 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), ，和 [查看信息并执行与订阅 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
#### 监视快照代理和日志读取器代理  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击发布，然后单击 **查看日志读取器代理状态** 或 **查看快照代理状态**。  
  
4.  在 **“查看日志读取器代理状态”** 或 **“查看快照代理状态”** 对话框中：  
  
    -   查看代理状态。  
  
    -   必要时启动或停止代理。  
  
    -   单击 **“监视器”** 启动 **复制监视器**。  
  
5.  单击 **“关闭”**。  
  
#### 监视分发代理和合并代理（从发布服务器）  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开要监视的订阅的发布。  
  
4.  右键单击该订阅，然后单击 **查看同步状态**。  
  
5.  在 **“查看同步状态”** 对话框中：  
  
    -   查看代理状态。  
  
    -   必要时启动或停止代理。  
  
    -   对于推送订阅，单击 **“监视器”** 启动 **复制监视器**。  
  
    -   对于请求订阅，单击 **“查看作业历史记录”** 启动 **日志文件查看器**，此查看器可以显示代理日志的输出。  
  
6.  单击 **“关闭”**。  
  
#### 监视分发代理和合并代理（从订阅服务器）  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击你想要监视，然后单击的订阅 **查看同步状态**。  
  
4.  在 **“查看同步状态”** 对话框中：  
  
    -   查看代理状态。  
  
    -   必要时启动或停止代理。  
  
    -   单击 **“查看作业历史记录”** 启动 **日志文件查看器**，此查看器可以显示代理日志的输出。  
  
5.  单击 **“关闭”**。  
  
## 另请参阅  
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [复制代理概述](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  