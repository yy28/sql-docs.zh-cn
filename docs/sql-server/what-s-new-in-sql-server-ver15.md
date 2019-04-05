---
title: SQL Server 2019 中的新增功能 | Microsoft Docs
ms.date: 03/27/2018
ms.prod: sql-server-2019
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cfb679bdec74536d62b3f332ff644d80435907c0
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618264"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新增功能

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 在早期版本的基础上构建，旨在将 SQL Server 发展成一个平台，以提供开发语言、数据类型、本地或云以及操作系统选项。 本文汇总了 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新增功能。 第一部分标识了最新预览版中添加的功能。 本文的其他部分提供了针对此 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 迄今为止发布的所有功能的详细信息。

有关详细信息和已知问题，请参阅 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 发行说明](sql-server-ver15-release-notes.md)。

试用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]！

- [![从评估中心下载](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下载 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以在 Windows 上安装](https://go.microsoft.com/fwlink/?LinkID=862101)。
- 在 Linux 上针对 [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md) 安装。
- [在 Docker 上运行 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../linux/quickstart-install-connect-docker.md)。

使用[最新工具](#tools)获得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳体验。

## <a name="ctp-24"></a>CTP 2.4

社区技术预览版 (CTP) 2.4 是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最新公开版本。 此版本包含来自 CTP 历史版本的改进功能，可修复 bug、增强安全性和优化性能。 此外，下面是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.4 的新增功能或增强功能。

- [大数据群集](#bigdatacluster)
  - 关于 GPU 支持在 Spark 中使用 TensorFlow 运行深度学习的指南。
  - Spark 运行时升级到 Spark 2.4。
  - 数据池的 `INSERT INTO SELECT` 支持。
  - 适用于外部表查询的 `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 选项子句。

- [数据库引擎](#databaseengine)
  - 截断错误消息默认包括表名和列名以及截断值。 请参阅[截断](#truncation)。
  - 新的 DMF `sys.dm_exec_query_plan_stats` 返回大多数查询的最后已知实际执行计划的等效项。
  - 透明数据加密 (TDE) 扫描 - 暂停和恢复。

- [SQL Server Analysis Services](#ssas)
  - 表格模型中的多对多关系。
  - 资源管理的属性设置。

以下部分介绍在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md) 的早期版本中引入的新功能。

## <a id="bigdatacluster"></a>大数据群集

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [大数据群集](../big-data-cluster/big-data-cluster-overview.md)支持新方案，包括以下内容：

- [GPU 支持在 Spark 中使用 TensorFlow 运行深度学习](../big-data-cluster/spark-gpu-tensorflow.md)。 (CTP 2.4)
- Spark 运行时升级到 Spark 2.4。 (CTP 2.4)
- 数据池的 `INSERT INTO SELECT` 支持。
- 适用于外部表查询的 `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 选项子句。
- [在 IntelliJ 中的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]大数据群集上提交 Spark 作业](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md)。 (CTP 2.3)
- 各种数据相关应用的[应用程序部署和管理体验](../big-data-cluster/big-data-cluster-create-apps.md)，包括使用 R 和 Python 操作化器学习模型、运行 SQL Server Integration Services (SSIS) 作业等。 (CTP 2.3)
- [在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]大数据群集中使用 Sparklyr](../big-data-cluster/sparklyr-from-RStudio.md)。 (CTP 2.3)
- 通过 [HDFS 分层](../big-data-cluster/hdfs-tiering.md)将兼容 HDFS 的外部存储装入大数据群集。 (CTP 2.3)
- 在大数据群集上使用 Azure Data Studio 中的 SparkR。 (CTP 2.2)
- [部署 Python 和 R 应用](../big-data-cluster/big-data-cluster-create-apps.md)。 (CTP 2.2)
- 在 Kubernetes 上部署带 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Spark Linux 容器的大数据群集。 (CTP 2.0)
- 从 HDFS 访问大数据。 (CTP 2.0)
- 使用 Spark 运行高级分析和机器学习。 (CTP 2.0)
- 使用 Spark 将数据流式传输到 SQL 数据池。 (CTP 2.0)
- 在 [Azure Data Studio](../sql-operations-studio/what-is.md) 中运行提供 notebook 体验的查询书籍。 (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 数据库引擎

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]为 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 引入或强化了以下新功能。

### <a name="new-querypostexecutionplanprofile-extended-event-ctp-24"></a>新的 query_post_execution_plan_profile 扩展事件 (CTP 2.4)

新的 `query_post_execution_plan_profile` 扩展事件基于轻型分析收集实际执行计划的等效项，与使用标准分析的 `query_post_execution_showplan` 不同。 有关详细信息，请参阅[查询分析基础结构](../relational-databases/performance/query-profiling-infrastructure.md)。

#### <a name="example-1---extended-event-session-using-standard-profiling"></a>示例 1 - 使用标准分析的扩展事件会话

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>示例 2 - 使用轻型分析的扩展事件会话

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

### <a name="new-dmf-sysdmexecqueryplanstats-ctp-24"></a>新的 DMF sys.dm_exec_query_plan_stats (CTP 2.4) 

新的 DMF `sys.dm_exec_query_plan_stats` 将基于轻型分析返回大多数查询的最后已知实际执行计划的等效项。 有关详细信息，请参阅 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) 和[查询分析基础结构](../relational-databases/performance/query-profiling-infrastructure.md)。 作为示例，请参见以下脚本：

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

这是一个选择加入功能，并且需要启用[跟踪标志](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。

### <a name="transparent-data-encryption-tde-scan---suspend-and-resume-ctp-24"></a>透明数据加密 (TDE) 扫描 - 暂停和恢复 (CTP 2.4)

为了在数据库上启用[透明数据加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md)，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 必须执行加密扫描，此操作会从数据文件将每个页面读入缓冲池，然后将加密的页面写回磁盘。 为了使用户能够更好地控制加密扫描，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了 TDE 扫描 - 暂停和恢复语法，可以实现当系统上的工作负荷繁重时或在关键业务时间内暂停扫描，然后稍后再恢复扫描。

使用以下语法暂停 TDE 加密扫描：

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

同样，以下语法将恢复 TDE 加密扫描：

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

为了显示加密扫描的当前状态，已将 `encryption_scan_state` 添加到了 `sys.dm_database_encryption_keys` 动态管理视图中。 还有一个名为 `encryption_scan_modify_date` 的新列，此列将包含上次加密扫描状态更改的日期和时间。 另请注意，如果在加密扫描处于暂停状态时重启 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，启动时系统将在错误日志中记录一条消息，指示存在已暂停的现有扫描。

### <a name="accelerated-database-recovery-ctp-23"></a>加速数据库恢复 (CTP 2.3)

通过重新设计 SQL Server 数据库引擎恢复过程，[加速数据库恢复](/azure/sql-database/sql-database-accelerated-database-recovery/)极大地提高了数据库可用性，尤其是存在长时间运行的事务时。 [数据库恢复](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started)是 SQL Server 用于让每个数据库以事务一致状态或干净状态启动的进程。 启用了加速数据库恢复的数据库在故障转移或其他非干净关闭后完成恢复操作的速度显著加快。 自 CTP 2.3 起，可以使用以下语法按数据库启用加速数据库恢复：

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

> [!NOTE]
> 在 Azure SQL DB 中利用该功能不需要此语法，该功能默认启用。

如果有易于受到大型事务影响的关键数据库，请在预览期间试用此功能。 向 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 团队](<https://aka.ms/sqlfeedback>)提供反馈。

### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>查询存储计划强制支持快速向前移动和静态游标 (CTP 2.3)

查询存储现在支持为快速向前和静态 T-SQL 及 API 游标强制执行查询执行计划。 现在，通过 `sp_query_store_force_plan` 或通过 SQL Server Management Studio 查询存储报表支持强制执行。

### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>跨多个作用域使用临时表减少了对工作负荷的重新编译 (CTP 2.3)

在推出此功能之前，当引用带有数据操作语言 DML 语句（`SELECT`、`INSERT`、`UPDATE`、`DELETE`）的临时表时，如果此临时表由外部作用域批处理创建，则会导致每次执行时都会重新编译 DML 语句。 借助此改进，SQL Server 可执行其他轻量级检查来避免不必要的重新编译：

- 检查在编译时用于创建临时表的外部作用域模块是否与用于连续执行的外部作用域模块相同。 
- 跟踪在初始编译时所做的任何数据定义语言 (DDL) 更改，并将它们与连续执行的 DDL 操作进行比较。 

最终结果是减少了无关的重新编译和 CPU 开销。

### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>改进了间接检查点可伸缩性 (CTP 2.3)

在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的之前版本中，如果存在生成大量脏页的数据库（例如 tempdb），用户可能会遇到计划程序无法完成错误。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为间接检查点引入了改进的可伸缩性，这应该有助于避免具有大量 UPDATE/INSERT 工作负荷的数据库中出现这些错误。

### <a name="utf-8-support-ctp-23"></a>UTF-8 支持 (CTP 2.3)

完全支持广泛使用的 UTF-8 字符编码作为导入或导出编码，或作为文本数据的数据库级或列级排序规则。 `CHAR` 和 `VARCHAR` 数据类型允许使用 UTF-8，并在创建或将对象的排序规则更改为带有 `UTF8` 后缀的排序规则时启用 UTF-8。 

例如：将 `LATIN1_GENERAL_100_CI_AS_SC` 更改为 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 仅适用于支持增补字符的 Windows 排序规则，如 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中所引入的。 `NCHAR` 和 `NVARCHAR` 仅允许 UTF-16 编码，并保持不变。

此功能可能会节省大量存储空间，具体取决于正在使用的字符集。 例如，使用已启用 UTF-8 的排序规则将带 ASCII（拉丁）字符串的现有列数据类型从 `NCHAR(10)` 更改为 `CHAR(10)`，意味着将减少 50% 的存储需求。 存储需求减少是因为 `NCHAR(10)` 需要 20 个字节进行存储，而 `CHAR(10)` 需要 10 个字节存储相同的 Unicode 字符串。

有关详细信息，请参阅 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。

**CTP 2.1** 现支持在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 安装期间默认选择 UTF-8 排序规则。

**CTP 2.2** 现支持将 UTF-8 字符编码与 SQL Server 复制结合使用。

**CTP 2.3** 现支持将 UTF-8 字符编码与 BIN2 排序规则 (UTF8_BIN2) 结合使用。

### <a name="scalar-udf-inlining-ctp-21"></a>标量 UDF 内联 (CTP 2.1)

标量 UDF 内联自动将标量用户定义函数 (UDF) 转换为关系表达式，并将其嵌入调用 SQL 查询，从而提高利用标量 UDF 的工作负载性能。 标量 UDF 内联有助于实现基于成本的 UDF 内部操作优化，并产生面向集合的并行高效计划，而不是低效、迭代、串行执行计划。 在数据库兼容性级别 150 下默认启用此功能。

有关详细信息，请参阅[标量 UDF 内联](../relational-databases/user-defined-functions/scalar-udf-inlining.md)。

### <a name="a-nametruncation-truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a><a name="truncation" />已对截断错误消息进行了改进，包括了表名和列名以及截断值 (CTP 2.1)

开发或维护数据移动工作负载的许多 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 开发人员和管理员非常熟悉错误消息 ID 8152 `String or binary data would be truncated`；当源数据太大而无法适应目标数据类型时，使用不同架构在源和目标之间进行数据传输会引发错误。 针对此错误消息进行故障排查可能非常耗时。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 针对此情况引入了更具体的新错误消息 (2628)：  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

新错误消息 2628 为数据截断问题提供更多上下文，从而简化了故障排查过程。 

**CTP 2.1 和 CTP 2.2** 这是一个选择加入错误消息，要求启用[跟踪标志](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460。

**CTP 2.4** 在数据库兼容性级别 150 下，错误消息 2628 成为默认截断消息并替换了错误消息 8152。 引入了新的数据库范围的配置 `VERBOSE_TRUNCATION_WARNINGS` 以在数据库兼容性级别为 150 时在错误消息 2628 和 8152 之间进行切换。 有关详细信息，请参阅 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。
对于数据库兼容性级别 140 或更低级别，错误消息 2628 仍然是要求启用[跟踪标志](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 的选择加入错误消息。

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>改进了用于统计信息阻塞的诊断数据 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为等待同步统计信息更新操作的长时间运行查询提供了改进的诊断数据。 如果 `SELECT` 在继续执行查询之前等待同步统计信息更新操作完成，则动态管理视图 `sys.dm_exec_requests` 列 `command` 显示 `SELECT (STATMAN)`。 此外，新的等待类型 `WAIT_ON_SYNC_STATISTICS_REFRESH` 会显示在 `sys.dm_os_wait_stats` 动态管理视图中。 它显示了针对同步统计信息刷新操作耗费的实例级别累计时间。

### <a name="hybrid-buffer-pool-ctp-21"></a>混合缓冲池 (CTP 2.1)

混合缓冲池是 SQL Server 数据库引擎的一项新功能，可以在必要时直接访问位于永久性内存 (PMEM) 设备上的数据库文件上的数据库页。 由于 PMEM 设备为数据访问提供非常低的延迟，因此，引擎可以放弃在缓冲池的“干净页面”区域中制作数据副本，只是直接在 PMEM 上访问该页。 使用内存映射 I/O 执行访问，就像启用一样。 这样可以避免将页面副本复制到 DRAM，并避免操作系统的 I/O 堆栈访问永久性存储上的页面，从而带来性能优势。 Windows 上的 SQL Server 和 Linux 上的 SQL Server 都提供此功能。

有关详细信息，请参阅[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)

### <a name="static-data-masking-ctp-21"></a>静态数据掩码 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了静态数据掩码。 可以使用静态数据掩码来清理 SQL Server 数据库副本中的敏感数据。 静态数据掩码有助于创建净化的数据库副本，其中所有敏感信息的更改方式使得副本可与非生产用户共享。 静态数据掩码可用于开发、测试、分析和业务报告、符合性、故障排除以及无法将特定数据复制到不同环境的任何其他情况。

静态数据掩码在列级别操作。 选择要对其应用掩码的列，并为所选的每列指定一个掩码函数。 静态数据掩码会复制数据库，然后将指定的掩码函数应用于各列。

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>静态数据掩码与动态数据掩码

数据掩码是在数据库上应用掩码以隐藏敏感信息并将其替换为新数据或经过清理的数据的过程。 Microsoft 提供两个掩码选项，静态数据掩码和动态数据掩码。 [!INCLUDE[ssSQL16](../includes/sssql16-md.md)] 中已引入动态数据掩码。 下表将比较这两种解决方案：

|静态数据掩码 |动态数据屏蔽|
|:----|:----|
|发生在数据库副本上 <br/><br/>无法检索原始数据<br/><br/>掩码发生在存储级别<br/><br/>所有用户均可访问相同的掩码数据<br/><br/>针对整个团队范围具有持续访问权限|发生在原始数据库上<br/><br/>原始数据保持不变<br/><br/>掩码在查询时发生<br/><br/>掩码因用户权限不同而异 <br/><br/>严格的用户特定访问权限限制|

### <a name="database-compatibility-level-ctp-20"></a>数据库兼容性级别 (CTP 2.0)

已添加数据库“COMPATIBILITY_LEVEL 150”。 若要启用特定用户数据库，请执行：

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="resumable-online-index-create-ctp-20"></a>可恢复联机索引创建 (CTP 2.0)

可恢复联机索引创建允许索引创建操作暂停并稍后从操作暂停或失败的位置恢复，而不是从头开始重新启动。

可恢复联机索引创建支持以下方案：
- 在索引创建失败后恢复索引创建操作，例如在数据库故障转移后或磁盘空间不足后。
- 暂停正在进行的索引创建操作并稍后恢复，以便根据需要允许暂时释放系统资源，并稍后恢复此操作。
- 在无需使用过多日志空间和阻止其他维护活动的长时间运行事务以及不允许日志截断的情况下创建大型索引。

如果没有此功能，当索引创建失败，则必须再次执行联机索引创建操作，且必须从头开始重新启动该操作。

在此版本中，我们将扩展可恢复功能，以将此功能添加到可用的[可恢复联机索引重新生成](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)。

此外，可以使用[面向联机和可恢复 DDL 操作的数据库范围的默认设置](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)，将此功能设置为特定数据库的默认设置。

有关详细信息，请参阅[可恢复联机索引创建](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)。

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>联机生成和重新生成聚集列存储索引 (CTP 2.0)

将行存储表转换为列存储格式。 创建聚集列存储索引 (CCI) 在以前版本 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中为离线过程 - 在创建 CCI 时需停止所有更改。 使用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]，可以联机创建或重新创建 CCI。 不会阻止工作负载，而且对基础数据所做的所有更改都将以透明方式添加到目标列存储表。 可以使用的新 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句示例有：

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>具有安全 Enclave 的 Always Encrypted (CTP 2.0)

使用就地加密和丰富计算来扩展 Always Encrypted。 扩展来自在服务器端的安全 enclave 内对纯文本数据启用计算。

加密操作包括列加密和列加密密钥轮换。 现在可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 来发布这些操作，并且它们不需要将该数据移出数据库。 安全 enclave 向一组更广泛的方案提供 Always Encrypted，包括以下两个要求：  

- 要求敏感数据受到保护，防止具有高特权但未经授权的用户（包括数据库管理员、系统管理员、云操作员或恶意软件用户）对其进行访问。
- 另一个要求是数据库系统支持对受保护数据的丰富计算。

有关详细信息，请参阅[具有安全 Enclave 的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。

> [!NOTE]
> 具有安全 enclave 的 Always Encrypted 仅可在 Windows OS 上使用。

### <a name="intelligent-query-processing-ctp-20"></a>智能查询处理 (CTP 2.0)

- 通过调整批处理模式和行模式运算符的内存授予大小，行模式内存授予反馈扩展了 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中引入的内存授予反馈功能。 对于内存授予过量的情况，如果授予的内存是实际使用内存大小的两倍，内存授予反馈将重新计算内存授予。 然后，连续执行将请求更少的内存。 对于造成到磁盘的溢出的大小不足的内存授予，内存授予反馈将触发重新计算内存授予。 然后，连续执行将请求更多的内存。 在数据库兼容性级别 150 下默认启用此功能。

- 近似 COUNT DISTINCT 返回组中唯一非空值的近似数。 此函数旨在用于大数据方案。 该函数针对查询进行了优化，其中满足所有以下条件：
   - 访问至少数百万行的数据集。
   - 聚合包含大量非重复值的一个或多个列。
   - 响应能力比绝对精度更重要。
      - `APPROX_COUNT_DISTINCT` 返回的结果通常在准确答案的 2% 范围内。
      - 它在准确答案所需的一小部分时间内返回近似答案。

- 行存储上的批处理模式不再需要列存储索引在批处理模式下处理查询。 批处理模式允许查询运算符在一组行上工作，而不是一次仅处理一行。 在数据库兼容性级别 150 下默认启用此功能。 当满足所有以下条件，批处理模式可提高访问行存储表的查询速度：
   - 查询使用分析运算符，如联接或聚合运算符。
   - 查询涉及 100,000 或更多行。
   - 该查询受到 CPU 的约束，而不受输入/输出数据的约束。
   - 创建和使用列存储索引具有以下缺点之一：
      - 会给查询增加过多开销。
      - 或者不可行，因为应用程序依赖于列存储索引尚不支持的一项功能。

- 表变量延迟编译功能提升了计划质量和引用表变量的查询的整体性能。 在优化和初始编译期间，此功能会传播基于实际表变量行计数的基数估计。 这种准确的行计数信息将用于优化下游计划操作。 在数据库兼容性级别 150 下默认启用此功能。

若要使用智能查询处理功能，设置数据库 `COMPATIBILITY_LEVEL = 150`。

### <a id="programmability"></a> Java 语言可编程性扩展 (CTP 2.0)

- **Java 语言扩展 （预览版）**：使用 Java 语言扩展来执行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 Java 代码。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例添加“机器学习服务（数据库内）”功能时将安装此扩展。

### <a id="sqlgraph"></a> SQL 图形功能 (CTP 2.3)

- **在图形匹配查询中使用派生表或视图别名 (CTP 2.1)** [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 预览版中的图形查询支持使用 `MATCH` 语法中的视图和派生表别名。 若要在 `MATCH` 中使用这些别名，必须使用 `UNION ALL` 运算符在一组节点或一组边界表上创建视图和派生表。 节点或边界表不一定包含筛选器。 在要查询图中两个或更多个实体之间的异类实体或异类连接的情况下，在 `MATCH` 查询中使用派生表和视图别名的功能非常有用。

- 通过 `MERGE` DML 中的支持匹配 (CTP 2.0)，可以指定单个语句中的图形关系，而不是单独的 `INSERT`、`UPDATE` 或 `DELETE` 语句。 使用 `MERGE` 语句中的 `MATCH` 谓词将节点或边界表中的当前图形数据与新数据合并。 此功能启用边界表上的 `UPSERT` 方案。 用户现在可以使用单个合并语句在两个节点之间插入一个新的边界或更新现有边界。

- **边缘约束 (CTP 2.0)** 被引入了 SQL 图形中的边界表。 边界表可以将任何节点连接到数据库中的任何其他节点。 引入边缘约束后，现在可以对此行为应用一些限制。 新 `CONNECTION` 约束可用于指定将允许给定边缘表在架构中连接的节点类型。 

  **(CTP 2.3)** 进一步扩展此功能，使你可以在边缘约束上定义级联删除操作。 可以定义数据库引擎在用户删除给定边缘连接的节点时执行的操作。

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations-ctp-20"></a>针对联机和可恢复 DDL 操作的数据库范围的默认设置 (CTP 2.0)

- 联机和可恢复 DDL 操作的数据库范围的默认设置允许对数据库级别的 `ONLINE` 和 `RESUMABLE` 的默认行为设置，而不是为每个单独的索引 DDL 语句（比如 index create 或 rebuild）定义这些选项。

- 使用 `ELEVATE_ONLINE` 和 `ELEVATE_RESUMABLE` 数据库范围的配置选项设置这些默认值。 这两个选项都会导致引擎自动将支持操作提升为索引联机或可恢复执行。 可以使用这些选项启用以下行为：

  - `FAIL_UNSUPPORTED` 选项允许所有联机或可恢复的索引操作，并使不支持联机或可恢复的索引操作失败。
  - `WHEN_SUPPPORTED` 选项允许支持的联机或可恢复操作并运行索引不支持的脱机或不可恢复操作。
  - `OFF` 选项允许执行所有脱机且不可恢复索引操作的当前行为，除非在 DDL 语句中显式指定。

要替代默认设置，请在 index create 和 rebuild 命令中包含 `ONLINE` 或 `RESUMABLE` 选项。 

如果没有此功能，则必须直接在索引 DDL 语句（如 index create 和 rebuild）中指定“联机”和“可恢复”选项。

有关可恢复的索引操作的详细信息，请参阅[可恢复联机索引创建](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/)。

### <a id="ha"></a>AlwaysOn 可用性组 - 更多同步副本 (CTP 2.0)

- 最多五个同步副本：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 将同步副本的最大数目从 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中的 3 增加到 5。 可以配置此组的 5 个副本在该组中进行自动故障转移。 有 1 个主要副本以及 4 个同步的次要副本。

- **主要副本到辅助副本连接重定向**：允许客户端应用程序连接定向到主要副本，而不考虑在连接字符串中指定的目标服务器。 此功能允许在不使用侦听器的情况下进行连接重定向。 在以下情况下使用次要副本到主要副本连接重定向：

  - 群集技术不提供侦听器功能。
  - 重定向较为复杂的多子网配置。
  - 读取扩展或灾难恢复场景，其群集类型为 `NONE`。

有关详细信息，请参阅[次要副本到主要副本读/写连接重定向（AlwaysOn 可用性组）](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。

### <a name="data-discovery-and-classification-ctp-20"></a>数据发现和分类 (CTP 2.0)

数据发现和分类提供本机内置于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的高级功能。 对最敏感的数据进行分类和标记提供以下优势：
- 帮助满足数据隐私标准和法规遵从性要求。
- 支持安全方案，如监视（审核），以及对敏感数据异常访问的警报。
- 可以更轻松地识别企业中敏感数据所在的位置，以便管理员采取正确措施来保护数据库。

有关详细信息，请参与 [SQL 数据发现和分类](../relational-databases/security/sql-data-discovery-and-classification.md)。

对[审核](../relational-databases/security/auditing/sql-server-audit-database-engine.md)进行了强化处理，在审核日志中包含了名为 `data_sensitivity_information` 的新字段，其中记录查询返回的实际数据的敏感度分类（标签）。 有关详细信息和示例，请参阅[添加敏感度分类](../t-sql/statements/add-sensitivity-classification-transact-sql.md)。

>[!NOTE]
>就审核启用方式方面没有任何更改。 在审核日志中包含了新字段 `data_sensitivity_information`，该字段记录查询返回的实际数据的敏感度分类（标签）。 请参阅[审核对敏感数据的访问](/azure/sql-database/sql-database-data-discovery-and-classification/#subheading-3)。

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>对永久性内存设备的扩展支持 (CTP 2.0)

任何置于永久性内存设备上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件现在都可以在启用模式下运行。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 直接访问设备，使用高效的 memcpy 操作绕过操作系统的存储堆栈。 此模式可以提高性能，因为它允许针对此类设备的低延迟输入/输出。
    - 示例 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件包括：
        - 数据库文件
        - 事务日志文件
        - 内存中 OLTP 检查点文件
    - 永久性内存也称为“存储类内存”。
    - 在一些非 Microsoft 网站上，永久性内存有时会通俗地称为“pmem”。

> [!NOTE]
> 对于此预览版，永久性内存设备上的文件启用只在 Linux 上可用。 Windows 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持自 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 起开始提供的永久性内存设备。

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>支持 DBCC CLONEDATABASE 中的列存储统计信息 (CTP 2.0)

`DBCC CLONEDATABASE` 创建仅限架构的数据库副本，其中包括在不复制数据的情况下对查询性能问题进行故障排除所需的所有元素。 在以前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，该命令不会复制所需的统计信息来准确地对列存储索引查询进行故障排除，且需要手动步骤来捕获此信息。 现在，在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，`DBCC CLONEDATABASE` 自动捕获列存储索引的统计信息 blob，因此不再需要任何手动步骤。

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>向 sp_estimate_data_compression_savings 添加了新选项 (CTP 2.0)

`sp_estimate_data_compression_savings` 返回所请求对象的当前大小并估算对象在所请求的压缩状态下的大小。 此过程当前支持三个选项：`NONE`、`ROW` 和 `PAGE`。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了两个新选项：`COLUMNSTORE` 和 `COLUMNSTORE_ARCHIVE`。 如果使用标准或存档列存储压缩在表中创建列存储索引，可以使用这些新选项来估计节省的空间。

### <a id="ml"></a> SQL Server 机器学习服务故障转移群集和基于分区的建模 (CTP 2.0)

- **基于分区的建模**：使用添加到 `sp_execute_external_script` 的新参数来处理每个数据分区的外部脚本。 此功能支持训练多个小型模型（每个数据分区一个模型）而不是一个大型模型。

- **Windows Server 故障转移群集**：在 Windows Server 故障转移群集上配置机器学习服务的高可用性。

有关详细信息，请参阅 [SQL Server 机器学习服务中的新增功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>默认情况下启用轻量查询分析基础结构 (CTP 2.0)

相比标准分析机制，轻量查询分析基础结构 (LWP) 能够更有效地提供查询性能数据。 现在，默认情况下启用轻量分析。 已在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 中引入此功能。 轻量分析提供查询执行统计信息集合机制，预期开销为 2% CPU，而标准查询分析机制的开销高达 75% CPU。 在早期版本中，默认禁用此功能。 数据库管理员可通过[跟踪标志 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 来启用它。 

有关此轻量分析的详细信息，请参阅[查询分析基础结构](../relational-databases/performance/query-profiling-infrastructure.md)。

**CTP 2.3** 引入了范围为新数据库的配置 `LIGHTWEIGHT_QUERY_PROFILING`用于启用或禁用轻量级查询分析基础结构。

### <a id="polybase"></a> 新 PolyBase 连接器

- 面向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的新连接器：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的外部数据引入了新连接器。

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>新 sys.dm_db_page_info 系统函数返回页面信息 (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` 返回有关数据库页面的信息。 该函数将返回包含页中标头信息的行，包括 `object_id`、`index_id` 和 `partition_id`。 在大多数情况下，此函数取代了使用 `DBCC PAGE` 的需要。 

为帮助解决与页面相关的等待，还向 `sys.dm_exec_requests` 和 `sys.sysprocesses` 添加了名为“page_resource”的新列。 此新列允许你通过另一个新系统函数 `sys.fn_PageResCracker` 将 `sys.dm_db_page_info` 联接到这些视图。 作为示例，请参见以下脚本：

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> Linux 上的 SQL Server

- **Docker 容器上使用 Kubernetes 的 AlwaysOn 可用性组 (CTP 2.2)**：Kubernetes 可以协调运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的容器，以提供一组高度可用的数据库，其中包含 SQL Server AlwaysOn 可用性组。 Kubernetes 运算符部署一个 StatefulSet，其中包括带 mssql-server container 的容器和运行状况监视器。

- **新容器注册表 (CTP 2.1)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的所有容器映像现均位于 Microsoft 容器注册表中。 Microsoft 容器注册表是用于分发 Microsoft 产品容器的官方容器注册表。 此外，现发布了已认证的基于 RHEL 映像。

  - Microsoft 容器注册表：`mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 经认证的基于 RHEL 的容器映像：`mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

- **复制支持 (CTP 2.0)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支持 Linux 上的 SQL Server 复制。 使用 SQL 代理的 Linux 虚拟机可以是发布服务器、分发服务器上或订阅服务器。 

  创建以下类型的发布：
  - 事务性
  - 快照
  - 合并

  配置复制 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或使用[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

- **支持 Microsoft 分布式事务处理协调器 (MSDTC) (CTP 2.0)**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支持 Microsoft 分布式事务处理协调器 (MSDTC)。 有关详细信息，请参阅[如何在 Linux 上配置 MSDTC](../linux/sql-server-linux-configure-msdtc.md)。

- **OpenLDAP 支持第三方 AD 提供商 (CTP 2.0)**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支持 OpenLDAP，它允许第三方提供商加入 Active Directory。

- **Linux 上的机器学习 (CTP 2.0)**：Linux 现在支持 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 机器学习服务（数据库内）。 支持包括 `sp_execute_external_script` 存储过程。 有关如何在 Linux 上安装机器学习服务的说明，请参阅[在 Linux 上安装 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 机器学习服务 R 和 Python 支持](../linux/sql-server-linux-setup-machine-learning.md)。

## <a id="mds"></a> Master Data Services 

- **用 HTML 替换的 Silverlight 控件 (CTP 2.0)**：Master Data Services (MDS) 门户不再依赖 Silverlight。 所有以前的 Silverlight 组件均已替换为 HTML 控件。

## <a id="security"></a>安全性

- **SQL Server 配置管理器中的证书管理 (CTP 2.0)**：SSL/TLS 证书广泛用于保护对 SQL Server 实例的访问。 证书管理现已集成到 SQL Server 配置管理器，以简化诸如以下常见任务：

  - 查看和验证安装在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的证书。 
  - 查看即将到期的证书。
  - 在参与到 AlwaysOn 可用性组的机器之间部署证书（从包含主要副本的节点）。
  - 在参与到故障转移群集实例的机器之间部署证书（从活动节点）。

  > [!NOTE]
  > 用户必须拥有所有群集节点的管理员权限。

## <a id="tools"></a>工具

- [**Azure Data Studio**](../azure-data-studio/what-is.md)：此前以预览版名称 SQL Operations Studio 发布，Azure Data Studio 是一个轻量、新式、开源的跨平台桌面工具，用于数据开发和管理中的最常见任务。 通过使用 Azure Data Studio 和 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 预览版扩展](../azure-data-studio/sql-server-2019-extension.md)，可以在 Windows、macOS 和 Linux 上连接到本地和云中的 SQL Server。 使用 Azure Data Studio，可以：

  - 现在支持 AAD。 (CTP 2.3)
  - 笔记本视图 UI 已移至 Azure Data Studio 核心。 (CTP 2.3)
  - 添加了新的向导，用于从 Hadoop 分布式文件系统 (HDFS) 创建到 SQL Server 大数据群集的外部数据源。 (CTP 2.3)
  - 改进了笔记本查看器 UI。 (CTP 2.3)
  - 添加了新的笔记本 API。 (CTP 2.3)
  - 添加了“重新安装笔记本依赖项”命令以协助 Python 包更新。 (CTP 2.3)
  - 连接和管理 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 大数据群集。 (CTP 2.1)
  - 在现代开发环境中使用快如闪电的 Intellisense、代码段和源代码管理集成编辑和运行查询。 (CTP 2.0) 
  - 快速使用结果集的内置图表来可视化数据。 (CTP 2.0)
  - 使用可自定义小组件为服务器和数据库创建自定义仪表板。 (CTP 2.0)  
  - 使用内置终端轻松管理更广泛的环境。 (CTP 2.0)
  - 在基于 Jupyter 构建的集成 notebook 体验中分析数据。 (CTP 2.0)
  - 使用自定义主题和扩展增强体验。(CTP 2.0)
  - 并通过内置订阅和资源浏览器探索 Azure 资源。 (CTP 2.0)
  - 支持使用 SQL Server 大数据群集方案。 (CTP 2.0)
  
  > [!TIP]
  > 有关 Azure Data Studio 的最新改进，请参阅 [Azure Data Studio 发行说明](../azure-data-studio/release-notes-azure-data-studio.md)。

- [**SQL Server Management Studio (SSMS) 18.0（预览版）**](../ssms/sql-server-management-studio-ssms.md)：支持 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。

  - 从 SSMS 启动 Azure Data Studio。 (CTP 2.3)
  - 支持具有安全 enclave 的 Always Encrypted。 (CTP 2.0)
  - 减小了下载大小。 (CTP 2.0)
  - 现基于 Visual Studio 2017 独立 Shell。 (CTP 2.0)
  - 有关完整列表，请参阅 [SSMS 更改日志](../ssms/sql-server-management-studio-changelog-ssms.md)。 (CTP 2.0)

- [**SQL Server PowerShell 模块**](http://www.powershellgallery.com/packages/SqlServer/21.1.18080)：SqlServer PowerShell 模块允许 SQL Server 开发人员、管理员和 BI 专业人员自动化数据库部署和服务器管理。

  - 从 21.0 升级到 21.1 以支持 SMO v150。
  - 更新了 SQL Server 提供程序 (SQLRegistration) 以显示 AS/IS/RS 组。
  - 修复了以 SQL Server 2014 为目标时 `New-SqlAvailabilityGroup` cmdlet 中的问题。
  - 已将 `–LoadBalancedReadOnlyRoutingList` 参数添加到 `Set-SqlAvailabilityReplica` 和 `New-SqlAvailabilityReplica`。
  - 更新了 `AnalysisService` cmdlet 以将来自 `Login-AzureAsAccount` 的缓存登录令牌用于 Azure Analysis Services。

## <a id="ssas"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS) 

### <a name="many-to-many-relationships-in-tabular-models-ctp-24"></a>表格模型中的多对多关系 (CTP 2.4)

此功能允许表之间存在多对多关系，两个表中的列都是非唯一的。 可以在维度和事实表之间以高于维度的键列的粒度定义关系。 这样避免了对维度表进行标准化并且可以改善用户体验，因为生成的模型具有较少带有逻辑分组列的表。 对于此 CTP 2.4 版本，多对多关系是仅限引擎于的功能。 

多对多关系要求模型处于 1470 兼容性级别，此级别目前仅在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 及更高版本中受支持。 对于此 CTP 2.4 版本，可以通过使用表格对象模型 (TOM) API、表格模型脚本语言 (TMSL) 和开源表格编辑器工具创建多对多关系。 未来版本中将包含 SQL Server Data Tools (SSDT) 中的支持以及文档。 Analysis Services 博客中将提供有关此 CTP 功能版本和其他 CTP 功能版本的其他信息。

### <a name="memory-settings-for-resource-governance-ctp-24"></a>资源管理的内存设置 (CTP 2.4)

此处所述的内存设置已在 Azure Analysis Services 中提供。 从 CTP 2.4 开始，这些设置现在也受到 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Analysis Services 的支持。 

- **Memory\QueryMemoryLimit** - 此内存属性可用于限制由提交给模型的 DAX 查询构建的内存假脱机。 
- **DbpropMsmdRequestMemoryLimit** - 此 XMLA 属性可用于替代适用于连接的 Memory\QueryMemoryLimit 服务器属性值。
- **OLAP\Query\RowsetSerializationLimit** - 此服务器属性限制行集中返回的行数，从而保护服务器资源免受大量数据导出使用的影响。 此属性适用于 DAX 和 MDX 查询。

可以使用最新版本的 SQL Server Management Studio (SSMS) 设置这些属性。 Analysis Services 博客中将提供有关此功能的其他信息。

### <a name="calculation-groups-in-tabular-models-ctp-23"></a>表格模型中的计算组 (CTP 2.3) 

计算组解决了复杂模型中的常见问题，即，使用相同的计算（例如时间智能）可能会出现度量值激增的问题。 计算组在报告客户端中作为具有单个列的表显示。 列中的每个值都表示一个可应用于任何度量值的可重用计算或计算项。  

计算组可以拥有任意数量的计算项。 每个计算项由 DAX 表达式定义。 引入了三个新的 DAX 函数来与计算组配合使用： 

- `SELECTEDMEASURE()` - 返回对当前位于上下文中的度量值的引用。  

- `SELECTEDMEASURENAME()` - 返回包含当前位于上下文中的度量值的名称的字符串。  

- `ISSELECTEDMEASURE(M1, M2, …)` - 返回布尔值，指示当前位于上下文中的度量值是否为指定为参数的度量值之一。

除新的 DAX 函数外，还引入了两个新的动态管理视图：

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

#### <a name="limitations-in-this-release"></a>此版本中的限制：

- 尚不支持 `ALLSELECTED DAX` 函数。
- 尚不支持在计算组表上定义的行级别安全性。
- 尚不支持在计算组表上定义的对象级别安全性。
- 尚不支持引用计算项的 DetailsRows 表达式。
- 尚不支持 MDX。

#### <a name="known-issues-in-this-release"></a>此版本中的已知问题：

- 模型中存在计算组可能导致度量值返回变量数据类型，这可能导致引用度量值的计算列和表刷新失败。

#### <a name="compatibility-level"></a>兼容级别

计算组要求模型处于 1470 兼容性级别，此级别目前仅在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 及更高版本中受到支持。 目前，可以使用表格对象模型 (TOM) API、表格模型脚本语言 (TMSL) 和开源表格编辑器工具创建计算组。 未来版本中将包含 SQL Server Data Tools (SSDT) 中的支持以及文档。 Analysis Services 博客中将提供有关此 CTP 功能版本和其他 CTP 功能版本的其他信息。

## <a name="other-services"></a>其他服务

自 CTP 2.4 起，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 将不为以下服务引入新功能：

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>后续步骤

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]发行说明](sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：技术白皮书](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />于 2018 年 9 月发布。 适用于面向 Windows、Linux 和 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
