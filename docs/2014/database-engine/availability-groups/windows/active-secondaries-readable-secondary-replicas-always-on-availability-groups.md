---
title: 活动辅助副本： 可读辅助副本 (Always On 可用性组） |Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 78f3f81a-066a-4fff-b023-7725ff874fdf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b35f34499100e8331f968d6f9297280451885290
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169607"
---
# <a name="active-secondaries-readable-secondary-replicas-always-on-availability-groups"></a>活动次要副本：可读次要副本（AlwaysOn 可用性组）
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 活动辅助功能包括支持对一个或多个次要副本的只读访问（可读次要副本）。 可读辅助副本允许对其所有辅助数据库的只读访问。 但是，可读辅助数据库并非设置为只读。 它们是动态的。 当对相应主数据库的更改应用到某一给定的辅助数据库时，该辅助数据库将更改。 对于典型的辅助副本，包括持久内存优化表，辅助数据库中的数据接近实时。 此外，全文检索与辅助数据库同步。 在许多情况下，主数据库和相应的辅助数据库之间的数据滞后时间只有几秒钟。  
  
 在主数据库中进行的安全设置会对辅助数据库永久保留。 这包括用户、数据库角色和应用程序角色及其各自的权限；如果对主数据库启用了透明数据加密 (TDE)，还将包括 TDE。  
  
> [!NOTE]  
>  尽管您无法将数据写入辅助数据库，但可以在承载辅助副本的服务器实例上写入读写数据库，包括用户数据库和 **tempdb**之类的系统数据库。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 还支持对可读辅助副本（*只读路由*）的读意向连接请求的重新路由。 有关只读路由的信息，请参阅 [Using a Listener to Connect to a Read-Only Secondary Replica (Read-Only Routing)](../../listeners-client-connectivity-application-failover.md#ConnectToSecondary)。  
  
 
  
##  <a name="bkmk_Benefits"></a> 优势  
 指定与可读辅助副本的只读连接具有以下优点：  
  
-   从主副本卸下辅助副本只读工作负荷，以便将资源用于关键任务工作负荷。 如果具有关键任务读工作负荷或不能滞后的工作负荷，应在主副本上运行它。  
  
-   提高承载可读辅助副本的系统的投资回报率。  
  
 此外，可读辅助副本对只读操作提供稳定的支持，如下所示：  
  
-   有关可读辅助数据库的自动临时统计信息可优化对基于磁盘的表的只读查询。 对于内存优化表，将自动创建缺少的统计信息。 但不会自动更新旧统计信息。 您需要手动更新主副本的统计信息。 有关详细信息，请参阅本主题后面的 [只读访问数据库的统计信息](#Read-OnlyStats)。  
  
-   基于磁盘的表的只读工作负荷使用行版本控制来消除辅助数据库上的阻塞争用。 对辅助数据库运行的所有查询都自动映射到快照隔离事务级别，即使在显式设置了其他事务隔离级别时也是如此。 此外，所有锁定提示都将被忽略。 这消除了读取器/编写器的争用。  
  
-   基于持久的内存优化表的只读工作负荷访问数据的方式与主数据库中的访问方式相同，使用具有相同事务隔离级别限制的本机存储过程或 SQL 互操作性。 对主副本运行的报表工作负荷或只读查询可以直接用于辅助副本，无需任何更改。 同样，对辅助副本运行的报表工作负荷或只读查询也可以直接用于主副本，无需任何更改。  与基于磁盘的表相似，对辅助数据库运行的所有查询都自动映射到快照隔离事务级别，即使在显式设置了其他事务隔离级别时也是如此。  
  
-   对于辅助副本上的基于磁盘的表和内存优化表类型，都可以对表变量执行 DML 操作。  
  
##  <a name="bkmk_Prerequisites"></a> 可用性组先决条件  
  
-   **可读辅助副本（必需）**  
  
     数据库管理员需要配置一个或多个副本，这样，在辅助角色下运行时，可允许所有连接（仅针对只读访问）或只允许读意向连接。  
  
    > [!NOTE]  
    >  或者，数据库管理员可以配置任何可用性副本，以便在主角色下运行时排除只读连接。  
  
     有关详细信息，请参阅本主题后面的 [关于对可用性副本的客户端连接访问 (SQL Server)](about-client-connection-access-to-availability-replicas-sql-server.md)之类的系统数据库。  
  
-   **可用性组侦听器**  
  
     为支持只读路由，可用性组必须具备 [可用性组侦听程序](../../listeners-client-connectivity-application-failover.md)。 只读客户端必须将其连接请求定向到此侦听器，并且客户端的连接字符串必须将应用程序意向指定为“只读”。 也就是说，它们必须是 *读意向连接请求*。  
  
-   **只读路由**  
  
     “只读路由” 指的是 SQL Server 将定向到可用性组侦听器的传入的读意向连接请求路由到可用的可读辅助副本的能力。 只读路由的先决条件如下：  
  
    -   为支持只读路由，可读辅助副本需要一个只读路由 URL。 此 URL 仅在本地副本在辅助角色下运行时起作用。 必须根据需要在逐个副本的基础上指定只读路由 URL。 每个只读路由 URL 都用于将读意向请求路由到一个特定的可读辅助副本。 通常，向每个可读辅助副本分配一个只读路由 URL。  
  
    -   要在其作为主副本时支持只读路由的每个可用性副本都要求一个只读路由列表。 一个给定的只读路由列表仅在本地副本在主角色下运行时才起作用。 必须根据需要在逐个副本的基础上指定此列表。 通常，每个只读路由列表中将包含各只读路由 URL，并且在列表的末尾具有本地副本的 URL。  
  
        > [!NOTE]  
        >  读意向连接请求将被路由到当前主副本的只读路由列表上的第一个可用可读辅助副本。 没有负载平衡。  
  
     有关详细信息，请参阅[为可用性组配置只读路由 (SQL Server)](configure-read-only-routing-for-an-availability-group-sql-server.md)。  
  
> [!NOTE]  
>  有关可用性组侦听程序的信息，以及只读路由的详细信息，请参阅 [可用性组侦听程序、客户端连接以及应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)之类的系统数据库。  
  
##  <a name="bkmk_LimitationsRestrictions"></a> 限制和局限  
 不完全支持某些操作，如下所示：  
  
-   当启用可读副本以便读取时，它便开始接收与其辅助数据库的连接。 但是，如果在主数据库上有活动事务，行版本将不会在相应的辅助数据库上完全可用。 必须提交或回滚在配置辅助副本时主副本上存在的所有活动事务。 在此过程完成前，对辅助数据库的事务隔离级别映射将不完整，并且查询被暂时阻塞。  
  
    > [!WARNING]  
    >  运行长时间运行的事务将影响保存的版本控制行数，对于基于磁盘的表和内存优化表都是如此。  
  
-   在具有内存优化表的辅助数据库上，即使始终对内存优化表生成行版本，也会阻塞查询，除非在启用辅助副本以便读取时主副本上的所有活动事务都已完成。 这将确保基于磁盘的表和内存优化表可同时用于报告工作负荷和只读查询。  
  
-   属于可读辅助副本的辅助数据库不支持更改跟踪和变更数据捕获：  
  
    -   在辅助数据库上显式禁用更改跟踪。  
  
    -   可以在辅助数据库上启用变更数据捕获，但不支持这样做。  
  
-   由于读操作会映射到快照隔离事务级别，因此，一个或多个辅助副本上的事务会阻止在主副本上清除虚影记录。 当所有辅助副本都不再需要虚影记录时，虚影记录清除任务将自动清除主副本上基于磁盘的表的虚影记录。  这类似于您在主副本上运行事务时执行的操作。 在辅助数据库上的极端情况下，需要终止正在阻塞虚影清除的长时间运行的读查询。 请注意，如果辅助副本断开连接或数据移动在辅助数据库上挂起，可能阻塞虚影清除。 此状态还会阻止日志截断，因此，如果此状态持续，则我们建议您从可用性组中删除此辅助数据库。 内存优化表没有虚影记录清除问题，因为行版本保存在内存中，独立于主副本上的行版本。  
  
-   如果文件包含辅助副本上仍需要的虚影记录，则主副本上对包含基于磁盘的表的文件的 DBCC SHRINKFILE 操作可能失败。  
  
-   从 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]中开始，甚至在主副本由于用户操作或失败而脱机时可读辅助副本仍可保持联机状态。 但是，只读路由并不在此情况下工作，因为可用性组侦听器也处于脱机状态。 对于只读工作负荷，客户端必须直接连接到只读辅助副本。  
  
> [!NOTE]  
>  如果你在托管可读次要副本的服务器实例上查询 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql) 动态管理视图，则可能会遇到 REDO 阻塞问题。 这是因为此动态管理视图获取指定用户表或视图的 IS 锁，而该锁可能阻止 REDO 线程对该用户表或视图的 X 锁请求。  
  
##  <a name="bkmk_Performance"></a> 性能注意事项  
 此节讨论可读辅助数据库的几个性能注意事项  
  
 
  
###  <a name="DataLatency"></a> 数据滞后时间  
 如果您的只读工作负荷可以容忍一定程度的数据滞后，则实现对辅助副本的只读访问很有用。 在数据滞后不可接受的情况下，请考虑对主副本运行只读工作负荷。  
  
 主副本将主数据库上的更改日志记录发送到辅助副本。 在每个辅助数据库上，专用重做线程应用这些日志记录。 在读访问权限的辅助数据库上，给定的数据更改不显示在查询结果中，直到包含更改的日志记录已应用到辅助数据库并且已在主数据库上提交事务。  
  
 这意味着在主副本和辅助副本之间将会存在一定程度的滞后时间，通常只需几秒钟。 但是，在极少数情况下，例如在网络问题降低了网络吞吐量的情况下，滞后时间可能会较长。 在存在 I/O 瓶颈和数据移动操作处于挂起状态时，将增加滞后时间。 为了监视挂起的数据移动，可以使用 [AlwaysOn 面板](use-the-always-on-dashboard-sql-server-management-studio.md) 或 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql) 动态管理视图。  
  
