---
title: SQL Server 2019 中的新增功能 | Microsoft Docs
ms.date: 08/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d65ca67e43c35f0997b3d0784c97e501606bd05b
ms.sourcegitcommit: c0fd28306a3b42895c2ab673734fbae2b56f9291
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71096889"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新增功能

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 在早期版本的基础上构建，旨在将 SQL Server 发展成一个平台，以提供开发语言、数据类型、本地或云以及操作系统选项。

本文总结了 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和增强功能。

有关详细信息和已知问题，请参阅 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 发行说明](sql-server-ver15-release-notes.md)。

使用[最新工具](what-s-new-in-sql-server-ver15-prerelease.md#tools)获得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳体验  。

>[!NOTE]
>内容是针对 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候选发布而发布的。 候选发布是预发布软件。 信息可能会发生变更。 若要详细了解支持方案，请参阅[支持](#support)。
>
>此次发布包含之前在社区技术预览版 (CTP) 中公布的改进。 这些改进不仅新增了功能、修复了 bug，还提高了安全性并优化了性能。 有关在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候选发布之前的 CTP 版本中引入和改进的功能列表，请参阅 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 公告存档](what-s-new-in-sql-server-ver15-prerelease.md)。

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 为 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 引入了 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]。 它还为 SQL Server 数据库引擎、SQL Server Analysis Services、SQL Server 机器学习服务、Linux 上的 SQL Server 和 SQL Server Master Data Services 提供了附加功能和改进。

下面几个部分概述了这些功能。

## [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 可缩放的大数据解决方案 | [部署](../big-data-cluster/deploy-get-started.md) SQL Server、Spark 和在 Kubernetes 上运行的 HDFS 容器的可缩放群集 <br/><br/> 在 Transact-SQL 或 Spark 中读取、写入和处理大数据<br/><br/> 通过大容量大数据轻松合并和分析高价值关系数据<br/><br/>查询外部数据源<br/><br/>在由 SQL Server 管理的 HDFS 中存储大数据<br/><br/>通过群集查询多个外部数据源的数据<br/><br/> 将数据用于 AI、机器学习和其他分析任务<br/><br/> 在 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 中部署和运行应用程序 <br/><br/> SQL Server 主实例数据库使用 Always On 可用性组<br/>|
| &nbsp; | &nbsp; |

如需了解更多详情，请参阅[什么是 SQL Server [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]](../big-data-cluster/big-data-cluster-overview.md)。

[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP) 公告存档](what-s-new-in-sql-server-ver15-prerelease.md)中列出了含有此功能的所有先前 CTP 版本中公告和更改的功能。

## <a name="database-engine"></a>数据库引擎

### <a name="security"></a>Security

|新增功能或更新 | 详细信息 |
|:---|:---|
|具有安全 Enclave 的 Always Encrypted|通过对服务器端安全隔离区中的纯文本数据启用计算，使用就地加密和丰富计算扩展 Always Encrypted。 就地加密可提高加密列、旋转列加密密钥等加密操作的性能和可靠性，因为这样可以避免将数据移出数据库。 对丰富计算（模式匹配和比较操作）的支持可将 Always Encrypted 解锁到一组更广泛的方案和应用程序，这些方案和应用程序需要敏感数据保护，同时还需要在 Transact-SQL 查询中使用更丰富的功能。 请参阅[包含安全 Enclave 的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。|
|暂停和恢复透明数据加密 (TDE) 的初始扫描|请参阅[透明数据加密 (TDE) 扫描 - 暂停和继续](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)。|
|SQL Server 配置管理器中的证书管理|请参阅[证书管理（SQL Server 配置管理器）](../database-engine/configure-windows/manage-certificates.md)。|
| &nbsp; | &nbsp; |

### <a name="graph"></a>图形

|新增功能或更新 | 详细信息 |
|:---|:---|
|边缘约束级联删除操作 |在图形数据库中，在边缘约束上定义级联删除操作。 请参阅[边缘约束](../relational-databases/tables/graph-edge-constraints.md)。 |
|新增图形函数 - `SHORTEST_PATH` | 可以使用 `MATCH` 内的 `SHORTEST_PATH` 来查找图中任意 2 个节点之间的最短路径，或执行任意长度遍历。|
|分区表和索引| 已分区表和已分区索引的数据被划分为多个单元，这些单元可以跨图形数据库中的多个文件组分散。 |
|在图形匹配查询中使用派生表或视图别名 |请参阅[图形匹配查询](../t-sql/queries/match-sql-graph.md)。 |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>索引

|新增功能或更新 | 详细信息 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]内启用优化，有助于提高索引中高并发插入的吞吐量。 此选项旨在用于易发生最后一页插入争用的索引，常见于有顺序键（如标识列、序列或日期/时间列）的索引。 有关详细信息，请参阅 [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)。|
|联机聚集列存储索引生成和重新生成 | 请参阅[联机执行索引操作](../relational-databases/indexes/perform-index-operations-online.md)。 |
|可恢复联机行存储索引生成 | 请参阅[联机执行索引操作](../relational-databases/indexes/perform-index-operations-online.md)。 |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>内存中数据库

