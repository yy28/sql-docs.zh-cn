---
title: SQL Server 2019 中的新增功能 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2ded17c5baf35949b16c173236f94f8d0d3dd299
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028914"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新增功能

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 在早期版本的基础上构建，旨在将 SQL Server 发展成一个平台，以提供开发语言、数据类型、本地或云以及操作系统选项。

本文总结了 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和增强功能。

有关详细信息和已知问题，请参阅 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 发行说明](sql-server-ver15-release-notes.md)。

使用[最新工具](what-s-new-in-sql-server-ver15-prerelease.md#tools)获得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳体验  。

## <a name="ctp-32-july-2019"></a>CTP 3.2 2019 年 7 月

社区技术预览版 (CTP) 3.2 是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最新公开发行版。 此版本包含来自 CTP 历史版本的改进功能，可修复 bug、增强安全性和优化性能。 有关 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 之前的每个 CTP 版本中的新功能和改进功能，请参阅 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 公告存档](what-s-new-in-sql-server-ver15-prerelease.md)。

### <a name="new-in-big-data-clusters"></a>大数据群集中的新增功能

|新增功能或更新 | 详细信息 |
|:---|:---|
|公共预览版 |在 CTP 3.2 之前，已向已注册的早期采用者提供 SQL Server 大数据群集。 此版本允许任何人体验 SQL Server 大数据群集的功能。 <br/><br/> 请参阅[开始使用 SQL Server 大数据群集](../big-data-cluster/deploy-get-started.md)。|
|`azdata` |CTP 3.2 引入了 `azdata`，这是一个使用 Python 编写的命令行实用程序，可让群集管理员通过 REST API 启动和管理大数据群集。 `azdata` 替换了 `mssqlctl`。 请参阅[安装 `azdata`](../big-data-cluster/deploy-install-azdata.md)。 |
|PolyBase |外部表列名现可用于查询 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 数据源。 在以前的 CTP 版本中，仅基于目标上的序号绑定列，未使用外部表定义中的列名。|
|HDFS 分层刷新 |引入了 HDFS 分层刷新功能，可刷新远程数据最新快照的现有装载。 请参阅 [HDFS 分层](../big-data-cluster/hdfs-tiering.md) |
|基于笔记本的故障排除 |CTP 3.2 引入了 Jupyter 笔记本，帮助完成 SQL Server 大数据群集中组件的[部署](../big-data-cluster/deploy-notebooks.md)以及[发现、诊断和故障排除](../big-data-cluster/manage-notebooks.md)。 |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Analysis Services 中的新增功能

| 新增功能或更新 | 详细信息 |
|:---|:---| 
| Power BI 缓存刷新的调控设置。  | Power BI 服务缓存 Live Connect 报告初始加载的仪表板磁贴数据和报告数据，导致向 SSAS 提交的缓存查询数目过多，在极端情况下导致服务器重载。 此版本引入了“ClientCacheRefreshPolicy”属性  。 此属性可用于替代此服务器级别的行为。 有关详细信息，请参阅[常规属性](https://docs.microsoft.com/analysis-services/server-properties/general-properties)。 |
| 联机附加  | 使用此功能，能够以联机操作的形式附加表格模型。 联机附加可用于本地查询横向扩展环境中只读副本的同步。 有关详细信息，请参阅[联机附加](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)。 |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>语言扩展的新增功能

|新增功能或更新 | 详细信息 |
|:---|:---|
| 新默认 Java 运行时  | SQL Server 现在包括 Azul System 的 Zulu Embedded，用于在整个产品中提供 Java 支持。 有关详细信息，请参阅 [Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/)（SQL Server 2019 现已提供免费支持的 Java）。 |

### <a name="new-in-sql-server-on-linux"></a>Linux 上的 SQL Server 的新增功能

|新增功能或更新 | 详细信息 |
|:---|:---|
| 变更数据捕获 (CDC) 支持 | Linux 上的 SQL Server 2019 现在支持变更数据捕获 (CDC)。 |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 功能（按组件）

以下各节重点介绍了早期版本的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中的新组件和增强的功能。

## <a name="big-data-clusters"></a>大数据群集

| 新增功能或更新 | 详细信息 |
|:---|:---|
| 可缩放的大数据解决方案 | [部署](../big-data-cluster/deploy-get-started.md) SQL Server、Spark 和在 Kubernetes 上运行的 HDFS 容器的可缩放群集 <br/><br/> 在 Transact-SQL 或 Spark 中读取、写入和处理大数据<br/><br/> 通过大容量大数据轻松合并和分析高价值关系数据<br/><br/>查询外部数据源<br/><br/>在由 SQL Server 管理的 HDFS 中存储大数据<br/><br/>通过群集查询多个外部数据源的数据<br/><br/> 将数据用于 AI、机器学习和其他分析任务<br/><br/> 在大数据群集中部署和运行应用程序 <br/>|
| &nbsp; | &nbsp; |

有关更多详细信息，请参阅[什么是 SQL Server 大数据群集](../big-data-cluster/big-data-cluster-overview.md)

[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP) 公告存档](what-s-new-in-sql-server-ver15-prerelease.md)中列出了含有此功能的所有先前 CTP 版本中公告和更改的功能。

