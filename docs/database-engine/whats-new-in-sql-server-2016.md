---
title: 数据库引擎中的新增功能 - SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
caps.latest.revision: 431
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Active
ms.openlocfilehash: 329ddc437d53421f93fb4c18c0b4f138ebdbd5e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>数据库引擎中的新增功能 - SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

本主题总结了 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]版本中引入的增强功能。  这些新功能和增强功能，这些功能可以提高设计、开发和维护数据存储系统的架构师、开发人员和管理员的能力和工作效率。

若要查看其他 SQL Server 组件的新增功能，请参阅 [SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)。

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 是 64 位应用程序。 32 位安装已停止使用，不过，某些元素仍以 32 位组件运行。

#### <a name="try-it-out"></a>进行试用

- 若要下载 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，请转到[评估中心](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)![下载](../analysis-services/media/download.png "下载")。

- 已经拥有 Azure 帐户？  然后转到 **[此处](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** ，以加速已安装有 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的虚拟机。

> [!NOTE]
> 有关最新发行说明，请参阅 [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)。
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  `CREATE OR ALTER <object>` 语法现可用于[过程](../t-sql/statements/create-procedure-transact-sql.md)、[视图](../t-sql/statements/create-view-transact-sql.md)[函数](../t-sql/statements/create-function-transact-sql.md)和[触发器](../t-sql/statements/create-trigger-transact-sql.md)。
-   已添加对更具一般性的查询提示模型的支持：`OPTION (USE HINT('<hint1>', '<hint2>'))`。 有关详细信息，请参阅 [查询提示 (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md)。  
- [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) DMV 已添加到列表提示。  
- 已添加 [Sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) DMV 以返回显示计划 XML 临时统计信息。  
- [Sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) DMV 已添加到指定表的增量统计信息。  
- `instant_file_initialization_enabled` 列已添加到 [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)。  
- `estimated_read_row_count` 列已添加到 [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)。  
-  `sql_memory_model` 和 `sql_memory_model_desc` 列已添加到 [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 以提供有关内存页的锁定模型的信息。
-  扩展了支持大量功能的版本。 这包括向所有版本增添了行级安全性、Always Encrypted、动态数据屏蔽、数据库审核、内存中 OLTP 和多个其他功能。 有关详细信息，请参阅 [SQL Server 2016 的各版本和支持的功能](../sql-server/editions-and-supported-features-for-sql-server-2016.md)。   
-  重新定义使用 Always On 进行加密的对象时，[sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 允许 Always On 加密更新元数据。  


##  <a name="Feature"></a> SQL Server 2016 RTM
本节包含以下小节：

-   [列存储索引](#columnstore)
-   [数据库作用域配置](#scopedconfiguration)
-   [内存中 OLTP](#InMemory)
-   [查询优化器](#QueryOptimizer)
-   [实时查询统计信息](#LiveStats)
-   [查询存储](#QueryStore)
-   [临时表](#TT)
-   [向 Microsoft Azure Blob 存储进行条带备份](#StripedBackupToAzure)
-   [向 Microsoft Azure Blob 存储进行文件快照备份](#FileSnapshotBackup)
-   [托管备份](#ManagedBackup)
-   [TempDB 数据库](#multipleTempDB)
-   [内置的 JSON 支持](#ForJson)
-   [PolyBase](#bkPolyBase)
-   [Stretch 数据库](#stretch)
-   [支持 UTF-8](#UTF8)
-   [新的默认数据库大小和自动增长值](#DefaultDB)
-   [Transact-SQL 增强功能](#TSQL)
-   [系统视图增强功能](#SystemTable)
-   [安全性改进](#Security)
-   [高可用性增强功能](#HighAvailability)
-   [复制增强功能](#Repl)
-   [工具增强功能](#Tools)

####  <a name="columnstore"></a> 列存储索引

此版本提供了一些用于列存储索引的改进功能，包括可更新的非聚集列存储索引、内存中表上的列存储索引以及更多用于可操作分析的新功能。

- 升级后可更新只读的非聚集列存储索引。  不需要重新生成索引即可将其更新。

- 对列存储索引的分析查询改进了性能，尤其是对于聚合与字符串谓词。

- 对 DMV 和 XEvents 的可支持性得到了改进。

有关更多详细信息，请参阅联机丛书的 [列存储索引指南](../relational-databases/indexes/columnstore-indexes-overview.md) 一节中的以下主题：

- [列存储索引版本的功能摘要](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) — 包括新增功能。

- [列存储索引数据加载](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [列存储索引查询性能](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [开始使用列存储进行实时运行分析](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [针对数据仓库的列存储索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [列存储索引碎片整理](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


####  <a name="scopedconfiguration"></a>数据库作用域配置


新的 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 语句可用于控制特定数据库的特定配置。 配置设置会影响应用程序的行为。

新语句在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 和 [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)]中可用。



####  <a name="InMemory"></a> 内存中 OLTP


##### <a name="storage-format-change"></a>存储格式更改

内存优化表的存储格式在 SQL Server 2014 和 2016 之间更改。 对于升级和从 SQL Server 2014 附加/还原，在数据库恢复过程中，序列化新的存储格式，并重启一次数据库。

- [Upgrade to SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


##### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE 进行了日志优化且并行运行

现在，当你对内存优化表执行 ALTER TABLE 语句时，只会将元数据更改写入日志。 这极大地减少了日志 IO。 此外，多数 ALTER TABLE 方案现在并行运行，从而可以极大地缩短该语句的持续时间。

- 有关非并行异常，包括 LOB，请参阅 [更改内存优化表](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)。



##### <a name="statistics"></a>统计信息

现在，[内存优化表的统计信息](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) 将自动更新。 此外，采样现在是一种受支持的统计信息收集方法，让你无需使用开销更大的 fullscan 方法。


##### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>针对内存优化表的并行和堆扫描

内存优化表及其索引现在支持并行扫描。 这提高了分析查询的性能。

此外，支持堆扫描，可以并行执行。 对于内存优化表，堆扫描是指使用用于存储行的内存堆数据结构对表中的所有行进行扫描。 对于全表扫描来说，堆扫描比使用索引的效率更高。

##### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>内存优化表的 Transact-SQL 改进

以下几个 Transact-SQL 元素在 SQL Server 2014 的内存优化表中不受支持，现在在 SQL Server 2016 中受支持：


- 支持 UNIQUE 约束和索引。


- 支持内存优化表之间的外键引用。
  - 这些外键只能引用主键，不能引用唯一键。


- 支持检查约束。

- 非唯一索引允许其键中有 NULL 值。

- 内存优化表支持触发器。
  - 仅支持 AFTER 触发器。 不支持 INSTEADOF 触发器。
  - 内存优化表上的所有触发器都必须使用 WITH NATIVE_COMPILATION。

- 完全支持内存优化表和本机编译的 T-SQL 模块中所有 SQL Server 代码页、索引排序规则和其他项目。


- 支持 [更改内存优化表](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)：
  - 添加和删除索引。 更改哈希索引的 bucket_count。
  - 进行架构更改：添加/删除/更改列；添加/删除约束。

- 内存优化表现在可以有多个列，这些列的合并长度超过 8060 字节页的长度。 例如，具有三个 `nvarchar(4000)`类型的列的表。 在此类示例中，某些列现在存储在行外。 你的查询丝毫不会意识到某列是在行内还是行外。

- 内存优化表现在支持[LOB（大型对象）类型](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)`和 `varchar(max)` 。


有关整体信息，请参阅：

- [内存中 OLTP 不支持的 Transact-SQL 构造](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [内存中 OLTP 不支持的 SQL Server 功能](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


##### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>本机编译模块的 Transact-SQL 改进

以下几个 Transact-SQL 元素在 SQL Server 2014 的本机编译模块中不受支持，现在在 SQL Server 2016 中受支持：


- 查询构造：
  - UNION 和 UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - SELECT 中的子查询


- INSERT、UPDATE 和 DELETE 语句现在可以包括 [OUTPUT 子句](../t-sql/queries/output-clause-transact-sql.md)。

- 现在可以在本机过程内通过以下方式使用 LOB：
  - 变量声明。
  - 接收的输入参数。
  - 传入本机过程内的字符串函数（例如 LTrim 或子字符串）的参数。


- 内联（表示单个语句）表值函数 (TVF) 现在可在本机编译。

- 标量用户定义函数 (UDF) 现在可在本机编译。

- 增强了对本机过程调用以下函数的支持：
  - 内置 [安全函数](../t-sql/functions/security-functions-transact-sql.md)。
  - 内置 [数学函数](../t-sql/functions/mathematical-functions-transact-sql.md)。
  - 内置函数 `@@SPID`。


- 现在支持 EXECUTE AS CALLER，这意味着创建本机编译的 T-SQL 模块时不再需要 EXECUTE AS 子句。


有关整体信息，请参阅：

- [本机编译的 T-SQL 模块支持的功能](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [更改本机编译的 T-SQL 模块](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)


##### <a name="performance-and-scaling-improvements"></a>性能和缩放性方面的改进

- 对数据大小不再有任何限制。 请参阅 [估算内存优化表的内存需求](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)。

- 现在有多个并发线程负责 [将内存优化表的更改保存到磁盘](../relational-databases/in-memory-oltp/scalability.md)。

- [对使用解释型 Transact-SQL 访问内存优化表](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md)提供并行计划支持。


##### <a name="enhancements-in-sql-server-management-studio"></a>SQL Server Management Studio 中的增强功能

- [确定表或存储过程是否应移植到内存中 OLTP](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 不再要求配置数据收集器或管理数据仓库。 现在可以直接对生产数据库运行报告。

- [用于迁移评估的 PowerShell Cmdlet](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) ，可用于评估一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中多个对象的迁移拟合度。

- 通过右键单击数据库并选择“任务”>“生成内存中 OLTP 迁移清单”来生成迁移清单。

##### <a name="cross-feature-support"></a>跨功能支持

- 支持对内存中 OLTP 使用临时版本由系统控制。 有关详细信息，请参阅 [系统版本控制临时表与内存优化表](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)

- 从内存中 OLTP 工作负载提供对本机编译代码的查询存储支持。 有关详细信息，请参阅 [通过内存中 OLTP 使用查询存储](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)。

- [内存优化表中的行级安全性](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- [使用多个活动的结果集 &#40;MARS&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) 连接现在可以访问内存优化表和本机编译的存储过程。

- [透明数据加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) 支持。 如果为数据库配置了加密，则[内存优化文件组](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)中的文件现在也会加密。

有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。


####  <a name="QueryOptimizer"></a>查询优化器
##### <a name="compatibility-level-guarantees"></a>兼容性级别保证
将数据库升级到 SQL Server 2016 时，如果继续停留在所使用的较旧的兼容性级别（例如，120 或 110），则不会有任何计划更改。 与查询优化器相关的新增功能和改进仅在最新的兼容性级别下可用。 
##### <a name="trace-flag-4199"></a>跟踪标志 4199
一般情况下，不需要在 SQL Server 2016 中使用跟踪标志 4199，因为此跟踪标志控制的大多数查询优化器行为已在 SQL Server 2016 中的最新兼容性级别 (130) 下无条件启用。
##### <a name="new-referential-integrity-operator"></a>新的引用完整性运算符
表最多可以将 253 个其他表和列作为外键引用（传出引用）。 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 将可在单独的表中引用的其他表和列（传入引用）的数量限制从 253 提高至 10,000。 有关限制，请参阅 [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md)。 引入了新的引用完整性运算符（兼容性级别 130），可就地执行引用完整性检查。 这提高了对具有大量传入引用的表的 UPDATE 和 DELETE 操作的总体性能，因此，使拥有大量的传入引用变得可行。 有关详细信息，请参阅 [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)（SQL Server 2016 中查询优化器的新增功能）
##### <a name="parallel-update-of-sampled-statistics"></a>并行更新抽样统计信息
现在并行执行数据采样以生成统计信息（兼容性级别 130），从而提高统计信息收集的性能。 有关详细信息，请参阅 [更新统计信息](../t-sql/statements/update-statistics-transact-sql.md)。
#### <a name="sublinear-threshold-for-update-of-statistics"></a>更新统计信息的次线性阈值
现在针对大型表的统计信息自动更新变得更加主动（兼容性级别 130）。 从 SQL Server 2016 开始，针对大型表的统计信息自动更新的触发阈值为 20%，此阈值随着表中行数的增加而减小（仍用百分比表示）。 不再需要设置跟踪标志 2371 来减小阈值。 
##### <a name="other-enhancements"></a>其他增强功能
Insert-select 语句中的 Insert 是多线程，或者可以具有并行计划（兼容性级别 130）。 若要获取并行计划，INSERT ... SELECT 语句必须使用 TABLOCK 提示。 有关详细信息，请参阅 [Parallel Insert Select](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)（并行的 Insert Select 语句）

####  <a name="LiveStats"></a> 实时查询统计信息
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 能够查看活动查询的实时执行计划。 此实时查询计划作为控制流，能够实时了解从一个查询计划操作员到另一个操作员的查询执行过程。 有关详细信息，请参阅 [Live Query Statistics](../relational-databases/performance/live-query-statistics.md)。

####  <a name="QueryStore"></a> 查询存储
查询存储是一种新功能，让 DBA 可以探查查询计划选择和性能。 它让你可以快速找到查询计划中的更改所造成的性能差异，从而简化了性能疑难解答。 这一性能会自动捕获查询、计划和运行时统计信息的历史记录，并将其保留以供你查看。 它按时间窗口将数据分割开来，使你可以查看数据库使用情况模式并了解服务器上何时发生了查询计划更改。 查询存储通过使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 对话框显示信息，并允许你将查询强制添加到一个所选查询计划。 有关详细信息，请参阅 [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。


####  <a name="TT"></a> 临时表
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 现在支持系统版本控制临时表。 临时表是一种能在任一时间点提供有关存储事实的正确信息的新类型的表。 每个临时表实际上是由两个表组成的，一个用于当前的数据，另一个用于历史数据。 系统可以确保当使用当前数据更改表中数据时，之前的值将会存储在历史表格中。 提供的查询构造可对用户隐藏此复杂性。 有关详细信息，请参阅 [Temporal Tables](../relational-databases/tables/temporal-tables.md)。

####  <a name="StripedBackupToAzure"></a> 向 Microsoft Azure Blob 存储进行条带备份
在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]中，使用 Microsoft Azure Blob 存储服务的“SQL Server 备份到 URL”现在支持使用块 Blob 的条带备份集，从而可以支持 12.8 TB 的最大备份大小。 有关示例，请参阅 [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples)。

####  <a name="FileSnapshotBackup"></a> 向 Microsoft Azure Blob 存储进行文件快照备份
 在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]中，“SQL Server 备份到 URL”现在支持使用 Azure 快照来备份数据库，其中，所有数据库文件将使用 Microsoft Azure Blob 存储服务进行存储。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。

####  <a name="ManagedBackup"></a> 托管备份
在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中，“SQL Server 托管备份到 Microsoft Azure”为备份文件使用新的块 Blob 存储。 此外，对托管备份还做了多项更改和增强。

-   支持备份的自动与自定义计划。

-   支持系统数据库备份。

-   支持使用简单恢复模式的数据库。

 有关详细信息，请参阅 [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)

> [!NOTE]
>  对于 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，这些新的托管备份功能尚未在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中提供相应的 UI 支持。

####  <a name="multipleTempDB"></a> TempDB 数据库
 对 TempDB 做了多项增强：

-   不再需要为 tempdb 使用跟踪标志 1117 和 1118。 如果有多个 tempdb 数据库文件，所有文件都将根据增长设置同时增长。 此外，tempdb 中的所有分配使用统一盘区。

-   默认情况下，安装程序会将尽可能多的 tempdb 文件添加为 CPU 计数或 8，以较小者为准。

-   安装过程中，你可以使用 SQL Server 安装向导的“数据库引擎配置 - TempDB”部分中的 UI 输入控件配置 tempdb 数据库文件数目、初始大小、自动增长增量和目录位置。

-   默认初始大小为 8MB，默认的自动增长增量为 64MB。

-   可为 tempdb 数据库文件指定多个卷。 如果指定了多个目录，tempdb 数据文件将以循环方式分散在目录中。

####  <a name="ForJson"></a> 内置的 JSON 支持
SQL Server 2016 针对导入和导出 JSON 以及处理 JSON 字符串添加了内置支持。 此内置支持包括以下语句和函数。

-   通过将 **FOR JSON** 子句添加到 **SELECT** 语句，将查询结果的格式设置为 JSON 或导出 JSON。 例如，使用 **FOR JSON** 子句委托从客户端应用程序到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 JSON 输出格式设置。 有关详细信息，请参阅[借助 FOR JSON 将查询结果格式化为 JSON (SQL Server)](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。

-   通过调用 **OPENJSON** 行集提供程序函数，将 JSON 数据转换为行与列或导入 JSON。 对于不能直接使用 JSON 的应用或服务，可以使用 **OPENJSON** 将 JSON 数据导入 SQL Server，或者将 JSON 数据转换为行与列。 有关详细信息，请参阅[用 OPENJSON (SQL Server) 将 JSON 数据转换为行和列](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)。

-   **ISJSON** 函数测试字符串是否包含有效 JSON。 有关详细信息，请参阅 [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md)

-   **JSON_VALUE** 函数从 JSON 字符串中提取标量值。有关详细信息，请参阅 [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md)。

-   **JSON_QUERY** 函数从 JSON 字符串中提取对象或数组。 有关详细信息，请参阅 [JSON_QUERY (Transact-SQL)](../t-sql/functions/json-query-transact-sql.md)。

-   **JSON_MODIFY** 函数更新 JSON 字符串中属性的值，并返回已更新的 JSON 字符串。 有关详细信息，请参阅 [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md)。

####  <a name="bkPolyBase"></a>PolyBase
 PolyBase 允许使用 T-SQL 语句访问存储在 Hadoop 或 Azure Blob 存储中的数据并以即席方式对其进行查询。 还允许查询半结构化的数据并将结果与存储在 SQL Server 中的关系数据集联接。 PolyBase 针对数据仓库工作负载进行了优化，旨在分析查询方案。

 有关详细信息，请参阅 [PolyBase 指南](../relational-databases/polybase/polybase-guide.md)。

####  <a name="stretch"></a> Stretch 数据库
 Stretch Database 是 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中的新功能，可以既透明又安全地将历史数据迁移到 Microsoft Azure 云。 可以无缝访问 SQL Server 数据，不管这些数据位于本地还是延伸到云中。 你设置决定数据存储位置的策略，而 SQL Server 则处理后台的数据移动。 整个表始终处于联机状态，始终可供查询。 而且，Stretch Database 无需对现有查询或应用程序进行任何更改 — 数据的位置对于应用程序来说是完全透明的。 有关详细信息，请参阅 [Stretch Database](../sql-server/stretch-database/stretch-database.md)。
 
####  <a name="UTF8"></a> 支持 UTF-8
[bcp 实用工具](../tools/bcp-utility.md)、[BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) 现在支持 UTF-8 代码页。 有关详细信息，请参阅这些主题以及[创建格式化文件 &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)。

####  <a name="DefaultDB"></a>新的默认数据库大小和自动增长值
模型数据库的新值和新数据库（基于模型）的默认值。 数据和日志文件的初始大小现在为 8 MB。 数据和日志文件的默认自动增长增量现在为 64MB。


###  <a name="TSQL"></a> Transact-SQL 增强功能
大量的增强功能支持本主题其他章节中所述的功能。 提供了以下附加增强功能。
- TRUNCATE TABLE 语句现在允许截断指定的分区。 有关详细信息，请参阅 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md)。
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) 现在允许执行多次更改列操作，同时保持表可用。
- 全文索引 DMV [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) 返回关键字在文档中的位置。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 和 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1 中也添加了此 DMV。
- 新的查询提示 **NO_PERFORMANCE_SPOOL** 可以防止将后台打印运算符添加到查询计划。 在配合假脱机操作运行许多并发查询时，这可以提高性能。 有关详细信息，请参阅[查询提示 (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md)。
- [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) 语句经过增强，可以接受 msg_string 参数。
- 非聚集索引的最大索引键大小已增加到 1700 字节。
- 为 AGGREGATE、ASSEMBLY、COLUMN、CONSTRAINT、DATABASE、DEFAULT、FUNCTION、INDEX、PROCEDURE、ROLE、RULE、SCHEMA、SECURITY POLICY、SEQUENCE、SYNONYM、TABLE、TRIGGER、TYPE、USER 和 VIEW 的相关删除语句添加了新的 DROP IF 语法。 请参阅有关语法的各个语法主题。
- 向 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)、[DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 和 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) 添加了 MAXDOP 选项，以指定并行度。
- 现在可以设置 SESSION_CONTEXT。 包括 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md) 函数、[CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) 函数和 [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 过程。
- 高级分析扩展允许用户执行以受支持语言（例如 R）编写的脚本。[!INCLUDE[tsql](../includes/tsql-md.md)] 通过引入 [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 存储过程和[启用了外部脚本的服务器配置选项](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)来支持 R。 有关详细信息，请参阅 [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md)。
- 此外，为了支持 R，还引入了创建外部资源池的功能。 有关详细信息，请参阅 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md)。  新的目录视图和 DMV（[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 和 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)）。 为 [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md) 提供了更多参数。 已将更多的列添加到某些现有资源调控器目录视图和 DMV。
- [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 语法已增强，提供 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 选项来支持始终加密功能。 有关详细信息，请参阅[迁移通过“始终加密”保护的敏感数据](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。
- [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) 和 [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) 函数可将值转换入和转换出 GZIP 算法。
- 添加了 [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) 和 [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) 函数以及 [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 视图，以支持日期和时间交互。
- 现在可以在数据库级别创建凭据（此外，还包括以前提供的服务器级别凭据）。 有关详细信息，请参阅 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)。
- 已将八个新属性添加到 [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md)：InstanceDefaultDataPath、InstanceDefaultLogPath、ProductBuild、ProductBuildType、ProductMajorVersion、ProductMinorVersion、ProductUpdateLevel 和 ProductUpdateReference。
- 已去除 [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md) 函数的 8000 个字节的输入长度限制。
- 添加了新的字符串函数 [STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) 和 [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md)。
- 自动增长选项：跟踪标志 1117 已由 ALTER DATABASE 的 AUTOGROW_SINGLE_FILE 和 AUTOGROW_ALL_FILES 选项取代，跟踪标志 1117 不再有效。 有关详细信息，请参阅 [ALTER DATABASE 文件和文件组选项 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 以及 [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 的新列 is_autogrow_all_files。
- 混合盘区分配：对于用户数据库，对象前 8 页的默认分配将从使用混合页盘区更改为使用统一盘区。 跟踪标志 1118 已由 ALTER DATABASE 的 SET MIXED_PAGE_ALLOCATION 选项取代，跟踪标志 1118 不再有效。 有关详细信息，请参阅 [ALTER DATABASE SET 选项 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) 以及 [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 的新列 `is_mixed_page_allocation_on`。


###  <a name="SystemTable"></a>系统视图增强功能
- 两个新视图支持行级安全性。 有关详细信息，请参阅 [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) 和 [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)。
- 七个新视图支持 Query Store 功能。 有关详细信息，请参阅[查询存储目录视图 (Transact-SQL)](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)。
- 向 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 添加了 24 个新列，以提供有关内存授予的信息。
- 添加了两个新的查询提示（MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT）用于指定内存授予。 请参阅[查询提示 (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md)。
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) 提供基于会话的报告，类似于服务器级 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) 提供有关标量值函数的执行统计信息。
- 从 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 开始，[sys.dm_db_index_usage_stats (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) 中的条目会像 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 以前的版本中那样得到保留。
- 新的动态管理函数 [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) 可以返回提交到的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的语句的相关信息。
- 两个新视图支持 [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md)：[sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 和 [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 


###  <a name="Security"></a> 安全性改进

####  <a name="RLS"></a> 行级安全性
行级安全性引入了基于谓词的访问控制。 它采用灵活的、基于谓词的集中式评估，可以考虑元数据（例如标签）或管理员根据需要确定的任何其他条件。 谓词用作一个条件，以便基于用户属性来确定用户是否具有合适的数据访问权限。 可以使用基于谓词的访问控制来实现基于标签的访问控制。 有关详细信息，请参阅 [行级安全性](../relational-databases/security/row-level-security.md)。


####  <a name="TCE"></a> Always Encrypted
使用始终加密， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以对加密数据执行操作，最重要的是，加密密钥与应用程序驻留在客户所信任的环境中，而不是驻留在服务器上。 始终加密保护客户的数据，因此 DBA 不需要访问纯文本数据。 数据的加密和解密在驱动程序级别透明地进行，这样在最大程度上减少了必须对现有应用程序所做的更改。 有关详细信息，请参阅 [Always Encrypted（数据库引擎）](../relational-databases/security/encryption/always-encrypted-database-engine.md)。


####  <a name="Masking"></a>动态数据屏蔽
动态数据屏蔽通过对非特权用户屏蔽敏感数据来限制敏感数据的公开。 动态数据屏蔽允许用户在尽量减少对应用程序层的影响的情况下，指定需要披露的敏感数据，从而防止对敏感数据的非授权访问。 它是一种基于策略的安全功能，可以隐藏对指定数据库字段进行查询时获得的结果集中的敏感数据，不会更改数据库中的数据。 有关详细信息，请参阅 [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md)。


####  <a name="Perms"></a> 新权限
- **更改任意安全策略** 权限已作为行级安全性实现的一部分提供。
- **ALTER ANY MASK** 和 **UNMASK** 权限已作为动态数据屏蔽实现的一部分提供。
- **ALTER ANY COLUMN ENCRYPTION KEY**、 **VIEW ANY COLUMN ENCRYPTION KEY**、 **ALTER ANY COLUMN MASTER KEY DEFINITION**和 **VIEW ANY COLUMN MASTER KEY DEFINITION** 权限已作为始终加密功能实现的一部分提供。
- **更改任何外部数据源** 和 **更改任何外部文件格式** 权限在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中可见，但仅适用于 [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)])。
- **执行任意外部脚本**权限已作为 R 脚本支持的一部分提供。
 - 可以通过**更改任意数据库范围的配置**权限来授权使用 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 语句。

####  <a name="TDE"></a>透明数据加密
- 透明数据加密已得到增强，支持对加密使用 Intel AES-NI 硬件加速。 这可以减少启用透明数据加密所需的 CPU 开销。

###  <a name="AES"></a> 终结点的 AES 加密
- 终结点的默认加密已从 RC4 更改为 AES。

####  <a name="newcredentialtype"></a> 新凭据类型
- 现在可以在数据库级别创建凭据（此外，还包括以前提供的服务器级别凭据）。 有关详细信息，请参阅 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)。


###  <a name="HighAvailability"></a>高可用性增强
SQL Server 2016 标准版现在支持 Always On 基本可用性组。 基本可用性组支持主要副本和次要副本。 此功能取代了已过时的高可用性数据库镜像技术。 有关基本和高级可用性组之间的差异的详细信息，请参阅[基本可用性组 &#40;Always On 可用性组&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。

现在，支持跨一组只读副本对读取意向连接请求进行负载平衡。 以前的行为始终将连接定向到路由列表中第一个可用的只读副本。 有关详细信息，请参阅 [在只读副本间配置负载平衡](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。

 支持自动故障转移的副本数已从两个增加到三个。

 Always On 故障转移群集现在支持组托管服务帐户。 有关详细信息，请参阅 [Group Managed Service Accounts](https://technet.microsoft.com/library/hh831782.aspx)（组托管服务帐户）。 对于 Windows Server 2012 R2，需要安装一项更新来避免更改密码后出现临时停机。 若要获取该项更新，请参阅 [在 Windows Server 2012 R2 域中更改密码后基于 gMSA 的服务无法登录](https://support.microsoft.com/kb/2998082/)。

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 支持 Windows Server 2016 上的分布式事务和 DTC。 有关详细信息，请参阅 [对分布式事务的支持](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport)。

 现在，你可以将 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 配置为在数据库脱机时进行故障转移。 此项更改需要在 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 或 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 语句中将 **DB_FAILOVER** 选项设置为 **ON**。

Always On 现在支持加密的数据库。 当你创建新的可用性组、添加数据库或者将副本添加到现有可用性组时，可用性组向导现在将提示你输入任何数据库的、包含数据库主密钥的密码。

现在，可以将两个不同 Windows Server 故障转移群集 (WSFC) 中的两个可用性组合并成一个分布式可用性组。 有关详细信息，请参阅[分布式可用性组&#40;Always On 可用性组&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。

直接种子设定允许通过网络自动设定次要副本的种子（而手动种子设定需要在次要副本上还原目标数据库的物理备份）。 可以通过在 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 或 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 语句中设置 **SEEDING_MODE=AUTOMATIC** 来指定直接种子设定。 还必须在用于直接种子设定的每个次要副本上使用 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 指定 **GRANT CREATE ANY DATABASE**。

**性能改进** — 通过在主要副本上对日志块进行更快速的并行压缩（一种优化的同步协议），并在次要副本上对日志记录进行并行解压缩和恢复，将可用性组的同步吞吐量提升了约 10 倍。 这将提高可读次要副本的新鲜度，并减少故障转移时的数据库恢复时间。 请注意，在 SQL Server 2016 中，对内存优化表的恢复操作目前不是并行的。

###  <a name="Repl"></a> 复制增强功能
- 现在支持复制内存优化表。 有关详细信息，请参阅 [复制到内存优化表订阅服务器](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)。
- 现在支持复制到 [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]。 有关详细信息，请参阅 [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md)。

###  <a name="Tools"></a> 工具增强功能

####  <a name="SSMS"></a> Management Studio
下载最新的 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 支持正在开发的、用于连接到 Microsoft Azure 的 Active Directory 身份验证库 (ADAL)。 它取代了 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中使用的基于证书的身份验证。
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 安装要求安装 .NET 4.6 作为先决条件。 安装 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 时，安装程序将自动安装 .NET 4.6。
- 新的查询结果网格支持在从结果网格中复制或保存文本时保留回车符/换行符。 可以从“工具”-“选项”菜单设置此功能。
- 不再从主功能树安装 SQL Server 管理工具；有关详细信息，请参阅 [安装带有 SSMS 的 SQL Server 管理工具](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)。
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 安装要求 .NET 4.6.1 作为先决条件。 安装 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 时，安装程序将自动安装 .NET 4.6.1。

####  <a name="UA"></a> 升级顾问
SQL Server 2016 Upgrade Advisor Preview 是一个独立的工具，可让以前版本的用户针对其 SQL Server 数据库运行一组升级规则，以查明重大更改和行为更改与已弃用的功能，以及为采用新功能（例如 Stretch Database）提供帮助。

 你可以从 [此处](https://www.microsoft.com/en-us/download/details.aspx?id=48119) 下载 Upgrade Advisor Preview，也可以使用 Web 平台安装程序来安装它。

## <a name="see-also"></a>另请参阅
[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)
 
[SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md) 
 
[安装带有 SSMS 的 SQL Server 管理工具](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)








