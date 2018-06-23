---
title: 监视复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 81f596d2-27a5-489d-bf8d-0f4361decd02
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 95827211835e7822544238a70fab4a36042f5602
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024548"
---
# <a name="monitoring-replication"></a>监视复制
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制监视器是一个图形工具，可用于监视复制拓扑的整体运行状况。 复制监视器提供了发布和订阅的状态和性能的详细信息，使您能够回答下列常见问题：  
  
-   我的复制系统是否正常？  
  
-   哪些订阅比较慢？  
  
-   我的事务订阅滞后程度如何？  
  
-   在事务复制中，现在提交的事务要过多久才能到达订阅服务器？  
  
-   为什么我的合并订阅比较慢？  
  
-   为什么代理不运行？  
  
 若要监视复制，用户必须是分发服务器上 **sysadmin** 固定服务器角色的成员，或者是分发数据库中 **replmonitor** 固定数据库角色的成员。 系统管理员可以将任何用户添加到 **replmonitor** 角色中，这样该用户就可以在复制监视器中查看复制活动，但不能管理复制。  
  
## <a name="in-this-section"></a>本节内容  
 下列主题提供有关复制监视器功能的信息。  
  
 [复制监视器界面概述](overview-of-the-replication-monitor-interface.md)  
 介绍复制监视器中的每个窗口和选项卡，并提供有关如何回答上面列出的问题的信息。  
  
 [启动复制监视器](start-the-replication-monitor.md)  
 说明如何启动复制监视器。  
  
 [允许非管理员使用复制监视器](allow-non-administrators-to-use-replication-monitor.md)  
 说明如何将权限分配给非管理员，以便他们可以使用复制监视器。  
  
 [从复制监视器中添加和删除发布服务器](add-and-remove-publishers-from-replication-monitor.md)  
 说明如何在复制监视器中添加或删除发布服务器。  
  
 [刷新复制监视器中的数据](refresh-data-in-replication-monitor.md)  
 说明如何刷新复制监视器中的数据。  
  
 [用复制监视器监视性能](monitor-performance-with-replication-monitor.md)  
 说明如何在复制监视器中监视性能，包括有关设置性能阈值的信息。 还包括合并复制的项目级统计信息，根据这些信息可以了解详细的处理过程。  
  
 [为事务复制测量滞后时间和验证连接](measure-latency-and-validate-connections-for-transactional-replication.md)  
 介绍跟踪令牌，跟踪令牌使您可以衡量事务复制拓扑的性能。  
  
 [监视复制代理](../agents/replication-agents.md)  
 说明如何查找有关每个复制代理的信息。  
  
 [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)  
 说明可在复制监视器中设置的警告、阈值和警报。 建议您对拓扑启用警告，以便及时获悉有关状态和性能的信息。  
  
 [缓存、刷新和复制监视器性能](caching-refresh-and-replication-monitor-performance.md)  
 说明复制监视器如何进行数据缓存和计算以提高性能，还解释了刷新用户界面与刷新缓存的关系。  
  
 [在复制监视器中查看发布和订阅状态](view-publication-and-subscription-status-in-replication-monitor.md)  
 说明如何使用复制监视器查看发布或订阅的状态信息。  
  
 [查看发布服务器的信息和执行其任务（复制监视器）](view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
 说明如何使用复制监视器查看发布服务器的信息和执行其任务。  
  
 [查看发布的信息和执行其任务（复制监视器）](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  
 说明如何使用复制监视器查看发布的信息和执行其任务。  
  
 [查看与发布关联的代理的信息和执行其任务（复制监视器）](view-information-and-perform-tasks-for-publication-agents.md)  
 说明如何使用复制监视器查看与发布相关的代理的信息和执行其任务。  
  
 [查看订阅的信息和执行其任务（复制监视器）](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
 说明如何使用复制监视器查看订阅的信息和执行其任务。  
  
 [查看与订阅关联的代理的信息和执行其任务（复制监视器）](view-information-and-perform-tasks-for-subscription-agents.md)  
 说明如何使用复制监视器查看与订阅相关的代理的信息和执行其任务。  
  
  