## <a name="database-engine"></a>数据库引擎

### <a name="security"></a>Security

|新增功能或更新 | 详细信息 |
|:---|:---|
|对加密列创建索引|可以对使用随机加密和已启用 enclave 的密钥加密的列创建索引，以提升丰富查询的性能（使用 `LIKE` 和比较运算符）。 请参阅[包含安全 Enclave 的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。
|暂停和恢复透明数据加密 (TDE) 的初始扫描|请参阅[透明数据加密 (TDE) 扫描 - 暂停和恢复](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|SQL Server 配置管理器中的证书管理|请参阅[证书管理（SQL Server 配置管理器）](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |


### <a name="graph"></a>图形

|新增功能或更新 | 详细信息 |
|:---|:---|
|边缘约束级联删除操作 |在图形数据库中，在边缘约束上定义级联删除操作。 请参阅[边缘约束](../relational-databases/tables/graph-edge-constraints.md)。 |
|新增图形函数 - `SHORTEST_PATH` | 可以使用 `MATCH` 内的 `SHORTEST_PATH` 来查找图中任意 2 个节点之间的最短路径，或执行任意长度遍历。|
|分区表和索引| 已分区表和已分区索引的数据被划分为多个单元，这些单元可以跨图形数据库中的多个文件组分散。 |
|在图形匹配查询中使用派生表或视图别名 |请参阅[图形边缘约束](../relational-databases/tables/graph-edge-constraints.md)。 |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>索引

|新增功能或更新 | 详细信息 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|可以在数据库引擎内启用优化，有助于提高索引中高并发插入的吞吐量。 此选项旨在用于易发生最后一页插入争用的索引，常见于有顺序键（如标识列、序列或日期/时间列）的索引。 有关详细信息，请参阅 [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)。|
|生成和重新生成联机聚集列存储索引 | 请参阅[联机执行索引操作](../relational-databases/indexes/perform-index-operations-online.md)。 |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>内存中数据库

|新增功能或更新 | 详细信息 |
|:---|:---|
|混合缓冲池的 DDL 控制 |使用[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)，可以在需要时直接访问位于永久性内存 (PMEM) 设备上数据库文件中的数据库页。|
|内存优化 tempdb 元数据|请参阅[内存优化 TempDB 元数据](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>链接服务器

|新增功能或更新 | 详细信息 |
|:---|:---|
|链接服务器支持 UTF-8 字符编码。 |[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|新增功能或更新 | 详细信息 |
|:---|:---|
|PolyBase |外部表列名现可用于查询 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 数据源。 |
| &nbsp; | &nbsp; |

### <a name="collation"></a>排序规则

|新增功能或更新 | 详细信息 |
|:---|:---|
|支持 UTF-8 字符编码 |已为 BIN2 排序规则 (`Latin1_General_100_BIN2_UTF8`) 启用。 请参阅[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md)。 |
|在安装期间默认选择 UTF-8 排序规则 | 请参阅[排序规则和 Unicode 支持](../relational-databases/collations/collation-and-unicode-support.md#ctp23)。 |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>服务器设置

|新增功能或更新 | 详细信息 |
|:---|:---|
|在安装时设置 `MIN` 和 `MAX` 服务器内存值 |可以在安装过程中设置服务器内存值。 使用默认值、计算出的推荐值，或在选择“推荐”  选项（请参阅[服务器内存服务器配置选项](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)）后手动指定你自己的值。|
|SQL Server 安装程序启用了 MAXDOP 设置 |新建议遵循已记录的指南。[配置最大并行度服务器配置选项](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|混合缓冲池| SQL Server 数据库引擎的一项新功能，可以在必要时直接访问位于永久性内存 (PMEM) 设备上的数据库文件上的数据库页。 请参阅[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)。|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>性能监视

|新增功能或更新 | 详细信息 |
|:---|:---|
|标量 UDF 内联 |自动将标量用户定义的函数 (UDF) 转换为关系表达式，并将其嵌入调用 SQL 查询。 请参阅[标量 UDF 内联](../relational-databases/user-defined-functions/scalar-udf-inlining.md)。 |
| `sys.dm_exec_requests` 列 `command` | 如果 `SELECT` 在继续执行查询之前等待同步统计信息更新操作完成，则显示 `SELECT (STATMAN)`。 请参阅 [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 动态管理视图中新的等待类型。 它显示了针对同步统计信息刷新操作耗费的实例级别累计时间。 请参阅 [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|
|查询存储的自定义捕获策略|启用后，在新的“查询存储捕获策略”设置下有额外可用的查询存储配置，可用于微调特定服务器中的数据收集。 有关详细信息，请参阅 [ALTER DATABASE SET 选项](../t-sql/statements/alter-database-transact-sql-set-options.md)。|
|`sys.dm_exec_query_plan_stats` |新的 DMF 返回大多数查询的最后已知实际执行计划的等效项。 请参阅 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)。|
|`LAST_QUERY_PLAN_STATS` | 要启用 `sys.dm_exec_query_plan_stats` 的新数据库范围配置。 请参阅 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|`LIGHTWEIGHT_QUERY_PROFILING`|新数据库范围配置。 请参阅 [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)。 |
|`query_post_execution_plan_profile` | 扩展事件基于轻型分析收集实际执行计划的等效项，与使用标准分析的 `query_post_execution_showplan` 不同。 请参阅[查询分析基础结构](../relational-databases/performance/query-profiling-infrastructure.md)。|
|行模式内存授予反馈。 |[行模式内存授予反馈](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|表变量延迟编译。|[表变量延迟编译](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|近似 `COUNT DISTINCT`。|[近似查询处理](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|行存储上的批处理模式。|[行存储上的批处理模式](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>语言扩展

|新增功能或更新 | 详细信息 |
|:---|:---|
|新 Java 语言 SDK | 简化了可从 SQL Server 运行的 Java 程序的开发。 请参阅 [SQL Server 机器学习服务中的新增功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。 |
|SQL Server 语言扩展 - [Java 语言扩展](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|[Microsoft SQL Server 用于 Java 的 Microsoft 扩展性 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) 目前是开源的，可[在 GitHub 上获取](https://github.com/microsoft/sql-server-language-extensions)。|
|注册外部语言|新的 DDL `CREATE EXTERNAL LANGUAGE` 在 SQL Server 中注册外部语言，如 Java。 请参阅 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。 |
|对 Java 数据类型的支持|请参阅 [Java 数据类型](../language-extensions/how-to/java-to-sql-data-types.md)。|

### <a name="spatial"></a>空间

|新增功能或更新 | 详细信息 |
|:---|:---|
| 新的空间引用标识符 (SRID) |[Australian GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) 提供了更为可靠和准确的数据，这些数据与全球定位系统提供的数据更加接近。 新 SRID 为：<br/><br/> - 7843 - 地理 2D<br/> - 7844 - 地理 3D <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 视图包含新 SRID 的定义。 |
| &nbsp; | &nbsp; |

### <a name="performance"></a>“性能”

|新增功能或更新 | 详细信息 |
|:---|:---|
|加速数据库恢复 | 按数据库启用加速数据库恢复。 请参阅[加速数据库恢复](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)。|
|强制快进和静态游标 | 查询存储计划强制支持快进和静态游标。 请参阅[计划强制支持快进和静态游标](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)。|
|减少了对工作负荷的重新编译| 改进跨多个作用域使用临时表。 请参阅[减少了对工作负荷的重新编译](../relational-databases/tables/tables.md#ctp23) |
|间接检查点可伸缩性 |请参阅[改进了间接检查点可伸缩性](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)。|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>可用性组

|新增功能或更新 | 详细信息 |
|:---|:---|
|最多五个同步副本|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 将同步副本的最大数目从 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中的 3 增加到了 5。 可以配置此组的 5 个副本在该组中进行自动故障转移。 有 1 个主要副本以及 4 个同步的次要副本。|
|次要副本到主要副本连接重定向| 允许客户端应用程序连接定向到主要副本，而不考虑在连接字符串中指定的目标服务器。 有关详细信息，请参阅[次要副本到主要副本读/写连接重定向（AlwaysOn 可用性组）](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。|
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
|Docker 容器上使用 Kubernetes 的 AlwaysOn 可用性组 |[容器的 Always On 可用性组](../linux/sql-server-ag-kubernetes.md) |
|复制支持 |[Linux 上的 SQL Server 复制](../linux/sql-server-linux-replication.md)
|支持 Microsoft 分布式事务处理协调器 (MSDTC) |[如何在 Linux 上配置 MSDTC](../linux/sql-server-linux-configure-msdtc.md) |
|OpenLDAP 支持第三方 AD 提供商 |[教程：对 Linux 上的 SQL Server 使用 Active Directory 身份验证](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux 上的机器学习 |[在 Linux 上配置机器学习](../linux/sql-server-linux-setup-machine-learning.md) |
|Tempdb 改进 | 默认情况下，Linux 上的 SQL Server 新安装会根据逻辑核心数创建多个 tempdb 数据文件（最多 8 个数据文件）。 这不适用于就地次要版本或主版本升级。 每个 tempdb 文件的大小为 8MB，且自动增长大小为 64MB。 此行为类似于 Windows 上的默认 SQL Server 安装。 |
| Linux 上的 PolyBase | 在 Linux 上为非 Hadoop 连接器[安装 PolyBase](../relational-databases/polybase/polybase-linux-setup.md)。<br/><br/>[PolyBase 类型映射](../relational-databases/polybase/polybase-type-mapping.md)。 |
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
|表格模型中的计算组| [表格模型中的计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|通过计算组提供对表格模型的 MDX 查询支持 | 请参阅[计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|使用计算组动态设置度量值的格式 |通过此功能，可使用[计算组](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)有条件地更改度量值的格式字符串。 例如，通过货币转换，可以使用不同的外币格式显示度量值。|
|表格模型中的多对多关系|[表格模型中的多对多关系](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|资源管理的属性设置|[资源管理的属性设置](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

有关从支持中排除的特定功能，请参阅[发行说明](sql-server-ver15-release-notes.md)。

此外，还为 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 新增或增强了以下功能。

## <a name="see-also"></a>另请参阅

- [`SqlServer` PowerShell 模块](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 文档](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>后续步骤

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]发行说明](sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：技术白皮书](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />于 2018 年 9 月发布。 适用于面向 Windows、Linux 和 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