####  <a name="bkmk_LatencyWithInMemOLTP"></a> 具有内存优化表的数据库上的数据延迟  
 为读取工作负荷访问辅助副本上的内存优化表时， *安全时间戳* 将用于从已于 *安全时间戳*之前提交的事务中返回行。 安全时间戳是垃圾收集线程用于对主副本上的行进行垃圾收集所使用的最早时间戳提示。 此时间戳将在自上次更新起内存优化表上的 DML 事务数超过内部阈值时更新。 每当主副本上最早的事务时间戳更新时，持久的内存优化表上的下一 DML 事务会将此时间戳作为特定日志记录的一部分发送到辅助副本。 辅助副本上的重做线程会在处理此日志记录时更新安全时间戳。  
  
#### <a name="the-impact-of-safe-timestamp-on-latency"></a>安全时间戳对延迟的影响  
  
-   对于事务吞吐量很高的 OLTP 工作负荷，延迟应与基于磁盘的表不相上下。 我们预计这是常见现象。  
  
-   长时间运行事务可能导致安全时间戳随机延迟。  这与访问基于磁盘的表没有什么不同，因为快照隔离的时间戳取决于最早事务的提交时间。  
  
-   自上次更新安全时间戳起，主副本上对事务的更改在下次传输和更新安全时间戳前在辅助副本上不可见。 如果主副本上的事务活动在跨越安全时间戳更新的内部阈值之前停止，则自上次更新安全时间戳起所做的更改在辅助副本上将不可见。 若要缓解此问题，您可能需要在主副本的虚拟持久的内存优化表上运行几个 DML 事务。 您也可以通过运行手动检查点强制传送安全时间戳，但不建议这么做。  
  
