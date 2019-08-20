---
title: SQL Server&#39;2014 中的新增功能 |Microsoft Docs
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
ms.openlocfilehash: f368da503c90595624f476344724719206cdb77c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893699"
---
# <a name="what39s-new-in-sql-server-2014"></a>SQL Server&#39;2014 中的新增功能
  本主题概述了中[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]的新功能的详细链接, 并汇总了的服务包[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**进行试用：** ![Azure 虚拟机小型](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)虚拟机有一个 azure 帐户？  然后转到 **[此处](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 以启动已安装 SQL Server 2014 Service Pack 1 (SP1) 的虚拟机。 
  
-   [新增&#40;功能数据库引擎&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 和商业智能中的新增功能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server 安装中的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]尚未为以下项引入重要的新功能:**  
  
-   [新增&#40;功能 Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新增&#40;功能 Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) 未引入重要新功能。
-  [SQL Server 2014 Service Pack 1 版本信息](https://support.microsoft.com/en-us/kb/3058865)。
-  [![下载适用于 Microsoft？的 Service Pack 1？SQL Server？](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) 2014[下载适用于 Microsoft 的 Service Pack 1？SQL Server？2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 版本信息](https://support.microsoft.com/en-us/kb/3171021)。
-  [![下载适用于 Microsoft 的 Service Pack 2？SQL Server？](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) 2014[下载适用于 Microsoft 的 Service Pack 2？SQL Server？2014](https://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下载 SQL Server 2014 sp2 功能包](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[下载 SQL Server 2014 sp2 功能包](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2包括以下改进:

### <a name="performance-and-scalability-improvements"></a>性能和可伸缩性改进 
-   **自动软 NUMA 分区:** 对于[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, 在实例启动期间启用跟踪标志8079时, 会启用自动软 NUMA。 如果在启动期间启用跟踪标志 8079, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 将询问硬件布局, 并在报告每个 NUMA 节点8个或更多 cpu 的系统上自动配置软 NUMA。 自动、软 NUMA 行为是超线程 (HT/逻辑处理器) 感知的。 通过提高侦听器数、缩放和网络与加密功能，其他节点的分区和创建会缩放后台处理。 建议先使用自动软 NUMA 测试性能工作负荷, 然后再将其投入生产。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **动态内存对象缩放:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 根据节点数和核心数动态地将内存对象分区, 以在新式硬件上缩放。 动态升级的目标是, 如果线程安全内存对象 (CMEMTHREAD) 成为瓶颈, 会自动对其进行分区。 无分区的内存对象可以动态提升为按节点进行分区 (分区数等于 NUMA 节点数), 并且通过节点分区的内存对象可以进一步提升为按 CPU 分区 (分区数等于Cpu)。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC CHECK\*命令的 MAXDOP 提示:** 此改进解决了[连接反馈 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 你现在可以使用 sp_configure 值以外的 MAXDOP 设置运行 DBCC CHECKDB。 如果 MAXDOP 超出使用资源调控器配置的值，则数据库引擎会使用资源调控器 MAXDOP 值（如 ALTER WORKLOAD GROUP (Transact-SQL) 中所述）。 当使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息, 请参阅[DBCC CHECKDB (transact-sql)](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **为缓冲池启用 > 8TB:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 为缓冲池使用启用了128TB 的虚拟地址空间。 此改进使 SQL Server 缓冲池可在新式硬件上扩展到超过8TB。
-   **SOS_RWLock 旋转锁改进:** SOS_RWLock 是在整个 SQL Server 基本代码的不同位置中使用的同步基元。  顾名思义, 代码可以具有多个共享 (读取器) 或单个 (写入方) 所有权。 此改进消除了对 SOS_RWLock 的需求, 并使用类似于内存中 OLTP 的无锁技术。 通过此更改, 许多线程可以并行读取受 SOS_RWLock 保护的数据结构, 而无需彼此阻止, 从而提高了可伸缩性。 在此更改之前, 旋转锁实现一次只允许一个线程获取 SOS_RWLock, 甚至读取数据结构。  [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空间本机实现:** 通过本机实现, 在 SP2 中[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]引入了大量的空间查询性能改进。 有关详细信息, 请参阅[知识库文章 KB3107399](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支持性和诊断改进
-   **数据库克隆:** Clone 数据库是一种新的 DBCC 命令, 可通过克隆不包含数据的架构和元数据来增强现有生产数据库的故障。 该克隆是通过命令`DBCC clonedatabase('source_database_name', 'clone_database_name')`创建的。  **注意：** 克隆的数据库不应用于生产环境。 使用以下命令确定是否已从克隆的数据库生成数据库: `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 返回值**1**表示数据库是从 clonedatabase 创建的, 而**0**表示该数据库不是克隆。
-   **Tempdb 可支持性:** 新的错误日志消息, 指示 tempdb 文件的数目以及服务器启动时存在的 tempdb 数据文件的大小/自动增长。
-   **数据库即时文件初始化日志记录:** 新的错误日志消息, 指示服务器 statup 上的数据库即时文件初始化 (启用/禁用) 的状态。
-   **调用堆栈中的模块名称:** Xevent 调用堆栈现在包含模块名称 + 偏移, 而不是绝对地址。
-   **递增统计信息的新 DMF:** 此改进解决了[连接反馈 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) , 以便能够在分区级别跟踪增量统计信息。 引入了一个新的 DMF sys.databases _db_incremental_stats_properties, 用于为增量统计信息公开每个分区的信息。
-   **索引使用情况 DMV 行为已更新:** 这项改进解决了来自客户的[连接反馈 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) , 在这种情况下, 重新生成索引将*不*会清除 sys.databases _db_index_usage_stats 中的任何现有行条目。 此行为现在与 SQL 2008 和 SQL Server 2016 相同。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改善了诊断 XE 和 Dmv 之间的相关性:** 此改进解决了[连接反馈 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 Query_hash 和 query_plan_hash 用于唯一标识查询。 DMV 将二者定义为 varbinary(8)，而 XEvent 将其定义为 UINT64。 由于 SQL server 不具有 "unisigned bigint", 因此强制转换并不总是有效。 这一改进引入了等效于 query_hash 和 query_plan_hash 的新 XEvent 操作/筛选器列，除非二者定义为有助于关联 XE 和 DMV 之间的查询的 INT64。
-   **支持 BULK INSERT 和 BCP 中的 UTF-8:** 此改进解决了[连接反馈 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) , 其中现在在 BULK INSERT 和 BCP 中启用了对以 utf-8 字符集编码的数据的导出和导入。
-   **轻型按运算符查询执行分析:** 虽然显示计划在查询执行计划和计划中的运算符成本方面提供了大量的信息, 但它对实际运行时统计信息 (例如, CPU、i/o 读取、每个线程的运行时间) 有有限的信息。 SQL 2014 SP2 介绍了显示计划中每个运算符的这些附加运行时统计信息, 并提供了一个 XEvent (query_thread_profile) 来帮助排查查询性能问题。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **更改跟踪清理:** 引入了一个新`sp_flush_CT_internal_table_on_demand`的存储过程, 用于按需清理更改跟踪内部表。
-   **AlwaysON 租约超时日志记录**添加了新的租约超时消息的日志记录功能, 以便记录当前时间和预期的续订时间。 此外, 在 SQL 错误日志中引入了关于超时的新消息。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **用于在 SQL Server 中检索输入缓冲区的新 DMF:** 现提供用于检索会话/请求 (sys.dm_exec_input_buffer) 的输入缓冲区的新 DMF。 它在功能上等同于 DBCC INPUTBUFFER。 [有关详细信息, 请参阅博客](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **对低估和 overestimated 内存授予的缓解措施:** 通过 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT 为 Resource Governor 添加了新的查询提示。 这样一来, 在运行查询时可以通过限制其内存授予来利用这些提示, 以防止内存争夺。 有关详细信息, 请参阅[知识库文章 KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **更好的内存授予/使用诊断:** 新的扩展事件已添加到 SQL Server (query_memory_grant_usage) 中跟踪功能的列表, 用于跟踪请求和授予的内存授予。 这提供了更好的跟踪和分析功能, 用于排查与内存授予相关的查询执行问题。 有关详细信息, 请参阅[知识库文章 KB3107173](https://support.microsoft.com/en-us/kb/3107173)。
-   **针对 tempdb 溢出的查询执行诊断:** -哈希警告和排序警告现在具有用于跟踪物理 i/o 统计信息的其他列、已使用的内存和受影响的行数。 我们还引入了一个新的 hash_spill_details 扩展事件。 现在, 你可以跟踪有关哈希和排序警告 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)) 的更多详细信息。 此改进现在还通过 XML 查询计划以新属性的形式公开给 SpillToTempDbType 复杂类型 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))。 现在, 设置统计信息显示排序工作表统计信息。 .
-   **改善了涉及驻留谓词下推的查询执行计划的诊断:** 此时将在查询执行计划中报告读取的实际行, 以帮助提高查询性能故障排除。 这应该不需要单独捕获 SET STATISTICS IO。 现在, 您可以在查询计划中查看与驻留谓词下推相关的信息。 有关详细信息, 请参阅[知识库文章 KB3107397](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他信息  
 [SQL Server 2014 资源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 资源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 网站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