|新增功能或更新 | 详细信息 |
|:---|:---|
|混合缓冲池的 DDL 控制 |使用[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)，可以在需要时直接访问位于永久性内存 (PMEM) 设备上数据库文件中的数据库页。|
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Unicode 支持

|新增功能或更新 | 详细信息 |
|:---|:---|
|支持 UTF-8 字符编码 |支持使用 UTF-8 字符进行导入和导出编码，并用作字符串数据的数据库级别或列级别排序规则。 这支持将应用程序扩展到全球范围，其中提供全球多语言数据库应用程序和服务的要求对于满足客户需求和特定市场规范至关重要。 请参阅[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。<br/><br/> [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候选发布为 PolyBase 外部表和 Always Encrypted 启用 UTF-8 支持。|
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|新增功能或更新 | 详细信息 |
|:---|:---|
|查询外部表 |外部表列名现可用于查询 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 数据源。 请参阅[什么是 PolyBase](../relational-databases/polybase/polybase-guide.md)。|
|支持 UTF-8 字符编码|外部表支持 UTF-8 字符。 请参阅[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。|
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>服务器设置

|新增功能或更新 | 详细信息 |
|:---|:---|
|混合缓冲池| [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的新功能，可以在需要时直接访问位于永久性内存 (PMEM) 设备上数据库文件中的数据库页。 请参阅[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)。|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>性能监视

|新增功能或更新 | 详细信息 |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 动态管理视图中新的等待类型。 它显示了针对同步统计信息刷新操作耗费的实例级别累计时间。 请参阅 [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|
|查询存储的自定义捕获策略|启用后，在新的“查询存储捕获策略”设置下有额外可用的查询存储配置，可用于微调特定服务器中的数据收集。 有关详细信息，请参阅 [ALTER DATABASE SET 选项](../t-sql/statements/alter-database-transact-sql-set-options.md)。|
|`LIGHTWEIGHT_QUERY_PROFILING`|新数据库范围配置。 请参阅 [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)。 |
|`sys.dm_exec_requests` 列 `command` | 如果 `SELECT` 在继续执行查询之前等待同步统计信息更新操作完成，则显示 `SELECT (STATMAN)`。 请参阅 [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|
|`sys.dm_exec_query_plan_stats` |新的 DMF 返回大多数查询的最后已知实际执行计划的等效项。 请参阅 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)。|
|`LAST_QUERY_PLAN_STATS` | 要启用 `sys.dm_exec_query_plan_stats` 的新数据库范围配置。 请参阅 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|`query_post_execution_plan_profile` | 扩展事件基于轻型分析收集实际执行计划的等效项，与使用标准分析的 `query_post_execution_showplan` 不同。 请参阅[查询分析基础结构](../relational-databases/performance/query-profiling-infrastructure.md)。|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>语言扩展

|新增功能或更新 | 详细信息 |
|:---|:---|
|新 Java 语言 SDK | 简化了可从 SQL Server 运行的 Java 程序的开发。 请参阅 [SQL Server 的用于 Java 的 Microsoft 扩展性 SDK](../language-extensions/how-to/extensibility-sdk-java-sql-server.md)。 |
|Java 语言 SDK 是开放源代码的 |[Microsoft SQL Server 用于 Java 的 Microsoft 扩展性 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) 目前是开源的，可[在 GitHub 上获取](https://github.com/microsoft/sql-server-language-extensions)。|
|对 Java 数据类型的支持|请参阅 [Java 数据类型](../language-extensions/how-to/java-to-sql-data-types.md)。|
|新默认 Java 运行时 | SQL Server 现在包括 Azul System 的 Zulu Embedded，用于在整个产品中提供 Java 支持。 有关详细信息，请参阅 [Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/)（SQL Server 2019 现已提供免费支持的 Java）。 |
|SQL Server 语言扩展| 使用扩展性框架执行外部代码。 请参阅 [SQL Server 语言扩展](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)。
|注册外部语言|新的 DDL `CREATE EXTERNAL LANGUAGE` 在 SQL Server 中注册外部语言，如 Java。 请参阅 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。 |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>空间

|新增功能或更新 | 详细信息 |
|:---|:---|
| 新的空间引用标识符 (SRID) |[Australian GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) 提供了更为可靠和准确的数据，这些数据与全球定位系统提供的数据更加接近。 新 SRID 为：<br/><br/> - 7843 表示地理 2D<br/> - 7844 表示地理 3D <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 视图包含新 SRID 的定义。 |
| &nbsp; | &nbsp; |

### <a name="performance"></a>性能

|新增功能或更新 | 详细信息 |
|:---|:---|
|加速数据库恢复 | 按数据库启用加速数据库恢复。 请参阅[加速数据库恢复](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)。|
|强制快进和静态游标 | 查询存储计划强制支持快进和静态游标。 请参阅[计划强制支持快进和静态游标](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)。|
|资源调控| `REQUEST_MAX_MEMORY_GRANT_PERCENT` 和 `ALTER WORKLOAD GROUP` 的 `CREATE WORKLOAD GROUP` 选项的可配置值已从整数更改为浮点数数据类型，以允许更精细地控制内存限制。 请参阅[修改工作负载组](../t-sql/statements/alter-workload-group-transact-sql.md)和[创建工作负载组](../t-sql/statements/create-workload-group-transact-sql.md)。|
|减少了对工作负荷的重新编译| 改进跨多个作用域使用临时表。 请参阅[减少了对工作负荷的重新编译](../relational-databases/tables/tables.md#ctp23) |
|间接检查点可伸缩性 |请参阅[改进了间接检查点可伸缩性](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)。|
|内存优化 `tempdb` 元数据| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了属于[内存数据库](../relational-databases/in-memory-database.md)功能系列的新功能，即内存优化 `tempdb` 元数据，它可有效消除此瓶颈，并为 `tempdb` 繁重的工作负荷解锁新的可伸缩性级别。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，管理临时表元数据时所涉及的系统表可以移动到无闩锁的非持久内存优化表中。 请参阅[内存优化 `tempdb` 元数据](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)。|
|并发 PFS 更新|[PFS 页](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125)是数据库文件中的特殊页面，SQL Server 用来在为对象分配空间时帮助定位可用空间的。 PFS 页上的页闩锁争用通常与 [`tempdb`](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) 关联，但当有许多并发对象分配线程时，也可能会在用户数据库上发生。 此改进改变了使用 PFS 更新来管理并发的方式，这样就能在共享闩锁（而不是排他闩锁）下更新它们。 自 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 起，此行为在所有数据库（包括 `tempdb`）中默认处于启用状态。|
|行模式内存授予反馈 |通过调整批处理模式和行模式运算符的内存授予大小，扩展了批处理模式内存授予反馈功能。 这可以自动更正导致内存浪费和并发减少的过度授予，并更正导致费用高昂的溢出到磁盘的内存授予不足。 请参阅[行模式内存授予反馈](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)。 |
|表变量延迟编译|提升了引用表变量的查询的计划质量和整体性能。 在优化和初始编译期间，此功能传播基于实际表变量行计数的基数估计。 这种准确的行计数信息可优化下游计划操作。 请参阅[表变量延迟编译](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)。 |
|`APPROX_COUNT_DISTINCT `|对于绝对精度不重要、但响应速度很关键的情况，`APPROX_COUNT_DISTINCT` 使用比 `COUNT(DISTINCT())` 更少的资源跨大型数据集进行聚合，以实现高级并发。 请参阅[近似查询处理](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)。|
|行存储上的批处理模式|行存储上的批处理模式支持批处理模式执行，而无需使用列存储索引。 批处理模式执行在分析工作负荷期间更高效地使用 CPU，但低于 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的版本中，只有当查询包含具有列存储索引的运算时才使用它。 然而，有些应用程序可能会使用列存储索引不支持的功能，因此无法利用批处理模式。 自 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 起，批处理模式在符合条件的分析工作负载上启用，这些工作负载的查询包含具有任何类型索引（行存储或列存储）的运算。 请参阅[行存储上的批处理模式](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore)。 |
|标量 UDF 内联|自动将标量 UDF 转换为关系表达式，并将它们嵌入调用 SQL 查询。 此转换提升了利用标量 UDF 的工作负载的性能。 请参阅[标量 UDF 内联](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)。|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>可用性组

|新增功能或更新 | 详细信息 |
|:---|:---|
|最多五个同步副本|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 将同步副本的最大数目从 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中的 3 增加到了 5。 可以配置此组的 5 个副本在该组中进行自动故障转移。 有 1 个主要副本以及 4 个同步的次要副本。|
|次要副本到主要副本连接重定向| 允许客户端应用程序连接定向到主要副本，而不考虑在连接字符串中指定的目标服务器。 有关详细信息，请参阅[次要副本到主要副本读/写连接重定向（AlwaysOn 可用性组）](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。|
| &nbsp; | &nbsp; |

### <a name="setup"></a>设置 

|新增功能或更新 | 详细信息 | 
|:---|:---| 
|新内存设置选项 | 在安装过程中设置“最小服务器内存(MB)”  和“最大服务器内存(MB)”  服务器配置。 有关详细信息，请参阅[“数据库引擎配置 - 内存”页](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)，以及[通过命令提示符安装 SQL Server](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install) 中的 `USESQLRECOMMENDEDMEMORYLIMITS`、`SQLMINMEMORY` 和 `SQLMAXMEMORY` 参数。 建议值遵循[服务器内存配置选项](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)中的内存配置准则。| 
|新并行度设置选项 | 在安装过程中设置“最大并行度”  服务器配置。 有关详细信息，请参阅[“数据库引擎配置 - MaxDOP”页](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)，以及[通过命令提示符安装 SQL Server](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install) 中的 `SQLMAXDOP` 参数。 默认值遵循[配置服务器配置选项“最大并行度”](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)中的最大并行度准则。| 
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>错误消息

|新增功能或更新 | 详细信息 |
|:---|:---|
|详细截断警告 | 截断错误消息默认包括表名和列名以及截断值。 请参阅 [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)。|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

| 新增功能或更新 | 详细信息 |
|:-----|:-----|
|新建容器注册表|[开始使用 Docker 上的 SQL Server 容器](../linux/quickstart-install-connect-docker.md) |
|复制支持 |[Linux 上的 SQL Server 复制](../linux/sql-server-linux-replication.md)
|支持 Microsoft 分布式事务处理协调器 (MSDTC) |[如何在 Linux 上配置 MSDTC](../linux/sql-server-linux-configure-msdtc.md) |
|OpenLDAP 支持第三方 AD 提供商 |[教程：对 Linux 上的 SQL Server 使用 Active Directory 身份验证](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux 上的机器学习 |[在 Linux 上配置机器学习](../linux/sql-server-linux-setup-machine-learning.md) |
|`tempdb` 改进： | 默认情况下，Linux 上的 SQL Server 新安装会根据逻辑内核数创建多个 `tempdb` 数据文件（最多 8 个数据文件）。 这不适用于就地次要版本或主版本升级。 每个 `tempdb` 文件的大小为 8MB，且自动增长大小为 64MB。 此行为类似于 Windows 上的默认 SQL Server 安装。 |
| Linux 上的 PolyBase | 在 Linux 上为非 Hadoop 连接器[安装 PolyBase](../relational-databases/polybase/polybase-linux-setup.md)。<br/><br/>[PolyBase 类型映射](../relational-databases/polybase/polybase-type-mapping.md)。 |
| 变更数据捕获 (CDC) 支持 | Linux 上的 SQL Server 2019 现在支持变更数据捕获 (CDC)。 |
| &nbsp; | &nbsp; |

## <a id="ml"></a>SQL Server 机器学习服务

|新增功能或更新 | 详细信息 |
|:---|:---|
|基于分区的建模|使用添加到 `sp_execute_external_script` 的新参数来处理每个数据分区的外部脚本。 此功能支持训练多个小型模型（每个数据分区一个模型）而不是一个大型模型。 请参阅[创建基于分区的模型](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)|
|Windows Server 故障转移群集| 在 Windows Server 故障转移群集上配置机器学习服务的高可用性。|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| 新增功能或更新 | 详细信息 |
|:---|:---|
|支持 Azure SQL 数据库托管实例数据库。| 在托管实例上承载 [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]。 请参阅[[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]安装和配置](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb)。|
|新 HTML 控件| HTML 控件替换了所有以前的 Silverlight 组件。 已删除 Silverlight 依赖项。|
| &nbsp; | &nbsp; |

## <a name="analysis-services"></a>Analysis Services

| 新增功能或更新 | 详细信息 |
|:---|:---|
|查询交叉| 请参阅[查询交错](https://docs.microsoft.com/analysis-services/tabular-models/query-interleaving) |
|通过计算组提供对表格模型的 MDX 查询支持 | 请参阅[计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|表格模型中的计算组| [表格模型中的计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|通过计算组提供对表格模型的 MDX 查询支持 | 请参阅[计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|使用计算组动态设置度量值的格式 |通过此功能，可使用[计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)有条件地更改度量值的格式字符串。 例如，通过货币转换，可以使用不同的外币格式显示度量值。|
|表格模型中的多对多关系|[表格模型中的多对多关系](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|资源管理的属性设置|[资源管理的属性设置](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| Power BI 缓存刷新的调控设置。  | Power BI 服务缓存 Live Connect 报告初始加载的仪表板磁贴数据和报告数据，导致向 SSAS 提交的缓存查询数目过多，在极端情况下导致服务器超载。 此版本引入了“ClientCacheRefreshPolicy”属性  。 此属性可用于替代此服务器级别的行为。 有关详细信息，请参阅[常规属性](https://docs.microsoft.com/analysis-services/server-properties/general-properties)。 |
| 联机附加  | 使用此功能，能够以联机操作的形式附加表格模型。 联机附加可用于本地查询横向扩展环境中只读副本的同步。 有关详细信息，请参阅[联机附加](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)。 |
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

有关从支持中排除的特定功能，请参阅[发行说明](sql-server-ver15-release-notes.md)。

此外，还为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 新增或增强了以下功能。

## <a name="see-also"></a>另请参阅

- [`SqlServer` PowerShell 模块](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 文档](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>后续步骤

- [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 发行说明] (sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：技术白皮书](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />于 2018 年 9 月发布。 适用于面向 Windows、Linux 和 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
