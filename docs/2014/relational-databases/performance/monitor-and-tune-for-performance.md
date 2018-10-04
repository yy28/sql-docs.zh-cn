---
title: 监视和优化性能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1acbc868471ebae0de110d8c346303e45cff50a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179757"
---
# <a name="monitor-and-tune-for-performance"></a>监视和优化性能
  监视数据库的目的是评估服务器的性能。 有效监视包括定期拍摄当前性能的快照来隔离导致问题的进程，以及连续收集数据来跟踪性能趋势。  
  
 日常数据库性能评估有助于使响应时间最小化并使吞吐量最大化，从而实现最佳性能。 有效网络流量、磁盘 I/O 和 CPU 使用率是实现最佳性能的关键。 您需要透彻地分析应用程序要求，了解数据的逻辑结构和物理结构，评估数据库使用情况，并协商使用 [如联机事务处理 (OLTP) 与决策支持] 冲突之间的平衡措施。  
  
## <a name="benefits-of-monitoring-and-tuning-databases-for-performance"></a>监视和优化数据库性能的好处  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Microsoft Windows 操作系统提供实用工具，允许您查看数据库的当前状态并跟踪条件变化时的性能。 可使用多种工具和技术来监视 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 了解如何监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有助于：  
  
-   确定是否可以提高性能。 例如，通过监视常用查询的响应时间，可以确定是否需要更改表的查询或索引。  
  
-   评估用户活动。 例如，通过监视尝试连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的用户，可以确定安全设置是否充分以及是否需要测试应用程序或开发系统。 例如，通过在执行 SQL 查询时对其进行监视，可以确定这些查询是否编写正确并生成预期的结果。  
  
-   解决任何问题或调试应用程序组件（如存储过程）。  
  
### <a name="monitoring-in-a-dynamic-environment"></a>动态环境中的监视  
 监视操作非常重要，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在动态环境中提供服务。 更改条件会导致性能发生变化。 在评估中，您可以看到性能会随着用户数量增加、用户访问和连接方法改变、数据库内容增加、客户端应用程序改变、应用程序中的数据变化、查询变得更加复杂以及网络流量上升而变化。 通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具来监视性能，可以将性能的某些变化与条件和复杂查询的变化相关联。 下列方案提供了此方面的示例：  
  
-   通过监视常用查询的响应时间，可以确定是否需要更改查询或执行查询的表上的索引。  
  
-   通过在执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询时对其进行监视，可以确定这些查询是否编写正确并生成预期的结果。  
  
-   通过监视试图连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的用户，可以确定安全设置是否得当并测试应用程序或开发系统。  
  
 响应时间是指以可视确认信息（指出正在处理查询）的形式将结果集的首行返回给用户所需的时间。 吞吐量是指在一段给定时间内，服务器处理的查询总数。  
  
 随着用户数量的增加，对服务器资源的竞争也会更激烈，进而导致响应时间增加和总体吞吐量减少。  
  
## <a name="monitoring-and-tuning-performance-tasks"></a>监视和优化性能任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|[监视 SQL Server 组件](monitor-sql-server-components.md)|提供有效地监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的任何组件所需的必要步骤。|  
|[性能监视和优化工具](performance-monitoring-and-tuning-tools.md)|列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 监视和优化工具。|  
|[建立性能基线](establish-a-performance-baseline.md)|提供有关如何建立性能基准的信息。|  
|[隔离性能问题](isolate-performance-problems.md)|介绍如何隔离数据库性能问题。|  
|[识别瓶颈](identify-bottlenecks.md)|介绍如何监视和跟踪服务器性能，以发现瓶颈。|  
|[服务器性能和活动监视](server-performance-and-activity-monitoring.md)|介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 性能和活动监视工具。|  
|[显示和保存执行计划](display-and-save-execution-plans.md)|介绍如何显示执行计划并将其保存到 XML 格式的文件中。|  
|[使用查询存储来监视性能](monitoring-performance-by-using-the-query-store.md)|查询存储将自动捕获查询、计划和运行时统计信息的历史记录，并保留它们以供查阅。|  
  
## <a name="see-also"></a>请参阅  
 [企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [数据库引擎优化顾问](database-engine-tuning-advisor.md)   
 [监视资源使用情况（系统监视器）](../performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server 事件探查器](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
