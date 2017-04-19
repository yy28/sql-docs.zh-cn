---
title: "SQL Server R Services 的 DMV | Microsoft Docs"
ms.custom: 
ms.date: 11/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f989df1a9948c0bda85a642e5daffa8b319a84ec
ms.lasthandoff: 04/11/2017

---
# <a name="dmvs-for-sql-server-r-services"></a>SQL Server R Services 的 DMV

本主题列出与 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 相关的系统目录视图和 DMV。 


有关扩展事件的详细信息，请参阅 [SQL Server R Services 的扩展事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)。

> [!TIP]
> 产品团队已提供可用于监视 R Services 会话和包的自定义报告。 有关详细信息，请参阅 [Monitor R Services using Custom Reports in Management Studio](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)（在 Management Studio 中使用自定义报告监视 R Services）。
> 

## <a name="system-configuration-and-system-resources"></a>系统配置和系统资源

可以使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 系统目录视图和 DMV 来监视与分析 R 脚本所用的资源。


**常规**
+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  返回用户连接和系统会话的信息。 可以通过查看 *session_id* 列识别系统会话；大于或等于 51 的值表示用户连接，小于 51 的值表示系统进程。 



+ [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  针对服务器使用的每个系统性能计数器返回一行。  可以使用此信息来确定运行了多少个脚本、使用哪种身份验证模式运行了哪些脚本，或者针对整个实例发出了多少次 R 调用。

  此示例只获取与 R 脚本相关的计数器：

  ```
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  此 DMV 针对每个实例的外部脚本报告以下计数器：

  + **执行总数**：本地或远程调用启动的 R 进程数
  + **并行执行数**：脚本包含 @parallel 规范的次数，以及 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 能够生成并使用并行查询计划的次数
  + **流式执行数**：调用流式处理功能的次数。 
  + **SQL CC 执行数**：远程实例化调用并将 SQL Server 用作计算上下文的 R 脚本运行次数 
  + **隐含身份验证登录次数**：使用隐含身份验证进行 ODBC 环回调用（即，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 代表发送脚本请求的用户执行调用）的次数
  + **总执行时间(毫秒)**：从开始调用到完成调用所消耗的时间。
  + **执行错误数**：脚本报告错误的次数。 此计数不包括 R 错误。


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  此 DMV 针对当前正在运行外部脚本的每个辅助角色帐户报告一行。 请注意，此辅助角色帐户不同于发送脚本的用户的凭据。 如果单个 Windows 用户发送多个脚本请求，只会分配一个辅助角色帐户来处理该用户发出的所有请求。 如果不同的 Windows 用户登录以运行外部脚本，将由单独的辅助角色帐户处理该请求。 
  结果当前未执行任何脚本，此 DMV 不会返回任何结果；因此，它最适合用于监视长时间运行的脚本。 返回值如下：
  + **external_script_request_id**：一个 GUID，也用作脚本和中间结果的存储工作目录的临时名称。  
  + **language**：类似于 `R` 的值，表示外部脚本的语言。
  + **degree_of_parallelism**：一个整数，指示已使用的并行进程数。 
  + **external_user_name**：Launchpad 辅助角色帐户，例如 SQLRUser01。 
  

+ [sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  此 DMV 用于内部监视（遥测），可跟踪针对实例发出了多少次 R 调用。 遥测服务将在启动 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 时启动，每次调用特定的 R 函数时会递增基于磁盘的计数器。

  每次调用函数都会递增此计数器。 例如，如果调用且并行运行了 `rxLinMod` ，该计数器会增大 1。
  
  通常情况下，只要生成性能计数器的进程处于活动状态，它们便有效。 因此，对 DMV 的查询不能显示已停止运行的服务的详细数据。 例如，如果 Launchpad 创建了多个并行 R 作业，而这些作业的执行速度很快，然后被 Windows 作业对象清理，那么，DMV 可能不会显示任何数据。
 
  但是，即使实例已关闭，此 DMV 所跟踪的计数器仍会保持运行，并且通过使用写入到磁盘保留 dm_external_script _execution 计数器的状态。
 
 有关 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用的系统性能计数器的详细信息，请参阅 [Use SQL Server Objects](../../relational-databases/performance-monitor/use-sql-server-objects.md)（使用 SQL Server 对象）。

**资源调控器视图**

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  返回有关当前资源池状态、资源池的当前配置以及资源池统计信息的信息。

  > [!IMPORTANT]
  > 
  > 在将其他资源分配给 R Services 之前，必须修改应用到其他服务器服务的资源池。


+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  一个新的目录视图，显示外部资源池的当前配置值。
  在 Enterprise Edition 中，可以配置其他外部资源池：例如，你可能想要以不同于源自远程客户端的作业的方式处理 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中运行的 R 作业的资源。 

  > [!NOTE]
  > 
  > 在 Standard Edition 中，所有 R 作业在同一个外部默认资源池中运行。

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  返回工作负荷组统计信息和工作负荷组的当前配置。 此视图可以与 sys.dm_resource_governor_resource_pools 联接以获取资源池名称。
  对于外部脚本，已添加一个新列用于显示与工作负荷组关联的外部池的 ID。 


+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  一个新的系统目录视图，用于查看关联到特定资源池的处理器和资源。

  对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。

  在默认配置中，工作负荷池自动分配到处理器，因此不会返回关联值。

  关联计划将资源池映射到由给定 ID 标识的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计划。 这些 ID 映射到 sys.dm_os_schedulers (Transact-SQL) 的 scheduler_id 列中的值。


> [!NOTE] 
> 
> 尽管只能在 Enterprise 和 Developer 版本中配置和自定义资源池，但在所有版本中都可以使用默认池和 DMV。 因此，可以在 Standard Edition 中使用这些 DMV 来确定 R 作业的资源上限。 

有关监视 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例的一般信息，请参阅 [Catalog Views](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)（目录视图）和 [Resource Governor Related Dynamic Management Views](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)（与资源调控器相关的动态管理视图）。

## <a name="r-script-execution-and-monitoring"></a>R 脚本执行和监视

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中运行的 R 脚本由 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 接口启动。 但是，Launchpad 的资源不会单独受到调控和监视，因为我们认为它是 Microsoft 提供的、用于适当管理资源的安全服务。

在 Launchpad 服务下运行的单个 R 脚本将使用 [Windows 作业对象](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)进行管理。 使用作业对象可将进程组作为一个单元进行管理。 每个作业对象都是分层的，可控制与其关联的所有进程的属性。 针对某个作业对象执行的操作会影响与该作业对象关联的所有进程。 

因此，如果需要终止与某个对象关联的一个作业，请注意所有相关的进程也会终止。 如果运行一个已分配到 Windows 作业对象的 R 脚本，并且该脚本运行一个必须终止的相关 ODBC 作业，则父 R 脚本进程也会终止。 

如果启动一个使用并行处理的 R 脚本，单个 Windows 作业对象将管理所有并行子进程。

若要确定进程是否在作业中运行，请使用 `IsProcessInJob` 函数。

## <a name="see-also"></a>另请参阅
[管理和监视](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)



