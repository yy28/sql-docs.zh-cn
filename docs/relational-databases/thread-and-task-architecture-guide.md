---
title: 线程和任务体系结构指南 | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: pmasl
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c19e3ad3589cad6f7503ff9f0e92c090bef5035
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "72305196"
---
# <a name="thread-and-task-architecture-guide"></a>线程和任务体系结构指南
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="operating-system-task-scheduling"></a>操作系统任务计划
线程是操作系统可以执行的最小处理单位，借助线程可以将应用程序逻辑分为多个并行执行路径。 当复杂应用程序包含可同时执行的多个任务时，线程非常有用。 

操作系统执行应用程序实例时，它将创建一个单元（称为进程）来管理该实例。 此进程包含一个执行线程。 它是由应用程序代码执行的一系列编程指令。 例如，如果一个简单应用程序具有一组可串行执行的指令，则会将该组指令作为单个任务处理，并且整个应用程序只有一个执行路径（或线程）。   更复杂的应用程序可能有几个任务，这些任务可以并行执行，而不是串行执行。  应用程序可以通过以下方式实现此操作：启动各个任务的独立进程（这属于资源密集型操作），或启动独立的线程（相对而言它消耗资源较少）。 而且，可以独立于与某进程关联的其他线程来安排每个线程的执行。

线程使复杂的应用程序能够更有效地利用处理器 (CPU)，即使在只有一个 CPU 的计算机上也是如此。 如果只有一个 CPU，则每次只能执行一个线程。 如果一个线程执行不使用 CPU 的长时间运行的操作（如磁盘读/写操作），则第一个操作完成之前可以执行另一个线程。 通过在其他线程等待操作完成的同时执行线程，应用程序可以最大限度地利用 CPU。 对于大量占用磁盘 I/O 的多用户应用程序（如数据库服务器），这尤其有效。 具有多个 CPU 的计算机可以同时在每个 CPU 上执行一个线程。 例如，如果某计算机有八个 CPU，则它可以同时执行八个线程。