#### <a name="monitoring-and-troubleshooting-data-latency-in-memory-optimized-tables"></a>监视内存优化表中的数据延迟并进行故障排除  
 您可以通过在主副本上运行以下查询来查看安全时间戳  
  
```  
  
SELECT MAX(base_generation)   
   AS max_base_generation  
   FROM sys.dm_db_xtp_gc_cycle_stats  
GO  
  
```  
  
 您还可以通过并发运行以下查询和活动的读取工作负荷，查明辅助副本上使用的安全时间戳。  
  
```  
  
SELECT begin_tsn   
   FROM sys.dm_db_xtp_transactions  
GO  
  
```  
  
###  <a name="ReadOnlyWorkloadImpact"></a> 只读工作负荷的影响  
 为辅助副本配置只读访问时，辅助数据库上的只读工作负荷占用来自重做线程的系统资源，如 CPU 和 I/O（对于基于磁盘的表），特别是在基于磁盘的表的只读工作负荷大量占用 I/O 的情况下。 访问内存优化表时没有 IO 影响，因为所有行都驻留在内存中。  
  
 此外，辅助副本上的只读工作负荷还会阻止通过日志记录应用的数据定义语言 (DDL) 发生更改。  
  
-   虽然读取操作由于行版本控制而不会占用共享锁，但这些操作会占用架构稳定性 (Sch-S) 锁，这些锁可能会阻塞正在应用 DDL 更改的重做操作。 DDL 操作包括 ALTER/DROP 表和视图，但不包括存储过程的 DROP 或 ALTER。 因此，如果删除基于磁盘的表或内存优化表，请对主副本执行。 当 REDO 线程处理日志记录以删除表时，必须获取表的 SCH_M 锁，并且必须可通过运行查询访问表阻塞。  对于主副本也是如此，只是删除表是用户会话的一部分，而不是 REDO 线程的一部份。  
  
