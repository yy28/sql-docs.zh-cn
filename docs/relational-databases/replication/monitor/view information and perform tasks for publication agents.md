---
title: "查看与发布相关的代理的信息并执行此代理的任务（复制监视器） | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "代理 [SQL Server 复制], 查看信息"
  - "查看复制代理信息"
  - "代理 [SQL Server 复制], 复制监视器中的任务"
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 查看与发布相关的代理的信息并执行此代理的任务（复制监视器）
  复制监视器提供了 **“代理”** 选项卡，其中包含与所选发布关联的代理的相关信息。 分发代理和合并代理均与订阅相关联有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
 此选项卡显示有关下列代理的信息：  
  
-   快照代理，用于所有发布。  
  
-   日志读取器代理，用于所有事务发布。  
  
-   队列读取器代理，用于为排队更新订阅启用的事务发布。  
  
 若要查看有关此选项卡上的选项的详细信息，请在菜单栏上单击 **“帮助”** 。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 查看与发布相关的代理的信息并执行此代理的任务  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  单击 **“代理”** 选项卡来查看有关代理的信息。 您还可以通过此选项卡访问更详细的信息并执行任务：  
  
    -   若要查看详细的信息 （如信息性消息和任何错误消息） 代理，右键单击代理，，然后单击 **查看详细信息**。  
  
    -   要查看有关运行 （如计划、 作业步骤的详细信息等） 的代理的作业的详细的信息，请右键单击代理，，然后单击 **属性**。  
  
    -   要管理的代理配置文件，用鼠标右键单击该代理，然后单击 **代理配置文件**。 有关详细信息，请参阅 [使用复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
    -   要启动未运行的代理，请右键单击代理，，然后单击 **启动代理**。  
  
    -   要停止正在运行的代理，请右键单击代理，，然后单击 **停止代理**。  
  
## 另请参阅  
 [在复制监视器中设置阈值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [查看信息并执行任务发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [复制代理管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  