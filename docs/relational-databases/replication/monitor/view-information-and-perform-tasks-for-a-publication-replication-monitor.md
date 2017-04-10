---
title: "查看发布的信息和执行其任务（复制监视器） | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查看发布信息"
  - "发布 [SQL Server 复制], 查看信息"
  - "发布 [SQL Server 复制], 复制监视器任务"
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 查看发布的信息和执行其任务（复制监视器）
  复制监视器提供下列选项卡，其中包括有关选定发布的信息：  
  
-   **所有订阅**  
  
     此选项卡显示有关所选发布的所有订阅的信息。  
  
-   **代理**  
  
     此选项卡显示与发布使用的所有代理有关的信息：  
  
    -   快照代理，用于所有发布。  
  
    -   日志读取器代理，用于所有事务发布。  
  
    -   队列读取器代理，用于具有排队更新订阅的事务发布。  
  
-   **警告** (对于分发服务器运行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更高版本)  
  
    -   此选项卡允许您为代理指定警告和警报。  
  
-   **跟踪令牌** (事务复制仅用于运行的分销商 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更高版本)  
  
     可以使用此选项卡衡量滞后时间，滞后时间是指从事务在发布服务器上提交到相应的事务在订阅服务器上提交之间间隔的时间。  
  
 有关每个选项卡上各选项的详细信息，请在右窗格中单击相应选项卡，然后在菜单栏上单击 **“帮助”** 。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 查看发布的信息并执行任务  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  要查看和修改发布属性，用鼠标右键单击该发布，然后单击 **属性**。  
  
3.  若要查看有关订阅的信息，请单击 **“所有订阅”** 选项卡。  
  
     要查看和修改订阅属性，右键单击该订阅，然后单击 **属性**。 您还可以通过该选项卡访问更详细的信息和执行任务。 有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
4.  若要查看有关代理的信息，请单击 **“代理”** 选项卡。 您还可以通过该选项卡访问更详细的信息和执行任务。 有关详细信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
5.  若要查看代理警告和阈值的相关信息，请单击 **“警告”** 选项卡。 有关详细信息，请参阅 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
6.  若要查看有关跟踪令牌的信息，请单击 **“跟踪令牌”** 选项卡。 有关如何使用跟踪令牌的详细信息，请参阅 [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## 另请参阅  
 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  