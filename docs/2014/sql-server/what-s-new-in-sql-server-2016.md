---
title: SQL Server 2014 中的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
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
ms.openlocfilehash: 23a1392256e103fa1bc112f11b5c5b97f5c398f1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75237706"
---
# <a name="whats-new-in-sql-server-2014"></a>SQL Server 2014 中的新增功能

本主题概述了中[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]的新功能的详细链接，并汇总了的服务包[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**试试看：** ![azure 虚拟机小型](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)虚拟机有一个 azure 帐户？  转到https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2以加速已安装 SQL Server 2014 Service Pack 1 （SP1）的虚拟机。

> [!TIP]
> [单击此处](../2014-toc/index.yml)了解 SQL Server 2014 的 "主页" 文档页。

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>新增功能文章

-   [新增功能 &#40;数据库引擎&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 和 Business Intelligence 中的新增功能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server 安装中的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]尚未引入以下功能的重要新功能：**  
  
-   [新增功能 &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新增功能 &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]（SP1）未引入重要新功能。
-  [SQL Server 2014 Service Pack 1 版本信息](https://support.microsoft.com/kb/3058865)。
-  [下载 Microsoft SQL Server 2014 的 service pack 1，下载 Microsoft SQL Server 2014 的 service pack 1。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [](https://www.microsoft.com/download/details.aspx?id=46694)


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 （SP2）
- [SQL Server 2014 Service Pack 2 版本信息](https://support.microsoft.com/kb/3171021)。
-  [下载适用于 Microsoft SQL Server 2014 的 service pack 2 下载 service pack 2 Microsoft SQL Server 2014。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [](https://go.microsoft.com/fwlink/?LinkID=821558)
-  [下载 SQL Server 2014 sp2 功能包下载 SQL Server 2014 sp2 功能包。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [](https://www.microsoft.com/download/details.aspx?id=53164)

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2包括以下改进：

### <a name="performance-and-scalability-improvements"></a>性能和可伸缩性改进 
-   **自动软 NUMA 分区：** 对于[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2，在实例启动期间启用跟踪标志8079时，会启用自动软 NUMA。 如果在启动期间启用跟踪标志8079， [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 将询问硬件布局，并在报告每个 NUMA 节点8个或更多 cpu 的系统上自动配置软 NUMA。 自动、软 NUMA 行为是超线程（HT/逻辑处理器）感知的。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议先用自动软 NUMA 测试性能工作负荷，然后再在生产环境中对其进行调整。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **动态内存对象缩放：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 根据节点数和核心数动态地将内存对象分区，以在新式硬件上缩放。 动态升级的目标是，如果线程安全内存对象（CMEMTHREAD）成为瓶颈，会自动对其进行分区。 无分区的内存对象可以按节点动态分区（分区数等于 NUMA 节点数）。 按节点分区的内存对象可通过 CPU 进一步分区（分区数等于 Cpu 数）。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC\* CHECK 命令的 MAXDOP 提示：** 此改进解决了[连接反馈（468694）](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 你现在可以使用除 sp_configure 值以外的 MAXDOP 设置运行 DBCC CHECKDB。 如果 MAXDOP 超出使用资源调控器配置的值，则数据库引擎会使用资源调控器 MAXDOP 值（如 ALTER WORKLOAD GROUP (Transact-SQL) 中所述）。 当使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息，请参阅[DBCC CHECKDB （transact-sql）](https://msdn.microsoft.com/library/ms176064.aspx)。
-   为**缓冲池启用 >8 tb：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 为缓冲池使用启用 128 tb 的虚拟地址空间。 此改进使 SQL Server 缓冲池可在新式硬件上扩展到 8 TB 以上。
-   **SOS_RWLock 旋转锁改进：** SOS_RWLock 是在整个 SQL Server 基本代码的不同位置中使用的同步基元。  顾名思义，代码可以具有多个共享（读取器）或单个（写入方）所有权。 此改进不再需要对 SOS_RWLock 的旋转锁，而是使用类似于内存中 OLTP 的无锁技术。 进行此更改后，许多线程可以并行读取受 SOS_RWLock 保护的数据结构，而无需彼此阻止。 这种并行化提高了可伸缩性。 在此更改之前，旋转锁实现一次只允许一个线程获取 SOS_RWLock，甚至读取数据结构。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空间本机实现：** 通过本机实现，在 SP2 中[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]引入了大量的空间查询性能改进。 有关详细信息，请参阅[知识库文章 KB3107399](https://support.microsoft.com/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支持性和诊断改进
-   **数据库克隆：** Clone 数据库是一种新的 DBCC 命令，可通过克隆不包含数据的架构和元数据来增强现有生产数据库的故障。 该克隆是通过命令`DBCC clonedatabase('source_database_name', 'clone_database_name')`创建的。  **注意：** 不应在生产环境中使用克隆的数据库。 使用以下命令确定是否已从克隆的数据库生成数据库： `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 返回值**1**表示数据库是从 clonedatabase 创建的，而**0**表示该数据库不是克隆。
-   **Tempdb 可支持性：** 一个新的错误日志消息，指示在启动时启动 tempdb 文件的数目，以及 tempdb 数据文件的大小和自动增长。
-   **数据库即时文件初始化日志记录：** 新的错误日志消息，指示服务器启动时数据库即时文件初始化（启用/禁用）的状态。
-   **调用堆栈中的模块名称：** 扩展事件（XEvent）调用堆栈现在包含模块名称加上偏移量，而不是绝对地址。
-   **递增统计信息的新 DMF：** 此改进解决了[连接反馈（797156）](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) ，以便能够在分区级别跟踪增量统计信息。 引入了新的 DMF sys.databases dm_db_incremental_stats_properties 来公开每个分区的信息以获取增量统计信息。
-   **索引使用情况 DMV 行为已更新：** 这项改进解决了来自客户的[连接反馈（739566）](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) ，在这种情况下，重新生成索引将*不*会清除来自 sys.databases. dm_db_index_usage_stats 的任何现有行条目。 此行为现在与 SQL 2008 和 SQL Server 2016 相同。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改善了诊断 XE 和 dmv 之间的相关性：** 此改进解决了[连接反馈（1934583）](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 `Query_hash`和`query_plan_hash`用于唯一标识查询。 DMV 将二者定义为 varbinary(8)，而 XEvent 将其定义为 UINT64。 由于 SQL server 不具有 "无符号 bigint"，因此强制转换并不总是有效。 此改进引入了新的 XEvent 操作和筛选列。 列等效于`query_hash`和`query_plan_hash`，只不过它们定义为 INT64。 INT64 定义有助于关联 XE 和 Dmv 之间的查询。
-   **支持 BULK INSERT 和 BCP 中的 utf-8：** 此改进解决了[连接反馈（370419）](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)。 BULK INSERT 和 BCP 现在可以导出或导入以 UTF-8 字符集编码的数据。
-   **每个运算符的查询执行的轻型分析：** 显示计划提供有关计划中每个运算符的成本的信息。 但实际的运行时统计信息对于 CPU、i/o 读取和每个线程的运行时间等因素而言是有限的。 SQL Server 2014 SP2 介绍了显示计划中每个运算符的这些附加运行时统计信息。 R2 还引入了一个名`query_thread_profile`为的 XEvent，以帮助对查询性能进行故障排除。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **更改跟踪清理：** 引入了一个新`sp_flush_CT_internal_table_on_demand`的存储过程，用于根据需要清理更改跟踪内部表。
-   **AlwaysON 租约超时日志记录**添加了新的租约超时消息的日志记录功能，以便记录当前时间和预期的续订时间。 此外，在 SQL 错误日志中引入了与超时有关的新消息。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **用于在 SQL Server 中检索输入缓冲区的新 DMF：** 用于检索会话/请求（sys.databases. dm_exec_input_buffer）输入缓冲区的新 DMF 现在可用。 此 DMF 在功能上等效于 DBCC INPUTBUFFER。 [有关详细信息，请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **对低估和 overestimated 内存授予的缓解措施：** 通过 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT 为 Resource Governor 添加了新的查询提示。 这一新查询允许您在运行查询时通过限制其内存授予来利用这些提示，以防止内存争夺。 有关详细信息，请参阅[知识库文章 KB310740](https://support.microsoft.com/kb/3107401)。
-   **更好的内存授予和使用情况诊断：** 已将名`query_memory_grant_usage`为的新扩展事件添加到 SQL Server 中的跟踪功能的列表中。 此事件跟踪请求和授予的内存授予。 此事件提供更好的跟踪和分析功能，用于排查与内存授予相关的任何查询执行问题。 有关详细信息，请参阅[知识库文章 KB3107173](https://support.microsoft.com/kb/3107173)。
-   **Tempdb 溢出的查询执行诊断：**-哈希警告和排序警告现在具有用于跟踪物理 i/o 统计信息、使用的内存和受影响的行的其他列。 我们还引入了一个新的 hash_spill_details 扩展事件。 现在，你可以跟踪有关哈希和排序警告（[KB3107172](https://support.microsoft.com/kb/3107172)）的更多详细信息。 此改进现在还通过 XML 查询计划以新属性的形式公开给 SpillToTempDbType 复杂类型（[KB3107400](https://support.microsoft.com/kb/3107400)）。 Set statistics `ON`现在显示排序工作表统计信息。
-   **改善了涉及驻留谓词下推的查询执行计划的诊断：** 此时将在查询执行计划中报告读取的实际行，以帮助提高查询性能故障排除。 这些行不必单独捕获 SET STATISTICS IO。 使用这些行，还可以在查询计划中查看与剩余谓词推送有关的信息。 有关详细信息，请参阅[知识库文章 KB3107397](https://support.microsoft.com/kb/3107397)。


## <a name="additional-information"></a>其他信息  
 [SQL Server 2014 资源](../2014-toc/index.yml)  
  
 [SQL Server 2014 发行说明](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 资源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 网站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