-   还有其他阻塞内存优化表。 如果辅助副本上存在本机存储过程的并发执行，删除本机存储过程可以导致 REDO 线程阻塞。 对于主副本也是如此，只是删除存储过程是用户会话的一部分，而不是 REDO 线程的一部份。  
  
 应了解与生成查询有关的最佳实践，并且在辅助数据库中应用这些最佳实践。 例如，将需要长时间运行的查询（如数据聚合）安排在低活动期间进行。  
  
> [!NOTE]  
>  如果 REDO 线程被次要副本上的查询阻塞，将引发 **sqlserver.lock_redo_blocked** XEvent。  
  
###  <a name="bkmk_Indexing"></a> 索引  
 若要优化可读辅助副本上的只读工作负荷，您可能需要对辅助数据库中的表创建索引。 因为您无法在辅助数据库上进行架构或数据更改，所以应在主数据库中创建索引，并且允许更改通过重做进程传输到辅助数据库。  
  
 若要监视辅助副本上的索引使用活动，请查询 **sys.dm_db_index_usage_stats**动态管理视图的 **user_seeks**、 **user_scans** 和 [user_lookups](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql) 列。  
  
###  <a name="Read-OnlyStats"></a> 只读访问数据库的统计信息  
 表和索引视图的列的统计信息用于优化查询计划。 对于可用性组，作为应用事务日志记录操作的一部分，在主数据库上创建和维护的统计信息将自动保留在辅助数据库中。 但是，辅助数据库上的只读工作负荷需要的统计信息可能与在主数据库上创建的统计信息不同。 但是，因为辅助数据库被限制为只读访问，所以无法在辅助数据库上创建统计信息。  
  
 为了解决此问题，辅助副本在 **tempdb**中创建和维护辅助数据库的临时统计信息。 将在临时统计信息名称后追加后缀 The suffix _readonly_database_statistic，以便将临时统计信息与主数据库永久保存的永久统计信息加以区分。  
  
 只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以创建和更新临时统计信息。 但是，您可以借助用于永久统计信息的相同工具来删除临时统计信息和监视其属性：  
  
-   使用 [DROP STATISTICS](/sql/t-sql/statements/drop-statistics-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句删除临时统计信息。  
  
-   使用 **sys.stats** 和 **sys.stats_columns** 目录视图监视统计信息。 **sys_stats** 包含一个 **is_temporary**列，用于指示哪些统计信息是永久的，哪些统计信息是临时的。  
  
 不支持自动更新主副本或辅助副本上内存优化表的统计信息。 必须监视辅助副本上的查询性能和计划，在需要时手动更新主副本上的统计信息。 不过，会在主副本和辅助副本上自动创建缺少的统计信息。  
  
 有关 SQL Server 统计信息的详细信息，请参阅 [统计信息](../../../relational-databases/statistics/statistics.md)。  
  

  
####  <a name="StalePermStats"></a> 辅助数据库上陈旧的永久统计信息  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可检测辅助数据库上的永久统计信息的过时时间。 但是，除了通过主数据库进行更改外，不能对永久统计信息进行更改。 为了进行查询优化， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在辅助数据库上为基于磁盘的表创建临时统计信息并使用它们来替代过时的永久统计信息。  
  
 永久统计信息在主数据库上进行更新后，自动将它们永久保存到辅助数据库。 然后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用更新的永久统计信息，该信息比临时统计信息要新。  
  
 如果可用性组进行故障转移，则在所有辅助副本上删除临时统计信息。  
  
####  <a name="StatsLimitationsRestrictions"></a> 限制和局限  
  
-   因为临时统计信息存储于 **tempdb**中，所以重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务将导致所有临时统计信息消失。  
  
-   后缀 suffix _readonly_database_statistic 是为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]生成的统计信息预留的。 在主数据库上创建统计信息时不能使用此后缀。 有关更多信息，请参见 [Statistics](../../../relational-databases/statistics/statistics.md)。  
  
##  <a name="bkmk_AccessInMemTables"></a> 访问辅助副本上的内存优化表  
 辅助副本上的读取工作负荷隔离级别只是主副本上允许的隔离级别。 辅助副本上没有隔离级别映射。 这确保可在主副本上运行的所有报表工作负荷都无需任何更改就可以在辅助副本上运行。 这样，您可以轻松地将报表工作负荷从主副本迁移到辅助副本，或者从辅助副本迁移到主副本（当辅助副本不可用时）。  
  
 以下查询在辅助副本上运行失败的方式与它们在主副本上失败的方式相同。  
  
