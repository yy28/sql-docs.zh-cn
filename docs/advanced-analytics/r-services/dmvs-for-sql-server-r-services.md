---
title: "用于 SQL Server R Services Dmv | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 用于 SQL Server R Services Dmv

本主题列出系统目录视图和 dmv，用来与相关 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 


有关扩展事件的信息，请参阅 [for SQL Server R Services 的扩展事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)。

> [!TIP]
> 产品团队提供了可用于监视 R Services 会话和包的自定义报表。 有关详细信息请参阅 [监视器 R Services 在 Management Studio 中使用自定义报表](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)。
> 

## <a name="system-configuration-and-system-resources"></a>系统配置和系统资源

你可以监视和分析使用 R 脚本使用的资源 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 系统目录视图和 Dmv。


**常规**
+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  返回用户连接和系统会话的信息。 你可以通过查看标识系统会话 *session_id* 列; 值大于或等于 51 用户连接，并且在系统进程正在 51 低于值。 



+ [sys.dm_os_performance_counters (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  返回的行对于每个服务器使用的系统性能计数器。  你可以使用此信息以查看运行多少脚本，使用哪种身份验证模式，或多少 R 调用发出总体实例上已运行的脚本。

  此示例将获取只与 R 脚本相关的计数器︰

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  此 DMV 的每个实例的外部脚本报告的以下计数器︰

  + **总执行**︰ 通过本地或远程调用启动的 R 进程数
  + **并行执行**︰ 脚本包含次数 @parallel 规范， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 能够生成并使用并行查询计划
  + **流式处理执行**︰ 的流式处理功能已调用的次数。 
  + **SQL CC 执行**︰ 数的 R 脚本运行其中调用实例化远程和 SQL Server 用作计算上下文 
  + **默示身份验证。登录名**︰ 的次数的 ODBC 环回调用已使用默示身份验证; 也就是说， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 执行代表用户通过发送脚本请求调用
  + **总执行时间 （毫秒）**︰ 调用和完成的调用之间经过的时间。
  + **执行错误**︰ 脚本报告的错误次数。 此计数不包括 R 错误。


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  此 DMV 报告当前正在运行的外部脚本的每个工作帐户的单个行。 请注意，此工作帐户发送该脚本的人员的凭据不同。 如果单个 Windows 用户发送多个脚本请求，则只有一个辅助帐户都将分配以处理来自该用户的所有请求。 如果不同的 Windows 用户登录时运行外部脚本，则请求将处理由单独的工作帐户。 
  此 DMV 不返回任何结果如果当前正在不执行任何脚本;因此，它是最适用于监视长时间运行脚本。 它将返回这些值︰
  + **external_script_request_id**︰ 一个 GUID，还可用于存储脚本和中间结果的工作目录的临时名称。  
  + **语言**: 值，如 `R` 表示外部脚本的语言。
  + **degree_of_parallelism**︰ 使用了一个整数，表示并行数的进程。 
  + **external_user_name**: SQLRUser01 之类的快速启动板辅助帐户。 
  

+ [sys.dm_external_script_execution_stats (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  此 DMV 提供内部监视工具 （遥测） 来跟踪多少 R 调用都是在实例上。 遥测服务启动时 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 不，递增每次调用特定的 R 函数的基于磁盘的计数器。

  此计数器在每次调用函数时递增。 例如，如果调用且并行运行了 `rxLinMod` ，该计数器会增大 1。
  
  通常情况下，只要生成性能计数器的进程处于活动状态，它们便有效。 因此，对 DMV 的查询不能显示已停止运行的服务的详细数据。 例如，如果快速启动板创建多个并行的 R 作业，但它们是非常快速地执行并由 Windows 作业对象然后清理，DMV 可能不会显示任何数据。
 
  但是，保持跟踪此 DMV 的计数器正在运行且为 dm_external_script _execution 计数器保留使用写入到磁盘，即使实例已关闭状态。
 
 有关使用系统的性能计数器的详细信息 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，请参阅 [使用 SQL Server 对象](../../relational-databases/performance-monitor/use-sql-server-objects.md)。

**资源调控器视图**

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  返回有关当前资源池状态、资源池的当前配置以及资源池统计信息的信息。

  > [!IMPORTANT]
  > 
  > 你必须修改之前你可以分配给 R Services 的其他资源应用于其他服务器服务的资源池。


+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  显示外部资源池的当前配置值的新目录视图。
  在 Enterprise Edition 中，你可以配置其他外部资源池︰ 例如，你可能决定处理在中运行的 R 作业的资源 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 分开那些源自远程客户端。 

  > [!NOTE]
  > 
  > 在标准版的所有 R 作业都运行相同的外部默认资源池。

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  返回工作负荷组统计信息和工作负荷组的当前配置。 此视图可以与 sys.dm_resource_governor_resource_pools 联接以获取资源池名称。
  外部脚本已显示与工作负荷组关联的外部池 id 已添加新列。 


+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  新的系统目录视图，使你能够查看处理器和关联到特定的资源池的资源。

  对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。

  在默认配置下，工作负载池中自动分配给处理器，因此没有关联的值返回。

  关联计划映射到的资源池 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 由给定 Id 标识的计划。 这些 Id 映射到 sys.dm_os_schedulers (Transact SQL) 中的 scheduler_id 列中的值。


> [!NOTE] 
> 
> 尽管仅在 Enterprise 中提供程序的功能来配置和自定义资源池并且开发人员版、 默认池，以及 Dmv 在所有版本中可用。 因此，可以在标准版中使用这些 Dmv 若要确定 R 作业资源上限。 

有关监视的常规信息 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例，请参阅 [目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) 和 [资源调控器相关的动态管理视图](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="r-script-execution-and-monitoring"></a>R 脚本执行和监视

R 脚本运行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通过启动 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 接口。 但是，快速启动板不控制或分别监视，因为它假定作为由适当管理资源的 Microsoft 提供的安全服务的资源。

在快速启动板服务下运行的各个 R 脚本使用管理 [Windows 作业对象](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)。 作业对象允许要作为一个单元管理的进程的组。 每个作业对象是分层，并控制与之关联的所有进程的属性。 在作业对象上执行的操作会影响与作业对象相关联的所有进程。 

因此，如果你需要终止与对象关联的一个作业，请注意还将终止所有相关的进程中的一种。 如果你正在分配给 Windows 作业对象的 R 脚本并运行该脚本的一个相关的 ODBC 作业，它必须终止，父 R 脚本进程也将被终止。 

如果启动使用并行处理的 R 脚本，单个 Windows 作业对象将管理所有并行子进程。

若要确定在作业中运行的进程，使用 `IsProcessInJob` 函数。

## <a name="see-also"></a>另请参阅
[管理和监视](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

