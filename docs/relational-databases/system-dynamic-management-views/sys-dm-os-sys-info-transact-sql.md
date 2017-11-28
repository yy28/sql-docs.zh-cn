---
title: "sys.dm_os_sys_info (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: "57"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7cc99a6d0f31d19909d41bde4dcd354d1e045215
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  返回一组有关计算机和有关 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 可用资源及其已占用资源的有用杂项信息。  
  
> **注意：**调用从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_sys_info**。  
  
|列名|数据类型|说明和特定于版本的注释 |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|指定当前的 CPU 时钟周期计数。 CPU 时钟周期数是从处理器的 RDTSC 计数器获得的。 它是一个仅增加的数字。 不可为 Null。|  
|**ms_ticks**|**bigint**|指定自从计算机启动以来的毫秒数。 不可为 Null。|  
|**cpu_count**|**int**|指定系统中的逻辑 CPU 数。 不可为 Null。|  
|**hyperthread_ratio**|**int**|指定一个物理处理器包公开的逻辑内核数与物理内核数的比。 不可为 Null。|  
|**physical_memory_in_bytes**|**bigint**|**适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 。<br /><br /> 指定计算机上的物理内存总量。 不可为 Null。|  
|**physical_memory_kb**|**bigint**|**适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 指定计算机上的物理内存总量。 不可为 Null。|  
|**virtual_memory_in_bytes**|**bigint**|**适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 。<br /><br /> 对用户模式进程可用的虚拟内存的数量。 通过使用 3 GB 开关，可以用它来确定是否 SQL Server 已启动。|  
|**virtual_memory_kb**|**bigint**|**适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 指定对用户模式进程可用的虚拟地址空间的总量。 不可为 Null。|  
|**bpool_commited**|**int**|**适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 。<br /><br /> 表示内存管理器中的已提交内存 (KB)。 不包括内存管理器中的保留内存。 不可为 Null。|  
|**committed_kb**|**int**|**适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 表示内存管理器中的已提交内存 (KB)。 不包括内存管理器中的保留内存。 不可为 Null。|  
|**bpool_commit_target**|**int**|**适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 。<br /><br /> 表示 SQL Server 内存管理器可以占用的内存量 (KB)。|  
|**committed_target_kb**|**int**|**适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 表示 SQL Server 内存管理器可以占用的内存量 (KB)。 使用类似如下的不同输入计算目标量：<br /><br /> -系统包括其负载的当前状态<br /><br /> -请求的当前进程的内存<br /><br /> -计算机上安装的内存量<br /><br /> -配置参数<br /><br /> 如果**committed_target_kb**大于**committed_kb**，内存管理器将尝试获取更多的内存。 如果**committed_target_kb**小于**committed_kb**，内存管理器将尝试收缩的内存提交量。 **Committed_target_kb**始终包括盗取和保留的内存。 不可为 Null。|  
|**bpool_visible**|**int**|**适用于：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 。<br /><br /> 在进程虚拟地址空间中可直接访问的缓冲池中的 8 KB 缓冲区数。 当未使用地址窗口化扩展插件 (AWE)，缓冲区池已获取其内存目标 (bpool_committed = bpool_commit_target) 时，bpool_visible 的值与 bpool_committed 的值相等。当在 32 位版本的 SQL Server 上使用 AWE 时，bpool_visible 表示用于访问由缓冲池区分配的物理内存的 AWE 映射窗口的大小。 此映射窗口的大小由进程地址空间绑定，因此，可见数量将小于提交数量，并且通过为数据库页之外的其他用途而消耗内存的内部组件会进一步减少可见数量。 如果 bpool_visible 的值太低，则可能收到内存不足错误。|  
|**visible_target_kb**|**int**|**适用于：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 等同于**committed_target_kb**。 不可为 Null。|  
|**stack_size_in_bytes**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建的每个线程的调用堆栈的大小。 不可为 Null。|  
|**os_quantum**|**bigint**|表示非抢先任务的量程（以毫秒数度量）。 Quantum （以秒为单位） = **os_quantum** / CPU 时钟速度。 不可为 Null。|  
|**os_error_mode**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的错误模式。 不可为 Null。|  
|**os_priority_class**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的优先级类。 可以为 NULL。<br /><br /> 32 = 正常（错误日志将指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正以正常的优先级基数 (=7) 启动）。<br /><br /> 128 = 高（错误日志将指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正以高优先级基数启动）。  (=13)。）<br /><br /> 有关详细信息，请参阅 [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)。|  
|**max_workers_count**|**int**|表示可以创建的最大工作线程数。 不可为 Null。|  
|**scheduler_count**|**int**|表示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中配置的用户计划程序数。 不可为 Null。|  
|**scheduler_total_count**|**int**|表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的计划程序总数。 不可为 Null。|  
|**deadlock_monitor_serial_number**|**int**|指定当前死锁监视序列的 ID。 不可为 Null。|  
|**sqlserver_start_time_ms_ticks**|**bigint**|表示**ms_tick**数时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上次启动。 与当前 ms_ticks 列进行比较。 不可为 Null。|  
|**sqlserver_start_time**|**datetime**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上次启动时的日期和时间。 不可为 Null。|  
|**affinity_type**|**int**|**适用于： [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** 通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定当前使用中的服务器 CPU 进程关联的类型。 不可为 Null。 有关详细信息，请参阅[ALTER SERVER CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 描述**affinity_type**列。 不可为 Null。<br /><br /> MANUAL = 已为至少一个 CPU 设置关联。<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以自由地在 CPU 之间移动线程。|  
|**process_kernel_time_ms**|**bigint**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过 [！包括 [ssCurrent]**(.../Token/ssCurrent_md.md)]。<br /><br /> 内核模式下所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程所用的总时间（毫秒）。 该值可能会大于单处理器时钟，因为它包括服务器上所有处理器的时间。 不可为 Null。|  
|**process_user_time_ms**|**bigint**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 用户模式下所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程所用的总时间（毫秒）。 该值可能会大于单处理器时钟，因为它包括服务器上所有处理器的时间。 不可为 Null。|  
|**time_source**|**int**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于检索时钟时间的 API。 不可为 Null。<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 描述**time_source**列。 不可为 Null。<br /><br /> QUERY_PERFORMANCE_COUNTER = [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API 检索挂钟时间。<br /><br /> MULTIMEDIA_TIMER =[多媒体计时器](http://go.microsoft.com/fwlink/?LinkId=163094)API 检索挂钟时间。|  
|**virtual_machine_type**|**int**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否正在虚拟环境下运行。  不可为 Null。<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**适用于：[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 描述**virtual_machine_type**列。 不可为 Null。<br /><br /> NONE =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未运行在虚拟机。<br /><br /> HYPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在某一 hypervisor 内运行，这意味着硬件辅助虚拟化。 安装 Hyper_V 角色时，虚拟机监控程序将承载操作系统，因此在主机操作系统上运行的实例将在虚拟机监控程序中运行。<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在某一虚拟机内运行，该虚拟机未采用 Microsoft Virtual PC 之类的硬件助手。|  
|**softnuma_configuration**|**int**|**适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 指定配置方式 NUMA 节点。 不可为 Null。<br /><br /> 0 = OFF 指示硬件默认值<br /><br /> 1 = 自动软件 NUMA<br /><br /> 2 = 通过注册表的手动软件 NUMA|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**适用于：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 。<br /><br /> 关闭 = SOFT-NUMA 功能为关闭<br /><br /> 在自动 = SQL Server 的 SOFT-NUMA 确定 NUMA 节点大小<br /><br /> 手动 = 手动配置的软件 NUMA|
|**process_physical_affinity**|**nvarchar(3072)** |**适用于： 开头[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]** 。<br /><br />做好的信息。 |
|**sql_memory_model**|**int**|**适用于： [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4，且开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1**。<br /><br />指定 SQL Server 用于将内存分配的内存模型。 不可为 Null。<br /><br />1 = 常规内存模型<br />2 = 锁定内存页<br /> 3 = 在内存中的大型页|
|**sql_memory_model_desc**|**nvarchar(120)**|**适用于： [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4，且开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1**。<br /><br />指定 SQL Server 用于将内存分配的内存模型。 不可为 Null。<br /><br />**常规**= SQL Server 使用传统的内存模型分配内存。 如果 SQL Server 服务帐户不具有锁定页中内存的权限在启动期间，这是默认 sql 内存模型。<br />**LOCK_PAGES** = SQL 服务器正在使用在内存中的中锁定页面的分配内存。 当 SQL Server 服务帐户在 SQL Server 启动过程中内存特权拥有锁定页时，这是默认 sql 内存管理器。<br /> **LARGE_PAGES** = SQL Server 正在使用在内存中的大页面分配内存。 SQL Server 使用大型页分配器时 SQL Server 服务帐户拥有内存特权锁定页在服务器启动时以及在开启跟踪标志 834 时将仅有企业版的内存分配。|
|**pdw_node_id**|**int**|**适用于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**<br /><br /> 此分布的节点标识符。|  
|**socket_count** |**int** | **适用于： 开头[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]** 。<br /><br />指定在系统上可用的处理器插槽数。 |  
|**cores_per_socket** |**int** | **适用于： 开头[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。**。<br /><br />指定在系统上的每个可用的插槽的处理器数。 |  
|**numa_node_count** |**int** | **适用于： 开头[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。**。<br /><br />指定在系统上可用的 numa 节点数。 此列包含物理 numa 节点，以及软 numa 节点。 |  
  
## <a name="permissions"></a>Permissions  
 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要`VIEW SERVER STATE`服务器上的权限。  
  
 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 操作系统相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