## <a name="sql-server-task-scheduling"></a>SQL Server 任务计划
在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的作用域中，请求是查询或批处理的逻辑表示形式。  请求还表示系统线程所需的操作，如检查点或日志编写器。 请求在其整个生存期期间以不同状态存在，并且在执行请求所需的资源不可用时请求可以累积等待，如[锁](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md#locks)或[闩锁](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md#latches)。 有关请求状态的详细信息，请参阅 [sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。

任务表示满足请求所需完成的工作单元。  可以向单个请求分配一个或多个任务。 并行请求有多个并行执行（而非串行）的活动任务。 在任何给定的时间点，串行执行的请求均仅有一个活动任务。 任务在其整个生存期期间以不同状态存在。 有关任务状态的详细信息，请参阅 [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)。 处于“挂起”状态的任务正在等待执行任务所需的资源可用。 有关正在等待的任务的详细信息，请参阅 [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作线程（又称为工作器或线程）是操作系统线程的逻辑表现形式。  执行串行请求时，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 将生成线程，以执行活动任务。 在[行模式](../relational-databases/query-processing-architecture-guide.md#execution-modes)下执行并行请求时，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 将分配线程，来协调负责完成已向其分配的任务的子线程。 为每个任务生成的工作线程数取决于以下因素：
-   请求是否符合并行要求（由查询优化器确定）。
-   根据当前负载，系统的实际可用的[并行度 (DOP)](../relational-databases/query-processing-architecture-guide.md#DOP) 是多少。 它可能不同于估计的 DOP，后者基于最大并行度 (MAXDOP) 的服务器配置。 例如，MAXDOP 的服务器配置可能是 8，但在运行时可用的 DOP 可能仅为 2，这样则会影响查询性能。 

> [!NOTE]
> 将按任务设置最大并行度 (MAXDOP) 限制，而非按请求限制  。 这意味着，在并行查询执行期间，单个请求可以生成多个任务，并且每个任务可以使用多个工作线程（数目最多达 MAXDOP 限制）。 有关 MAXDOP 的详细信息，请参阅[配置最大并行度服务器配置选项](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。

计划程序（又称为 SOS 计划程序）管理需要处理时间来代表任务执行工作的工作线程。  每个计划程序映射单个处理器 (CPU)。 线程可以在计划程序内活动的时间称为 OS 量程，最长为 4 毫秒。 量程时间到期后，线程将其时间转让给需要访问 CPU 资源的其他线程，并更改自己的状态。 用于将 CPU 资源访问最大化的线程之间的协作称为“协作计划”（又称为非抢先计划）  。 反之，线程状态更改会传播到与该线程关联的任务，并会传播到与相应任务关联的请求。 有关线程状态的详细信息，请参阅 [sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。 有关计划程序的详细信息，请参阅 [sys.dm_os_schedulers](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。 

### <a name="allocating-threads-to-a-cpu"></a>为 CPU 分配线程
默认情况下，每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例启动每个线程，操作系统根据负载从计算机上的处理器 (CPU) 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例分发线程。 如果已在操作系统级别启用了进程关联，则操作系统会将每个线程分配给特定的 CPU。 与之相反，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工作线程分配给在 CPU 之间平均分发线程的计划程序。  
    
为了执行多任务处理，例如当多个应用程序访问同一组 CPU 时，操作系统有时会在不同 CPU 之间移动工作线程。 虽然从操作系统方面而言，这种活动是高效的，但是在高系统负荷的情况下，该活动会降低 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的性能，因为每个处理器缓存都会不断地重新加载数据。 如果将各个 CPU 分配给特定线程，则通过消除处理器的重新加载需要以及减少 CPU 之间的线程迁移（因而减少上下文切换），可以提高在这些条件下的性能；线程与处理器之间的这种关联称为“处理器关联”。 如果已经启用了关联，则操作系统会将每个线程分配给一个特定的 CPU。 

[关联掩码选项](../database-engine/configure-windows/affinity-mask-server-configuration-option.md)通过使用 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 进行设置。 如果未设置关联掩码，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例会在未应用掩码的计划程序之间平均分配工作线程。

> [!CAUTION]
> 请勿在操作系统中配置 CPU 关联后，还在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中配置关联掩码。 这些设置实现的效果相同，如果配置不一致，则可能会得到意外的结果。 有关详细信息，请参阅[关联掩码选项](../database-engine/configure-windows/affinity-mask-server-configuration-option.md)。

当服务器上连接有大量客户端时，线程池有助于优化性能。 一般情况下，会为每个查询请求创建一个单独的操作系统线程。 但是，当到服务器的连接达到数以百计时，为每个查询请求使用一个线程会占用大量的系统资源。 [最大工作线程数选项](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)使 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以为更大数量的查询请求创建一个工作线程池，从而提高性能。 

### <a name="using-the-lightweight-pooling-option"></a>使用 lightweight pooling 选项
切换线程上下文的开销可能不是很大。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的大多数实例不会发现轻型池选项设置为 0 或 1 时性能有何差别。 只有运行在具有下列特征的计算机上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例可能从[轻型池](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)受益：    
* 大型多 CPU 服务器
* 所有 CPU 都以接近最大容量运行
* 存在高级别的上下文切换

如果将轻型池的值设为 1，则可能会略微提高这些系统的性能。

> [!IMPORTANT]
> 请勿使用纤程模式计划日常操作。 这会抑制上下文切换优点的正常发挥，从而降低性能，因为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的某些组件在纤程模式下不能正常工作。 有关详细信息，请参阅[轻型池](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。

## <a name="thread-and-fiber-execution"></a>线程和纤程的执行
Microsoft Windows 使用从 1 到 31 的数值优先级系统计划线程的执行优先级。 零是保留值，专供操作系统使用。 当有多个线程等待执行时，Windows 将分派优先级最高的线程。

默认情况下，每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的优先级都是 7，这个优先级称为正常优先级。 此默认值为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 线程提供了足够高的优先级以获得足够的 CPU 资源，而不会对其他应用程序造成负面影响。 

[优先级提升](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)配置选项可用于将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的线程优先级提高到 13。 此优先级称为高优先级。 此设置为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 线程提供了一个比其他大多数应用程序高的优先级。 因此，通常当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 线程准备好运行时便获得分派，而不会被其他应用程序的线程抢先。 这可以在服务器只运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例而未运行其他应用程序时提高性能。 但是，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中发生占用大量内存的操作，其他应用程序便不可能有足够高的优先级而抢先于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 线程。 

如果在一台计算机上运行多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，而只为其中的某些实例打开了 priority boost 选项，那么任何以正常优先级运行的实例的性能都将受到负面影响。 而且，如果打开了优先级提升选项，服务器上的其他应用程序和组件的性能将会降低。 因此，必须在严格控制下使用此选项。

## <a name="hot-add-cpu"></a>热添加 CPU
热添加 CPU 是指能够动态向运行中的系统添加 CPU。 添加 CPU 时，可以通过添加新硬件来进行物理添加，或者通过联机硬件分区进行逻辑添加，或者通过虚拟化层进行虚拟添加。 从 [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] 开始，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持热添加 CPU。

热添加 CPU 的要求：  
* 要求使用支持热添加 CPU 的硬件。
* 要求使用 Windows Server 2008 Datacenter 的 64 位版本或 Windows Server 2008 Enterprise Edition for Itanium-Based Systems 操作系统。
* 要求具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise。
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 无法配置为使用软 NUMA。 有关软 NUMA 的详细信息，请参阅 [Soft-NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md)。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不会在添加 CPU 后自动开始使用它们。 这可以防止 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用可能是为其他用途而添加的 CPU。 添加 CPU 后，请执行 [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) 语句以便 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将新 CPU 识别为可用资源。

> [!NOTE]
> 如果配置了 [affinity64 掩码](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) ，则必须修改 affinity64 掩码以使用新 CPU。
 
## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>在具有超过 64 个 CPU 的计算机上运行 SQL Server 的最佳做法

### <a name="assigning-hardware-threads-with-cpus"></a>给硬件线程分配 CPU
不要使用 affinity mask 和 affinity64 mask 服务器配置选项来将处理器绑定到特定线程。 这些选项限制为 64 个 CPU。 请改用 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 的 `SET PROCESS AFFINITY` 选项。

### <a name="managing-the-transaction-log-file-size"></a>管理事务日志文件大小
不要依赖于自动增长来增加事务日志文件的大小。 增加事务日志必须是一个串行的过程。 扩展日志可能会阻止事务继续写操作，直到完成日志扩展。 请通过将文件大小设置为足够支持环境中典型工作负荷的值来预分配日志文件的空间。

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>设置索引操作的最大并行度
可以通过暂时将数据库的恢复模式设置为大容量日志恢复模式或简单恢复模式，以在具有许多 CPU 的计算机上改进索引操作（如创建或重新创建索引）的性能。 这些索引操作可以导致重大的日志活动和日志争用，从而影响 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所做的最佳并行度 (DOP) 选择。

除调整最大并行度 (MAXDOP) 服务器配置选项以外，请考虑使用 [MAXDOP 选项](../t-sql/statements/alter-index-transact-sql.md)调整索引操作的并行度  。 有关详细信息，请参阅 [配置并行索引操作](../relational-databases/indexes/configure-parallel-index-operations.md)。 有关调整最大并行度服务器配置选项的详细信息和指南，请参阅[配置最大并行度服务器配置选项](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。

### <a name="setting-the-maximum-number-of-worker-threads"></a>设置最大工作线程数
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将在启动时动态配置最大工作线程数服务器配置选项。  在启动时，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用可用 CPU 数和系统体系结构通过经过证实的[公式](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md#Recommendations)确定此服务器配置。

此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 SQL Server 专业人员更改。 如果怀疑存在性能问题，可能不是由于工作线程不可用。 很有可能是导致工作线程等待的因素造成的，例如 I/O。 在更改最大工作线程设置之前，最好找到导致性能问题的根本原因。 但是，如果需要手动设置最大工作线程数，必须始终将此配置值设置为至少为系统上存在的 CPU 数的七倍的值。 有关详细信息，请参阅[配置最大工作线程数](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)。

### <a name="using-sql-trace-and-sql-server-profiler"></a>使用 SQL 跟踪和 SQL Server Profiler
不建议在生产环境中使用 SQL 跟踪和 SQL Profiler。 运行这些工具的系统开销也会随着 CPU 的数目的增加而增加。 如果您必须在生产环境中使用 SQL 跟踪，请将跟踪事件的数目限制为最少。 请在负荷下仔细探查和测试每个跟踪事件，并且避免使用显著影响性能的事件组合。

> [!IMPORTANT]
> 已弃用 SQL 跟踪和 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]。 包含 Microsoft SQL Server 跟踪和重播对象的“Microsoft.SqlServer.Management.Trace”命名空间也已遭弃用  。 
> [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 
> 请改用扩展事件。 有关[扩展事件](../relational-databases/extended-events/extended-events.md)的详细信息，请参阅[快速入门：SQL Server 中的扩展事件](../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)和 [SSMS XEvent 探查器](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。

> [!NOTE]
> 针对 Analysis Services 工作负荷的 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 尚未弃用，我们将继续提供支持。

### <a name="setting-the-number-of-tempdb-data-files"></a>设置 TempDB 数据文件的数目
文件数取决于计算机上的（逻辑）处理器数。 一般而言，如果逻辑处理器数目小于或等于 8，则使用的数据文件数与逻辑处理器数相同。 如果逻辑处理器数目大于 8，则使用 8 个数据文件，如果仍然存在争用，则以 4 的倍数增加数据文件的数量，直到争用减少到可接受的级别或对工作负荷/代码进行更改。 另外，请注意其他 TempDB 建议，可从[在 SQL Server 中优化 TempDB 性能](../relational-databases/databases/tempdb-database.md#optimizing-tempdb-performance-in-sql-server)查看它们。 

但是，通过仔细考虑 tempdb 的并发需要，可以减少数据库管理开销。 例如，如果一个系统具有 64 个 CPU 并且通常只有 32 个查询使用 tempdb，则将 tempdb 文件的数目增加到 64 将不会提高性能。

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>可以使用超过 64 个 CPU 的 SQL Server 组件
下表列出了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件，并指示它们是否可以使用超过 64 个 CPU。

|进程名称   |可执行程序 |是否可使用超过 64 个 CPU |  
|----------|----------|----------|  
|SQL Server 数据库引擎 |Sqlserver.exe  |是 |  
|Reporting Services |Rs.exe |否 |  
|Analysis Services  |As.exe |否 |  
|Integration Services   |Is.exe |否 |  
|Service Broker |Sb.exe |否 |  
|全文搜索   |Fts.exe    |否 |  
|SQL Server 代理   |Sqlagent.exe   |否 |  
|SQL Server Management Studio   |Ssms.exe   |否 |  
|SQL Server 安装程序   |Setup.exe  |否 |  
