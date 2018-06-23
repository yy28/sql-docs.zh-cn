---
title: 什么&#39;s SQL Server 2014 中的新增功能 |Microsoft 文档
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 70
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9144eeb653649e36cfed3551e4ec465d403ffdcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018326"
---
# <a name="what39s-new-in-sql-server-2014"></a>什么&#39;s SQL Server 2014 中的新增功能
  本主题总结了中的新增功能的详细的链接[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]，并总结了服务包 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**进行试用：** ![Azure 虚拟机小型](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)有一个 Azure 帐户？  然后转到**[此处](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 到加快具有 SQL Server 2014 Service Pack 1 (SP1) 的虚拟机已安装。 
  
-   [新增功能&#40;数据库引擎&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [什么是 Analysis Services 和 Business Intelligence 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 安装中的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 不具有与以下会引入重要的新功能：**  
  
-   [新增功能&#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新增功能&#40;复制&#41;](../relational-databases/replication/what-s-new-replication.md)  
  
-   [新增功能&#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) 不未引入重要的新功能。
-  [SQL Server 2014 Service Pack 1 发行信息](https://support.microsoft.com/en-us/kb/3058865)。
-  [![下载 Service Pack 1 Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [下载 Microsoft® SQL Server® 2014 Service Pack 1](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 版本信息](https://support.microsoft.com/en-us/kb/3171021)。
-  [![下载 Service Pack 2 Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](http://go.microsoft.com/fwlink/?LinkID=821558) [下载 Microsoft® SQL Server® 2014 Service Pack 2](http://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下载 SQL Server 2014 SP2 功能包](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[下载 SQL Server 2014 SP2 功能包](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2)包括以下改进：

### <a name="performance-and-scalability-improvements"></a>性能和可伸缩性改进 
-   **自动 Soft NUMA 分区：** 与[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]时实例启动期间开启跟踪标志 8079 启用 SP2、 自动 Soft NUMA。 在启动期间，启用跟踪标志 8079 后[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 就询问硬件布局并自动对 Soft NUMA 配置报告每个 NUMA 节点 8 或多个 Cpu 的系统上。 自动的软 NUMA 行为是超线程 （超线程/逻辑处理器），注意。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议第一个测试与自动软 NUMA 性能工作负荷之前在生产环境中打开它。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **动态内存对象缩放：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 动态分区基于的节点和现代硬件上的缩放的内核数的内存对象。 动态升级的目标是进行自动分区为线程安全内存对象 (CMEMTHREAD)，如果它将成为一个瓶颈。 未分区的内存的对象可以动态提升要分区的节点 （NUMA 节点数的分区等于的数量） 和按 CPU （数分区等于分区的内存对象节点按分区可以通过进一步提升Cpu)。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC CHECK MAXDOP 提示\*命令：** 解决了这一改进[connect 反馈 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 你现在可以运行 DBCC CHECKDB 与 sp_configure 值以外的 MAXDOP 设置。 如果 MAXDOP 超出使用资源调控器配置的值，则数据库引擎会使用资源调控器 MAXDOP 值（如 ALTER WORKLOAD GROUP (Transact-SQL) 中所述）。 当使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息，请参阅[DBCC CHECKDB (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **启用 > 缓冲池的 8 TB:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 使 128 TB 的缓冲池使用率的虚拟地址空间。 这一改进使 SQL Server 缓冲池扩展超过 8 TB 在现代硬件上。
-   **SOS_RWLock 旋转锁改善：** SOS_RWLock 是基中的 SQL Server 代码的不同位置中使用一个同步基元。  顾名思义，代码可以拥有多个共享 （读取者） 或单 (writer) 所有权。 这一改进无需为 SOS_RWLock 旋转锁，而是使用类似于内存中 OLTP 的无锁的技术。 进行此更改后，多个线程可以读取由 SOS_RWLock 并行保护，而不阻止相互和从而提供高的可伸缩性的数据结构。 在此更改后之前, 的旋转锁实现允许只有一个线程获取 SOS_RWLock 一次，甚至可以读取的数据结构。  [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空间的本机实现：** 空间查询性能显著提高在中引入[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 通过本机实现。 有关详细信息，请参阅[知识库文章 KB3107399](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支持性和诊断改进
-   **数据库克隆：** 克隆数据库是一个新的 DBCC 命令，增强了现有的生产数据库通过克隆的架构和不含数据的元数据进行故障排除。 使用命令创建克隆`DBCC clonedatabase(‘source_database_name’, ‘clone_database_name’)`。  **注意：** 克隆数据库不应在生产环境中使用。 使用以下命令确定是否已从克隆数据库生成数据库： `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 返回值**1**指示从 clonedatabase 时创建数据库**0**指示它不是克隆。
-   **Tempdb 可支持性：** 服务器启动时存在的一种新的错误日志消息，指示 tempdb 文件数和大小/自动增长的 tempdb 数据文件。
-   **数据库即时文件初始化日志记录：** 一种新的错误日志消息，指示在服务器 statup，数据库即时文件初始化 （启用/禁用） 的状态。
-   **在调用堆栈中的模块名称：** Xevent 调用堆栈现在包含模块名称 + 而不是绝对地址的偏移量。
-   **有关增量统计信息的新 DMF:** 解决了这一改进[connect 反馈 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics)若要启用跟踪在分区级别的增量统计信息。 引入了新的 DMF sys.dm_db_incremental_stats_properties 来公开信息每个分区的增量统计信息。
-   **更新的索引使用情况 DMV 行为：** 解决了这一改进[connect 反馈 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats)从客户将重新生成索引*不*清除 sys.dm_db 从任何现有行条目该索引 _index_usage_stats。 行为现在将与 SQL 2008 和 SQL Server 2016 中的相同。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改进的诊断 XE 和 Dmv 之间的关联：** 解决了这一改进[connect 反馈 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 Query_hash 和 query_plan_hash 用于唯一标识查询。 DMV 将二者定义为 varbinary(8)，而 XEvent 将其定义为 UINT64。 SQL server 不具有"unisigned bigint"，因为不始终能强制转换。 这一改进引入了等效于 query_hash 和 query_plan_hash 的新 XEvent 操作/筛选器列，除非二者定义为有助于关联 XE 和 DMV 之间的查询的 INT64。
-   **支持 utf-8 中大容量插入和 BCP:** 解决了这一改进[connect 反馈 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)中大容量插入和 BCP 现在启用导出和导入的数据编码 utf-8 字符集中的支持。
-   **轻量的每个运算符查询执行分析：** 尽管 showplan 计划中的查询执行计划和成本的运算符上提供大量的信息，但它具有有限的实际的信息进行查询性能故障排除时如 （CPU、 I/O 读取，经过的时间每个线程） 的运行时统计信息。 SQL 2014 SP2 引入了这些其他运行时统计信息每中显示计划，以及 XEvent (query_thread_profile) 以帮助解决查询性能的运算符。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **更改跟踪清除：** 一个新的存储过程`sp_flush_CT_internal_table_on_demand`引入到清理更改按需跟踪内部表。
-   **AlwaysON 租约超时的日志记录**添加新的日志记录功能，使租约超时消息，以便当前时间和预期的续订时间被记录下来。 此外中有关超时 SQL Errorlog 引入了一封新邮件。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **用于检索新 DMF 输入 SQL Server 中的缓冲区：** 用于检索输入的缓冲区，会话/请求 (sys.dm_exec_input_buffer)，那么现在提供新 DMF。 它在功能上等同于 DBCC INPUTBUFFER。 [请参阅有关详细信息博客](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **在留住和会被高估内存授予的缓解措施：** 添加新的查询提示为资源调控器中通过 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT。 这使您能够通过上限设置以防止内存争用其内存授予运行查询时利用这些提示。 有关详细信息，请参阅[知识库文章 KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **更好的内存授予/使用情况诊断：** 新的扩展的事件已添加到的 SQL Server (query_memory_grant_usage) 中的跟踪功能来跟踪列表内存授予请求和授予。 这提供更好地跟踪和分析功能故障排除相关的内存授予的查询执行问题。 有关详细信息，请参阅[知识库文章 KB3107173](https://support.microsoft.com/en-us/kb/3107173)。
-   **查询执行诊断 tempdb 溢出：**-哈希警告和排序警告现在已有其他列来跟踪物理 I/O 统计信息、 使用的内存和受影响的行。 我们还引入了新的 hash_spill_details 扩展的事件。 现在你可以为哈希和排序警告跟踪更详尽信息 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172))。 这一改进现在还通过 XML 查询中的计划为 SpillToTempDbType 复杂类型的新属性的形式公开 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))。 现在显示排序工作表统计信息，请开启统计信息。 实例时都提供 SQL Server 登录名。
-   **改进了涉及残留谓词下推的查询执行计划的诊断：** 读取的实际行现在将报告以帮助改进查询性能故障排除的查询执行计划中。 这应不需要单独捕获 SET STATISTICS IO。 现在允许你查看查询计划中残留谓词下推与相关的信息。 有关详细信息，请参阅[知识库文章 KB3107397](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他信息  
 [SQL Server 2014 资源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](http://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 资源中心](http://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 网站](http://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  