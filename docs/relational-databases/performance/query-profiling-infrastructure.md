---
title: 查询分析基础结构 |Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query profiling
- lightweight query profiling
- lightweight profiling
- lwp
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 481a2fe18c99621b8331ab204a99e1d7efd37f24
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55889978"
---
# <a name="query-profiling-infrastructure"></a>查询分析基础结构
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 提供了访问查询执行计划的运行时信息的功能。 出现性能问题时，最重要的操作之一是准确了解正在执行的工作负载以及如何驱动使用资源。 为此，访问[实际执行计划](../../relational-databases/performance/display-an-actual-execution-plan.md)是很重要的。

虽然查询完成是实际查询计划可用性的先决条件，但[实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)可以提供对查询执行过程的实时见解，因为数据是从一个[查询计划运算符](../../relational-databases/showplan-logical-and-physical-operators-reference.md)移动到另一个。 实时查询计划显示总体查询进度和操作员级运行时执行统计信息（例如处理的行数、经过的时间、操作员进度等）。由于此数据是实时可用的，无需等待完成查询，因此这些执行统计信息对于调试查询性能问题非常有用，例如长时间运行查询以及无限期运行而从未完成过的查询。

## <a name="the-standard-query-execution-statistics-profiling-infrastructure"></a>标准查询执行统计信息分析基础结构

必须启用查询执行统计信息配置文件基础结构或标准分析，以收集有关执行计划的信息，即行数、CPU 和 I/O 使用情况。 以下收集目标会话的执行计划信息的方法利用标准分析基础结构：

- [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) 
- [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
- [实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)

> [!NOTE]
> 使用 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的实时查询统计信息可以利用标准分析基础结构。    
> 在更高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果已启用[轻型分析基础结构](#lwp)，那么它会被实时查询统计信息而不是标准分析所利用。

以下为所有会话全局收集执行计划信息的方法利用标准分析基础结构：

-  ***query_post_execution_showplan*** 扩展事件。 若要启用扩展事件，请参阅 [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  
- [SQL Trace](../../relational-databases/sql-trace/sql-trace.md) 和 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md) 中的 Showplan XML 跟踪事件。 有关此跟踪事件的详细信息，请参阅 [Showplan XML 事件类](../../relational-databases/event-classes/showplan-xml-event-class.md)。

当运行使用 query_post_execution_showplan 事件的扩展事件会话时，还会填充 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV，它使用[活动监视器](../../relational-databases/performance-monitor/activity-monitor.md)或直接查询 DMV，为所有会话启用实时查询统计。 有关详细信息，请参阅 [Live Query Statistics](../../relational-databases/performance/live-query-statistics.md)。

## <a name="lwp"></a>轻型查询执行统计信息分析基础结构

从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，引入了新的轻型查询执行统计信息概要分析基础结构或轻型分析。 

> [!NOTE]
> 本机编译存储过程不支持轻型分析。  

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v1"></a>轻型查询执行统计信息分析基础结构 v1

**适用对象**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 到 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]）。 
  
从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，通过引入轻型分析，减少了收集执行计划信息的性能开销。 和标准分析不同，轻型分析不收集 CPU 运行时信息。 但是，轻型分析仍收集行计数和 I/O 使用情况信息。

还引入了一个新的利用轻型分析的 query_thread_profile 扩展事件。 此扩展事件公开了每个运算符的执行统计信息，从而可以更深入地了解每个节点和线程的性能。 使用此扩展事件的示例会话可以按下面的示例进行配置：

```sql
CREATE EVENT SESSION [NodePerfStats] ON SERVER
ADD EVENT sqlserver.query_thread_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

> [!NOTE]
> 有关查询分析的性能开销的详细信息，请参阅博客文章[Developers Choice:Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)（开发人员之选：随时随地查询进度）。 

当运行使用 query_thread_profile 事件的扩展事件会话时，还会使用轻型分析填充 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV，它使用[活动监视器](../../relational-databases/performance-monitor/activity-monitor.md)或直接查询 DMV，为所有会话启用实时查询统计。

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v2"></a>轻型查询执行统计信息分析基础结构 v2

**适用对象**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 到 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]）。 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 包括具有最小开销的轻型分析的修订版本。 对于“适用范围”中提到的上述版本，使用[跟踪标志 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)也可以全局启用轻型分析。 引入了新的 DMF [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 以返回正在进行的请求的查询执行计划。

从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11 开始，如果未全局启用轻型分析，则可以使用新的 [USE HINT查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)参数 QUERY_PLAN_PROFILE 以查询级别启用轻型分析，且适用于任何会话。 当包含此新提示的查询完成时，还会输出新的 query_plan_profile 扩展事件，该事件提供类似于 query_post_execution_showplan 扩展事件的实际执行计划 XML。 

> [!NOTE]
> 即使未使用查询提示，query_plan_profile 扩展事件也会利用轻量分析。 

使用 query_plan_profile 扩展事件的示例会话可以像下面的示例一样进行配置：

```sql
CREATE EVENT SESSION [PerfStats_LWP_Plan] ON SERVER
ADD EVENT sqlserver.query_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v3"></a>轻型查询执行统计信息分析基础结构 v3

**适用对象**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 开始）

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 包括一个新修订的轻型分析版本，用于收集所有执行的行计数信息。 默认情况下，[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 中已启用轻型分析，跟踪标志 7412 无效。

## <a name="remarks"></a>Remarks

> [!IMPORTANT]
> 由于在执行引用 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 的监视存储过程时可能存在随机 AV，因此请确保在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中安装了 [KB 4078596](http://support.microsoft.com/help/4078596)。

从轻型分析 v2 开始，其开销很低，任何尚未受 CPU 限制的服务器都可连续运行轻型分析，并允许数据库专业人员随时使用任何正在运行的执行，例如使用活动监视器或直接查询 `sys.dm_exec_query_profiles`，并获取运行时统计信息的查询计划。

有关查询分析的性能开销的详细信息，请参阅博客文章[Developers Choice:Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)（开发人员之选：随时随地查询进度）。 

## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [性能监视和优化工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [打开活动监视器 (SQL Server Management Studio)](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [活动监视器](../../relational-databases/performance-monitor/activity-monitor.md)     
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [使用扩展事件监视系统活动](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)      
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [跟踪标志](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Showplan 逻辑运算符和物理运算符参考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
 [实际执行计划](../../relational-databases/performance/display-an-actual-execution-plan.md)    
 [实时查询统计信息](../../relational-databases/performance/live-query-statistics.md)      
 [Developers Choice:Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)（开发人员之选：随时随地查询进度）
