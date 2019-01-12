---
title: 什么&#39;SQL Server 2014 中的 s |Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 57acb73332f90f4084243184f480edf0a1395a7b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124817"
---
# <a name="what39s-new-in-sql-server-2014"></a>什么&#39;SQL Server 2014 中的 s
  本主题总结了中的新增功能的详细的链接[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]，并总结了服务包 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**进行试用：**![Azure 虚拟机小](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)有一个 Azure 帐户？  然后转**[此处](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 启动具有 SQL Server 2014 Service Pack 1 (SP1) 的虚拟机已安装。 
  
-   [新增功能&#40;数据库引擎&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [什么是 Analysis Services 和 Business Intelligence 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 安装中的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 不到以下引入重大的新功能：**  
  
-   [新增功能&#40;集成服务&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新增功能&#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) 未引入重大的新功能。
-  [SQL Server 2014 Service Pack 1 发布信息](https://support.microsoft.com/en-us/kb/3058865)。
-  [![下载 Service Pack 1 Microsoft??SQL Server??2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [下载 Service Pack 1 的 Microsoft??SQL Server??2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 版本信息](https://support.microsoft.com/en-us/kb/3171021)。
-  [![下载 Service Pack 2 的 Microsoft??SQL Server??2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [下载 Service Pack 2 的 Microsoft??SQL Server??2014](https://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下载 SQL Server 2014 SP2 功能包](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[下载 SQL Server 2014 SP2 功能包](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2)包括以下改进：

### <a name="performance-and-scalability-improvements"></a>性能和可伸缩性改进 
-   **自动 Soft NUMA 分区：** 使用[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]实例启动期间启用跟踪标志 8079,sql 时启用 SP2、 自动 Soft NUMA。 在启动期间，启用跟踪标志 8079 后[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 会询问硬件布局和报告每个 NUMA 节点 8 或更多 Cpu 的系统上自动配置 Soft NUMA。 自动的软 NUMA 行为是超线程 （HT/逻辑处理器） 感知。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议首先测试自动 Soft NUMA 性能工作负荷前将其设为在生产环境中。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **动态内存对象缩放：**[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 动态分区内存对象基于数量的节点和核心以缩放现代硬件上。 动态升级旨在自动分区的线程安全内存对象 (CMEMTHREAD) 成为瓶颈。 未分区内存对象可以动态升级，以便按节点 （数 NUMA 节点数的分区等于）、 分区和内存对象按节点分区可以通过进一步提升 CPU （分区等号的数量进行分区Cpu)。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC CHECK 的 MAXDOP 提示\*命令：** 这项改进解决[connect 反馈 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 你现在可以运行 DBCC CHECKDB 的 sp_configure 值之外的 MAXDOP 设置。 如果 MAXDOP 超出使用资源调控器配置的值，则数据库引擎会使用资源调控器 MAXDOP 值（如 ALTER WORKLOAD GROUP (Transact-SQL) 中所述）。 当使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息，请参阅[DBCC CHECKDB (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **启用 > 8 TB，缓冲池：**[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 支持 128 TB 的缓冲池使用率的虚拟地址空间。 此改进使 SQL Server 缓冲池以缩放 8 TB 以上现代硬件上。
-   **SOS_RWLock 旋转锁改进：** SOS_RWLock 是在 SQL 服务器的基本代码的各个位置中使用的同步基元。  顾名思义，代码可以有多个共享 （读取器） 或单 （编写器） 的所有权。 这一改进无需 SOS_RWLock 旋转锁，而是使用类似于内存中 OLTP 的无锁定技术。 进行此更改后，多个线程可以读取由 SOS_RWLock 并行保护，而无需相互阻止和从而提供增强的可伸缩性的数据结构。 在此更改前旋转锁实现允许只有一个线程获取 SOS_RWLock 一次，甚至还可以读取的数据结构。  [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空间本机实现：** 中引入的空间查询性能得到显著提高[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 到本机实现。 有关详细信息，请参阅[知识库文章 KB3107399](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支持性和诊断改进
-   **克隆数据库：** 克隆数据库是一个新的 DBCC 命令，增强了对现有生产数据库克隆架构和不含数据的元数据进行故障排除。 使用命令创建克隆`DBCC clonedatabase('source_database_name', 'clone_database_name')`。  注意：克隆的数据库不应用于生产环境。 使用以下命令确定是否已从克隆数据库生成一个数据库： `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 返回值**1**指示数据库创建时的 clonedatabase **0**指示它不是克隆。
-   **Tempdb 可支持性：** 新的错误日志消息，指明 tempdb 文件的数目和大小/tempdb 数据文件在服务器启动时存在的自动增长。
-   **数据库即时文件初始化日志记录：** 新的错误日志消息，指明服务器 statup，数据库即时文件初始化 （启用/禁用） 的状态上。
-   **在调用堆栈中的模块名称：** Xevent 调用堆栈现包含模块名称 + 而不是绝对地址的偏移量。
-   **有关增量统计信息的新 DMF:** 这项改进解决[connect 反馈 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics)若要启用跟踪的增量统计信息的分区级别。 引入了新的 DMF sys.dm_db_incremental_stats_properties 公开信息每个分区的增量统计信息。
-   **索引使用 DMV 更新行为：** 这项改进解决[connect 反馈 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats)的客户将重新生成索引*不*清除从 sys.dm_db_index_usage_stats 该索引的任何现有行项。 行为现在将与 SQL 2008 和 SQL Server 2016 中的相同。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改进了 XE 和 Dmv 诊断之间的相关性：** 这项改进解决[connect 反馈 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 仅 Query_hash 和 query_plan_hash 用于标识查询。 DMV 将二者定义为 varbinary(8)，而 XEvent 将其定义为 UINT64。 由于 SQL server 不具有"unisigned bigint"，则强制转换不并非始终有效。 这一改进引入了等效于 query_hash 和 query_plan_hash 的新 XEvent 操作/筛选器列，除非二者定义为有助于关联 XE 和 DMV 之间的查询的 INT64。
-   **对 utf-8 BULK INSERT 和 BCP 中的支持：** 这项改进解决[connect 反馈 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) BULK INSERT 和 BCP 中现在启用支持导出和导入以 utf-8 字符集编码的数据。
-   **轻型按运算符查询执行分析：** 尽管显示计划提供了很多信息的查询执行计划和运算符的成本在计划中，但它具有有限的实际信息进行故障排除查询性能，而运行时统计信息，如 (CPU、 I/O 读取，占用时间每个线程)。 SQL 2014 SP2 引入了每个运算符对显示计划，以及一个 XEvent (query_thread_profile) 来帮助排除查询性能中这些额外的运行时统计信息。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **更改跟踪清除：** 一个新的存储过程`sp_flush_CT_internal_table_on_demand`清除更改跟踪内部表按需引入。
-   **AlwaysON 租约超时的日志记录**添加租约超时消息的新日志记录功能，以便记录当前时间和预期的续订时间。 此外有关超时 SQL Errorlog 中引入了新的消息。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **用于检索 SQL Server 中的输入的缓冲区的新 DMF:** 现提供用于检索会话/请求 (sys.dm_exec_input_buffer) 的输入缓冲区的新 DMF。 它在功能上等同于 DBCC INPUTBUFFER。 [请参阅博客获取详细信息的](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **在留住和会被高估内存授予的缓解措施：** 添加了新的查询提示为资源调控器中通过 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT。 这可以通过防止内存争用内存授予上限运行查询时利用这些提示。 有关详细信息，请参阅[知识库文章 KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **更好的内存授予/使用诊断：** 新的扩展的事件已添加到 SQL Server (query_memory_grant_usage) 中的跟踪功能来跟踪内存授予请求和授予的列表。 这提供更好地跟踪和分析功能以进行故障排除与内存授予的查询执行问题。 有关详细信息，请参阅[知识库文章 KB3107173](https://support.microsoft.com/en-us/kb/3107173)。
-   **Tempdb 溢出的查询执行诊断：**-哈希警告和排序警告现在具有其他列来跟踪物理 I/O 统计信息、 使用的内存和受影响的行。 我们还引入了新的 hash_spill_details 扩展的事件。 现在，你可以跟踪更详尽的信息的哈希和排序警告 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172))。 此改进现在还通过 XML 查询计划为 SpillToTempDbType 复杂类型的新属性的形式公开 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))。 设置统计信息现在显示了对工作表的统计信息进行排序。 .
-   **对于涉及残留谓词下推的查询执行计划的改进了的诊断：** 读取的实际行现在将在查询执行计划，以帮助改进查询性能故障排除报告。 这应抵消单独捕获 SET STATISTICS IO 的需求。 现在可以看到查询计划中残留谓词下推到相关的信息。 有关详细信息，请参阅[知识库文章 KB3107397](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他信息  
 [SQL Server 2014 资源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 资源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 网站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
