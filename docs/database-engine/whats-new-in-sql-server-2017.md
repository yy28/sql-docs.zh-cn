---
title: 数据库引擎中的新增功能 - SQL Server 2017 | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
author: rothja
ms.author: jroth
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 6c0889349631a543e970b11eff9bb24a6f2da208
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874453"
---
# <a name="whats-new-in-database-engine---sql-server-2017"></a>数据库引擎中的新增功能 - SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

本主题介绍对 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 的 [!INCLUDE[ssdenoversion-md](../includes/ssdenoversion-md.md)] 所做的改进。 单击下面的链接可获取每项改进的详细信息。

> [!NOTE]  
> SQL Server 2017 还包括 SQL Server 2016 Service Pack 中新增的功能。 有关这些项目，请参阅 [SQL Server 2016（数据库引擎）中的新增功能](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)。

**增强功能**  

- CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 使用 `PERMISSION_SET = SAFE` 创建的 CLR 程序集可以访问外部系统资源、调用非托管代码以及获取 sysadmin 特权。 从 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 开始，引入了名为 `clr strict security` 的 `sp_configure` 选项，以增强 CLR 程序集的安全性。 默认启用 `clr strict security`，并将 `SAFE` 和 `EXTERNAL_ACCESS` 程序集与标记为 `UNSAFE` 的程序集同等对待。 可禁用 `clr strict security` 选项以实现后向兼容性，但不建议这样做。 Microsoft 建议所有程序集都通过证书或非对称密钥进行签名，且该证书或非对称密钥具有已在主数据库中获得 `UNSAFE ASSEMBLY` 权限的相应登录名。 现在可以将 CLR 程序集添加到允许列表中，作为 `clr strict security` 功能的变通方法。 添加 [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)、[sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) 和 [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) 以支持受信任的程序集允许列表。 有关详细信息，请参阅 [CLR 严格安全性](configure-windows/clr-strict-security.md)。  
- 引入了新的 DMF [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)，用于公开摘要级别特性和有关事务日志文件的信息；对于监视事务日志的运行状况很有用。  
- 可恢复的联机索引重新生成。 可恢复的联机索引重新生成可从发生故障（例如到副本的故障转移或磁盘空间不足）后联机索引重新生成操作停止处恢复该操作。 还可暂停操作，随后再恢复联机索引重新生成操作。 例如，可能需要暂时释放系统资源，以便执行高优先级任务或在其他维护时段完成索引重新生成操作（如果可用的维护时段太短，不足以处理大型表格）。 最后一点，可恢复的联机索引重新生成操作不需要大量的日志空间，因此可以在可恢复的重新生成操作运行时执行日志截断。 请参阅 [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 和[联机索引操作准则](../relational-databases/indexes/guidelines-for-online-index-operations.md)。
- ALTER DATABASE SCOPED CONFIGURATION 的 IDENTITY_CACHE 选项  。 向 `ALTER DATABASE SCOPED CONFIGURATION` T-SQL 语句添加了新选项 IDENTITY_CACHE。 此选项设置为 `OFF` 时，如果服务器意外重启或故障转移到辅助服务器，数据库引擎可避免标识列的值中出现空白。 请参阅 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。   
-  [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] 现在提供图形数据库功能，可对更具意义的面向关系的数据建模。 包括用于创建节点和边界表的新 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 语法，以及用于查询的关键字 [MATCH](../t-sql/queries/match-sql-graph.md)。 有关详细信息，请参阅[使用 SQL Server 2017 进行图形处理](../relational-databases/graphs/sql-graph-overview.md)。   
- 新一代的查询处理改进，将对应用程序工作负荷的运行时状况采用优化策略。 对于这款适应性查询处理功能系列初版，我们进行了 3 项新的改进：批处理模式自适应联接、批处理模式内存授予反馈，以及针对多语句表值函数的交错执行     。  请参阅 [SQL 数据库中的智能查询处理](../relational-databases/performance/intelligent-query-processing.md)。
- 自动优化是一种数据库功能，提供对潜在查询性能问题的深入了解、提出建议解决方案并自动解决已标识的问题。 [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] 中的自动优化功能会在检测到潜在性能问题时发出通知，并允许应用更正措施或 [!INCLUDE[ssde-md](../includes/ssde-md.md)] 自动解决性能问题。 有关详细信息，请参阅[自动优化](../relational-databases/automatic-tuning/automatic-tuning.md)。
- 针对内存优化表上的非群集索引生成的性能增强。 显著优化了数据库恢复期间 MEMORY_OPTIMIZED 表的 bwtree（非聚集）索引重新生成的性能。 这一改进明显缩短了使用非聚集索引时的数据库恢复时间。  
- [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 有三个新列：socket_count、cores_per_socket、numa_node_count。 这在 VM 中运行服务器时非常有用，因为超出 NUMA 会导致过度使用主机，这最终会转化为性能问题。
- 在 [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) 中引入了新列 modified_extent_page_count\,，用于跟踪数据库的每个数据库文件中的差异更改。 使用新列 modified_extent_page_count 可生成智能备份解决方案，如果数据库中发生更改的页面的百分比低于阈值（假设为 70-80%），此解决方案将执行差异备份；否则将执行完整数据库备份。
- SELECT INTO ...ON FileGroup - [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) 现支持将表加载到文件组，使用 SELECT INTO TSQL 语法中添加的 ON 关键字的用户的默认文件组除外  。
- Tempdb 安装程序改进 - 此安装程序允许最多将初始 tempdb 文件大小指定为 256 GB (262,144 MB)/文件；如果文件大小设置为大于 1 GB 的值且未启用 IFI，客户会收到警告  。 请务必了解不启用实例文件初始化 (IFI) 的影响，此时安装时间可能会呈指数增加，具体取决于指定的 tempdb 数据文件的初始大小。 IFI 不适用于事务日志大小，因此在安装期间启动 tempdb 时，指定较大的事务日志值始终会增加安装时间，这与 SQL Server 服务帐户的 IFI 设置无关。
- 引入了新的 dmv [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)，用于跟踪每个数据库的版本存储使用情况。 新 dmv 可用于监视 tempdb 获取版本存储使用情况，借此可根据每个数据库的版本存储使用情况要求预先规划 tempdb 的大小，不会产生任何性能开销或在生产数据库上运行此 dmv 的开销。
- 引入了新的 DMF [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)，用于向 DBCC LOGINFO 公开 VLF 等信息，以监视和发出警报，并避免由于 VLF 数量、VLF 大小而导致的潜在事务日志问题或客户遇到的 shrinkfile 问题。
- 改进了高端服务器上小型数据库的备份性能 - 在 SQL Server 中执行数据库备份的同时，备份进程会要求对缓冲池执行多次迭代以消耗当前进行的 I/O。 因此，备份时间不只是数据库大小的函数，还是活动缓冲池大小的函数。 SQL Server 2017 对备份进行了优化，可避免多次迭代缓冲池，进而动态提高中小型数据库的备份性能。 当备份页面和备份 IO 占用的时间超过缓冲池迭代时，数据库大小将增加，此时性能提高的幅度会降低。  
- 查询存储现在可以跟踪等待统计摘要信息。 在查询存储中按查询跟踪等待统计类别可体验下一级别的性能故障排除，还能提供工作负荷性能及其瓶颈的详细信息，同时保留查询存储的主要优势。  
- 系统版本控制的临时表现在支持级联删除和级联更新。  
- 间接检查点性能改进。
- 新增了对“无群集可用性组”的支持。
- 添加了“最小复制提交可用性组”设置。
- 可用性组现可跨 Windows-Linux 工作，从而实现跨操作系统的迁移和测试。
- 新增了对“临时表保留策略”的支持，
- New DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增了对联机非聚集列存储索引生成和重新生成的支持
- 添加了[sys.dm_db_stats_histogram (TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) ，用于检查统计信息。
- 随 SQL Server Management Studio 版本 16.4 发布的数据库优化顾问 (DTA)，在分析 SQL Server 2016 及更高版本时，具有额外的选项。    
   - 改进的性能。 有关详细信息，请参阅 [使用数据库引擎优化顾问 (DTA) 改进性能的建议](../relational-databases/performance/performance-improvements-using-dta-recommendations.md)。
   - `-fc` 选项，可允许建议列存储索引。 有关详细信息，请参阅 [DTA 实用工具](../tools/dta/dta-utility.md) 和 [数据引擎优化顾问 (DAT) 中的列存储索引建议](../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)。  
   - `-iq` 选项，可允许 DTA 从查询存储中查看工作负载。 有关详细信息，请参阅 [使用查询存储中的工作负载优化数据库](../relational-databases/performance/tuning-database-using-workload-from-query-store.md)。  
- 对于内存中功能，还提供了对内存优化表和本机编译函数的其他增强功能。 有关说明这些增强功能的代码示例，请参阅[使用内存中 OLTP 优化 JSON 处理](../relational-databases/json/optimize-json-processing-with-in-memory-oltp.md)。
    - 支持内存优化表中的计算列，包括计算列上的索引。
    - 在本机编译模块和检查约束中对 JSON 函数的完全支持。  
    - 本机编译模块中的`CROSS APPLY` 运算符。   
- 增加了新的字符串函数 [CONCAT_WS](../t-sql/functions/concat-ws-transact-sql.md)、 [TRANSLATE](../t-sql/functions/translate-transact-sql.md)和 [TRIM](../t-sql/functions/trim-transact-sql.md) 。   
- `WITHIN GROUP` 子句现在支持 [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) 函数。
- 增加了两个新的日语排序规则系列（Japanese_Bushu_Kakusu_140 和 Japanese_XJIS_140），并增加了在这些新的日语排序规则中使用的排序规则选项 Variation-selector-sensitive (_VSS)。 此外，所有新的排序规则将自动支持补充字符，而无需指定 _SC 选项。 有关详细信息，请参阅 [排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)   
- 新的批量访问选项（[BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET(BULK...)](../t-sql/functions/openrowset-transact-sql.md)）允许直接从如下两种文件访问数据：指定为 CSV 格式的文件，以及通过[外部数据源](../t-sql/statements/create-external-data-source-transact-sql.md) 的新 `BLOB_STORAGE` 选项存储在 Azure Blob 存储中的文件。
- 数据库 **COMPATIBILITY_LEVEL** 140 已添加。   在此级别上运行的客户将获得最新语言功能和查询优化器行为。 这包括每个 Microsoft 发布的预发布版本中的更改。
- 对计算增量统计信息更新阈值的方式的改进（需要140 兼容模式）。
- [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 已添加。
- 我们对内存优化对象进行了几项性能和语言增强：
    - 内存优化表现在支持 `sp_spaceused`。
    - 内存优化表和本机编译的 T-SQL 模块现在支持 `sp_rename`。
    - 本机编译的 T-SQL 模块现在支持 `CASE` 表达式。
    - 内存优化表上 8 个索引的限制已消除。
    - 本机编译的 T-SQL 模块中现在支持 `TOP (N) WITH TIES`。
    - 针对内存优化表的 `ALTER TABLE` 现在通常要快得多。
    - 现在可并行执行内存优化表的事务日志恢复。 这有助于加速恢复并显著提高 AlwaysOn 可用性组配置的持续吞吐量。
    - 现在可在 Azure 存储中存储内存优化文件组文件。 现在还支持在 Azure 存储中备份/还原内存优化文件。
- 聚集列存储索引现支持 LOB 列 (nvarchar(max)、varchar(max)、varbinary(max))。
- 已添加 [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) 聚合函数。  
- 新权限： `DATABASE SCOPED CREDENTIAL` 当前属于安全对象类，可支持 `CONTROL`、 `ALTER`、 `REFERENCES`、 `TAKE OWNERSHIP`和 `VIEW DEFINITION` 权限。 现可在 `sys.fn_builtin_permissions` 中查看仅限于 SQL 数据库的 `ADMINISTER DATABASE BULK OPERATIONS`。   
- 添加了 [sys.dm_os_host_info](../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV，为 Windows 和 Linux 提供操作系统信息。   
- 使用 R Services 创建数据库角色，以管理与包关联的权限。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。

