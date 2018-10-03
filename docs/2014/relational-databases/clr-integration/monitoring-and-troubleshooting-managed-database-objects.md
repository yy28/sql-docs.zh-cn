---
title: 托管数据库对象监视和故障排除 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f03266a5460e9e34a404256e5df415f799b29d98
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090647"
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>托管数据库对象监视和故障排除
  本主题提供的信息介绍用于对正在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中运行的托管数据库对象和程序集进行监视和故障排除的工具。  
  
## <a name="profiler-trace-events"></a>事件探查器跟踪事件  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供 SQL 跟踪和事件通知来监视数据库引擎中发生的事件。 通过记录指定事件，SQL 跟踪可以帮助您解决性能问题、审核数据库活动、收集用于测试环境的示例数据、调试 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句和存储过程以及为性能分析工具收集数据。 有关详细信息，请参阅[SQL 跟踪](../sql-trace/sql-trace.md)并[扩展事件](../extended-events/extended-events.md)。  
  
|事件|Description|  
|-----------|-----------------|  
|[Assembly Load 事件类](../../database-engine/assembly-load-event-class.md)|用于监视程序集加载请求（成功和失败）。|  
|[Sql: batchstarting 事件类](../event-classes/sql-batchstarting-event-class.md)， [sql: batchcompleted 事件类](../event-classes/sql-batchcompleted-event-class.md)|提供有关已开始或完成的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 批处理的信息。|  
|[SP: Starting 事件类](../event-classes/sp-starting-event-class.md)， [SP: Completed 事件类](../event-classes/sp-completed-event-class.md)|用于监视 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 存储过程的执行。|  
|[Sql: stmtstarting 事件类](../event-classes/sql-stmtstarting-event-class.md)， [sql: stmtcompleted 事件类](../event-classes/sql-stmtcompleted-event-class.md)|用于监视 CLR 和 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 例程的执行。|  
  
## <a name="performance-counters"></a>性能计数器  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供了对象和计数器，系统监视器可以使用它们监视运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的计算机中的活动。 对象可以是任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源，例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 锁或 Windows 进程。 每个对象有一个或多个计数器，用于确定所要监视对象的各方面信息。 有关详细信息，请参阅 [使用 SQL Server 对象](../performance-monitor/use-sql-server-objects.md)。  
  
|Object|Description|  
|------------|-----------------|  
|[SQL Server - CLR 对象](../performance-monitor/sql-server-clr-object.md)|CLR 执行所花的总时间。|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Windows 系统监视器 (PERFMON.EXE) 计数器  
 Windows 系统监视器 (PERFMON.EXE) 工具具有多个性能计数器，可用来监视 CLR 集成应用程序。 可以通过“sqlservr”进程名称筛选 .NET CLR 性能计数器，以跟踪当前正在运行的 CLR 集成应用程序。  
  
|性能对象|Description|  
|------------------------|-----------------|  
|SqlServer:CLR|提供服务器的 CPU 统计信息。|  
|.NET CLR 异常|跟踪每秒异常数。|  
|.NET CLR 加载|提供有关服务器中加载的 AppDomains 和程序集的信息。|  
|.NET CLR 内存|提供有关 CLR 内存使用量的信息。 如果内存使用量变得过大，则此对象可用于标记警报。|  
|SQL Server 的 .NET 数据访问接口|跟踪每秒的连接数和断开连接数。 此对象可用于监视数据库活动的级别。|  
  
## <a name="catalog-views"></a>目录视图  
 目录视图返回由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库引擎使用的信息。 建议您使用目录视图这一最常用的目录元数据界面，它可为您提供最有效的方法来获取、转换并显示此信息的自定义形式。 所有用户可用的目录元数据都通过目录视图来显示。 有关详细信息，请参阅[目录视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)。  
  
|目录视图|Description|  
|------------------|-----------------|  
|[sys.assemblies &#40;Transact SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)|返回有关在数据库中注册的程序集的信息。|  
|[sys.assembly_references &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)|标识引用其他程序集的程序集。|  
|[sys.assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)|返回有关在程序集中定义的每个函数、存储过程和触发器的信息。|  
|[sys.assembly_files &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)|返回有关在数据库中注册的程序集文件的信息。|  
|[sys.assembly_types &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)|标识由程序集定义的用户定义类型 (UDT)。|  
|[sys.module_assembly_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql)|标识在其中定义 CLR 模块的程序集。|  
|[sys.parameter_type_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)|返回有关属于用户定义类型的参数的信息。|  
|[sys.server_assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)|标识在其中定义 CLR 触发器的程序集。|  
|[sys.server_triggers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)|标识服务器上的服务器级别 DDL 触发器，包括 CLR 触发器。|  
|[sys.type_assembly_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql)|标识在其中定义用户定义类型的程序集。|  
|[sys.types (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)|返回在数据库中注册的系统和用户定义类型。|  
  
## <a name="dynamic-management-views"></a>动态管理视图  
 动态管理视图和函数返回可用于监视服务器实例的运行状况、诊断故障以及优化性能的服务器状态信息。 有关详细信息，请参阅[动态管理视图和函数&#40;TRANSACT-SQL&#41;](../views/views.md)。  
  
|DMV|Description|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)|提供有关服务器中每个应用程序域的信息。|  
|[sys.dm_clr_loaded_assemblies &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql)|标识在服务器上注册的每个托管程序集。|  
|[sys.dm_clr_properties &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql)|返回有关宿主 CLR 的信息。|  
|[sys.dm_clr_tasks &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql)|标识当前正在运行的所有 CLR 任务。|  
|[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)|返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 为加快查询执行而缓存的查询执行计划的信息。|  
|[sys.dm_exec_query_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)|返回缓存查询计划的聚合性能统计信息。|  
|[sys.dm_exec_requests &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql)|返回有关在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中正在执行的每个请求的信息。|  
|[sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)|返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中当前处于活动状态的所有内存分配器，包括 CLR 内存分配器。|  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时 (CLR) 集成编程概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