-   对于仅对内存优化表运行的查询，只支持快照、可重复读和可序列化隔离级别。 除非在数据库级别启用了 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 选项，否则所有具有未提交读或读提交隔离级别的查询都会返回错误。  
  
    ```tsql  
    SET TRANSACTION ISOLATION LEVEL READ_COMMITTED  
    -- This is not allowed  
    BEGIN TRAN  
    SELECT * FROM t_hk  
    COMMIT  
  
    ```  
  
     错误消息：  
  
    ```  
    Msg 41368, Level 16, State 0, Line 2  
    Accessing memory optimized tables using the CREAD_COMMITTED isolation level is supported only for autocommit transactions. It is not supported for explicit or implicit transactions. Provide a supported isolation level for the memory optimized table using a table hing, such as WITH (SNAPSHOT).  
    ```  
  
-   内存优化表不支持锁定提示。 例如，以下所有查询都会因错误失败。 只允许 NOLOCK 提示，用于内存优化表时为 NOOP。  
  
    ```tsql  
    SELECT * FROM t_hk WITH (PAGLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (ROWLOCK)  
    SELECT * FROM t_hk WITH (READPAST)  
    SELECT * FROM t_hk WITH (TABLOCK)  
    SELECT * FROM t_hk WITH (XLOCK)  
    SELECT * FROM t_hk WITH (UPDLOCK)  
    ```  
  
-   对于跨容器事务，不支持会话隔离级别为“快照”的访问内存优化表的事务。 例如，  
  
    ```tsql  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT  
    -- This is not allowed  
    BEGIN TRAN  
       SELECT * FROM t_hk  
    COMMIT  
    ```  
  
     错误消息：  
  
    ```  
    Msg 41332, Level 16, State 0, Line 5  
    Memory optimized tables and natively compiled stored procedures cannot be accessed or created when the session TRANSACTION ISOLATION LEVEL is set to SNAPSHOT.  
    ```  
  
##  <a name="bkmk_CapacityPlanning"></a> 容量规划注意事项  
  
-   对于基于磁盘的表，可读次要副本出于以下两个原因需要占用 **tempdb** 中的空间：  
  
    -   快照隔离级别会将行版本复制到 **tempdb**中。  
  
    -   在 **tempdb**中创建和维护辅助数据库的临时统计信息。 临时统计信息会促使略微增大 **tempdb**的大小。 有关详细信息，请参阅本节后面的 [只读访问数据库的统计信息](#Read-OnlyStats)。  
  
-   在配置对一个或多个辅助副本的读访问时，主数据库将对已删除、修改或插入的数据行添加 14 个字节的系统开销，以便为基于磁盘的表存储指向辅助数据库上的行版本的指针。 这 14 个字节开销将转入辅助数据库。 在向数据行添加 14 个字节的系统开销时，可能会发生页拆分。  
  
     行版本数据不由主数据库生成。 而是辅助数据库生成行版本。 但是，行版本控制在主数据库和辅助数据库中都会增加数据存储。  
  
     行版本数据的增加依赖于主数据库上的快照隔离或读提交快照隔离 (RCSI) 级别设置。 下表介绍可读辅助数据库上基于磁盘的表的不同设置下的版本控制行为。  
  
    |可读辅助副本？|启用了快照隔离或 RCSI 级别隔离？|主数据库|辅助数据库|  
    |---------------------------------|-----------------------------------------------|----------------------|------------------------|  
    |否|否|无行版本或 14 个字节的系统开销|无行版本或 14 个字节的系统开销|  
    |否|用户帐户控制|行版本和 14 个字节的系统开销|无行版本但有 14 个字节的系统开销|  
    |用户帐户控制|否|无行版本但有 14 个字节的系统开销|行版本和 14 个字节的系统开销|  
    |用户帐户控制|用户帐户控制|行版本和 14 个字节的系统开销|行版本和 14 个字节的系统开销|  
  
##  <a name="bkmk_RelatedTasks"></a>相关任务  
  
-   [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [监视可用性组 (Transact-SQL)](monitor-availability-groups-transact-sql.md)  
  
-   [查看可用性副本属性 (SQL Server)](view-availability-replica-properties-sql-server.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [SQL Server AlwaysOn 团队博客： SQL Server AlwaysOn 官方团队博客](http://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [关于对可用性副本的客户端连接访问 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [统计信息](../../../relational-databases/statistics/statistics.md)  
  
  
