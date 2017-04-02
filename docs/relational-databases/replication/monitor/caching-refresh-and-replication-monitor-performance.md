---
title: "缓存、刷新和复制监视器性能 | Microsoft Docs"
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
  - "监视性能 [SQL Server 复制], 复制监视器"
  - "缓存 [SQL Server 复制], 复制"
  - "复制监视器, 缓存"
  - "刷新数据"
  - "复制监视器, 刷新"
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# 缓存、刷新和复制监视器性能
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制监视器旨在有效地监视生产系统中的大量计算机。 系统定期对复制监视器用来执行计算和收集数据的查询进行缓存和刷新。 缓存可减少在复制监视器中查看不同页时所需的查询和计算次数，并可很好地满足多个用户的监视需要。  
  
 缓存刷新由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业“用于分发的复制监视刷新器” 进行处理。 作业是连续运行的，但缓存刷新计划取决于上次刷新后等待的特定时间：  
  
-   如果上次创建缓存后，代理历史记录有更改，则等待时间是以下时间中的最小值：4 秒或创建上一个缓存所用的时间。  
  
-   如果上次创建缓存后，代理历史记录没有更改（可能有其他更改），则等待时间是以下时间中的最大值：30 秒或创建上一个缓存所用的时间。  
  
## 刷新复制监视器用户界面  
 可以通过下列方式刷新复制监视器用户界面：  
  
-   复制监视器主窗口（包括所有选项卡），默认每 5 秒钟自动刷新一次。 自动刷新不强制刷新缓存；用户界面显示缓存中最新的数据。 可以通过编辑发布服务器设置为发布服务器的所有关联窗口自定义刷新速率。 也可以禁用发布服务器的自动刷新。  
  
-   默认情况下，从复制监视器启动的详细信息窗口不自动刷新，但与正在同步的合并订阅相关的窗口除外。 如果指定详细信息窗口自动刷新，则它们的刷新速率与复制监视器主窗口相同。  
  
-   所有窗口都可以手动都刷新通过按 f5 键或右键单击复制监视器树中的节点，单击 **刷新**。 手动刷新会强制刷新缓存。  
  
 有关详细信息，请参阅 [刷新复制监视器中的数据](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md)。  
  
## 性能注意事项  
 尽管复制监视器旨在高效运行，但请注意以下事项：  
  
-   如果有大量的发布或订阅，请为用户界面设置一个频率较低的自动刷新计划。  
  
-   避免并发运行多个复制监视器实例。  
  
-   避免注册大量分发服务器，并避免设置复制监视器自动连接到所有分发服务器上。  
  
## 另请参阅  
 [运行复制维护作业 （&） #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  