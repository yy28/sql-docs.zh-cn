---
title: SQL Server Profiler 模板和权限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e5ecb04dcca4a3e73f1d2351f569960cfd7fec0c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-profiler-templates-and-permissions"></a>SQL Server Profiler 模板和权限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何在内部解析查询。 这就使管理员能够准确查看提交到服务器的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或多维表达式，以及服务器是如何访问数据库或多维数据集以返回结果集的。  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]可以执行下列操作：  
  
-   创建基于可重用模板的跟踪  
  
-   当跟踪运行时监视跟踪结果  
  
-   将跟踪结果存储在表中  
  
-   根据需要启动、停止、暂停和修改跟踪结果  
  
-   重播跟踪结果  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 只监视感兴趣的事件。 如果跟踪变得太大，可以基于所需的信息进行筛选，以便只收集部分事件数据。 监视过多事件会增加服务器和监视进程的开销，并且可能导致跟踪文件或跟踪表变得很大，尤其是当监视进程持续很长时间时。  
  
> [!NOTE]  
>  大于 1 GB 的跟踪列值将返回错误，并且会在跟踪输出中被截断。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[SQL Server Profiler 模板](../../tools/sql-server-profiler/sql-server-profiler-templates.md)|介绍 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]附带的预定义跟踪模板。|  
|[运行 SQL Server Profiler 所需的权限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|介绍运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]时所需的权限。|  
|[保存跟踪和跟踪模板](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|介绍如何保存跟踪输出和将跟踪定义保存到模板中。|  
|[修改跟踪模板](../../tools/sql-server-profiler/modify-trace-templates.md)|介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]来修改跟踪模板。|  
|[启动跟踪](../../tools/sql-server-profiler/start-a-trace.md)|介绍启动、暂停或停止跟踪时将发生的情况。|  
|[将跟踪与 Windows 性能日志数据关联](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 将 Windows 性能日志数据与跟踪相关联。|  
|[使用 SQL Server Profiler 查看和分析跟踪](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|介绍如何使用跟踪对数据进行故障排除、在跟踪中显示对象名以及在跟踪中查找事件。|  
|[使用 SQL Server Profiler 分析死锁](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 识别造成死锁的原因。|  
|[在 SQL Server Profiler 中使用 SHOWPLAN 结果来分析查询](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 收集和显示“显示计划”和“显示计划统计信息”的结果。|  
|[使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]设置针对数据列的筛选器以筛选跟踪输出。|  
|[重播跟踪](../../tools/sql-server-profiler/replay-traces.md)|解释重播跟踪的意义以及重播跟踪所需的条件。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [启动 SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
