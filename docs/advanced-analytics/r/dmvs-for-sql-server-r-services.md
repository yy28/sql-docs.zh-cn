---
title: "对 SQL Server 机器学习服务 Dmv |Microsoft 文档"
ms.custom: 
ms.date: 07/31/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6846ac36293ae2459c21bc8bd2b99ef144804c8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dmvs-for-sql-server-machine-learning-services"></a>对 SQL Server 机器学习服务的 Dmv

主题列出系统目录视图和 dmv，用来与 SQL Server 中的机器学习相关。

有关扩展事件的信息，请参阅[扩展事件的机器学习](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)。

> [!TIP]
> 产品团队提供的自定义报告可用于监视机器学习会话和包使用率。 有关详细信息，请参阅[监视在 Management Studio 中使用自定义报表的机器学习](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="system-configuration-and-system-resources"></a>系统配置和系统资源

你可以监视和分析通过使用外部脚本的资源[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]系统目录视图和 Dmv。

+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  返回用户连接和系统会话的信息。 可以通过查看 *session_id* 列识别系统会话；大于或等于 51 的值表示用户连接，小于 51 的值表示系统进程。

+ [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  针对服务器使用的每个系统性能计数器返回一行。  可以使用此信息来确定运行了多少个脚本、使用哪种身份验证模式运行了哪些脚本，或者针对整个实例发出了多少次 R 调用。

  此示例只获取与 R 脚本相关的计数器：

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%External Scripts%'
  ```

  此 DMV 针对每个实例的外部脚本报告以下计数器：

  + **总执行**： 通过本地或远程调用启动的外部进程数
  + **并行执行**： 脚本包含次数 _@parallel_ 规范，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]能够生成并使用并行查询计划
  + **流式处理执行**： 的流式处理功能已调用的次数
  + **SQL CC 执行**： 数外部脚本的运行其中调用远程实例化和 SQL Server 已用作计算上下文
  + **隐含身份验证登录次数**：使用隐含身份验证进行 ODBC 环回调用（即，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 代表发送脚本请求的用户执行调用）的次数
  + **总执行时间 （毫秒）**： 调用和完成的调用之间经过的时间
  + **执行错误数**：脚本报告错误的次数。 此计数不包括 R 错误。


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  此 DMV 针对当前正在运行外部脚本的每个辅助角色帐户报告一行。 请注意，此辅助角色帐户不同于发送脚本的用户的凭据。 如果单个 Windows 用户发送多个脚本请求，只会分配一个辅助角色帐户来处理该用户发出的所有请求。 如果不同的 Windows 用户登录以运行外部脚本，将由单独的辅助角色帐户处理该请求。

  结果当前未执行任何脚本，此 DMV 不会返回任何结果；因此，它最适合用于监视长时间运行的脚本。 返回值如下：

  + **external_script_request_id**： 的 GUID，还可用于存储脚本和中间结果的工作目录的临时名称
  + **语言**: 值，如`R`表示外部脚本的语言
  + **degree_of_parallelism**： 使用了一个整数，表示并行数的进程
  + **external_user_name**: 快速启动板辅助帐户，如**SQLRUser01**

+ [sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  此 DMV 提供内部监视工具 （遥测） 来跟踪多少外部脚本调用都是在实例上。 遥测服务启动时[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]不，增加每次调用特定的机器学习函数了一个基于磁盘的计数器。

  此计数器在每次调用特定的跟踪函数时递增。 例如，如果调用且并行运行了 `rxLinMod` ，该计数器会增大 1。
  
  通常情况下，只要生成性能计数器的进程处于活动状态，它们便有效。 因此，对 DMV 的查询不能显示已停止运行的服务的详细数据。 例如，如果 Launchpad 创建了多个并行 R 作业，而这些作业的执行速度很快，然后被 Windows 作业对象清理，那么，DMV 可能不会显示任何数据。
 
  但是，即使实例已关闭，此 DMV 所跟踪的计数器仍会保持运行，并且通过使用写入到磁盘保留 dm_external_script _execution 计数器的状态。
 
 有关 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用的系统性能计数器的详细信息，请参阅 [Use SQL Server Objects](../../relational-databases/performance-monitor/use-sql-server-objects.md)（使用 SQL Server 对象）。

## <a name="resource-governor-views"></a>资源调控器视图

支持资源调控器的版本，在创建 R 或 Python 工作负荷的外部资源池可以 en 有效地跟踪和管理资源。

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
  > 在 Standard Edition 中，外部脚本的所有作业在相同的外部默认资源池内都执行。

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  返回工作负荷组统计信息和工作负荷组的当前配置。 此视图可以与 `sys.dm_resource_governor_resource_pools` 联接以获取资源池名称。
  对于外部脚本，已添加一个新列用于显示与工作负荷组关联的外部池的 ID。

+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  一个新的系统目录视图，用于查看关联到特定资源池的处理器和资源。

  对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。

  在默认配置中，工作负荷池自动分配到处理器，因此不会返回关联值。

  关联计划将资源池映射到由给定 ID 标识的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计划。 这些 Id 映射到中的值`scheduler_id`中的列`sys.dm_os_schedulers`。


> [!NOTE] 
> 
> 尽管只能在 Enterprise 和 Developer 版本中配置和自定义资源池，但在所有版本中都可以使用默认池和 DMV。 因此，可以在标准版中使用这些 Dmv 来确定资源上限为你外部脚本的作业。

有关监视 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例的一般信息，请参阅 [Catalog Views](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)（目录视图）和 [Resource Governor Related Dynamic Management Views](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)（与资源调控器相关的动态管理视图）。

## <a name="monitoring-script-execution"></a>监视脚本执行

在中运行的 R 和 Python 脚本[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通过启动[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]接口。 但是，Launchpad 的资源不会单独受到调控和监视，因为我们认为它是 Microsoft 提供的、用于适当管理资源的安全服务。

在快速启动板服务下运行的单个脚本使用管理[Windows 作业对象](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)。 使用作业对象可将进程组作为一个单元进行管理。 每个作业对象都是分层的，可控制与其关联的所有进程的属性。 针对某个作业对象执行的操作会影响与该作业对象关联的所有进程。

因此，如果需要终止与某个对象关联的一个作业，请注意所有相关的进程也会终止。 如果运行一个已分配到 Windows 作业对象的 R 脚本，并且该脚本运行一个必须终止的相关 ODBC 作业，则父 R 脚本进程也会终止。

如果启动使用并行处理的外部脚本时，单个 Windows 作业对象将管理所有并行子进程。

若要确定进程是否在作业中运行，请使用 `IsProcessInJob` 函数。

## <a name="next-steps"></a>后续步骤

[管理和监视计算机学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

