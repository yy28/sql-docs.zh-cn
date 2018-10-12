---
title: SQL Server 2019 中的新增功能 | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68a872164528bec49b0342f603107fb86e31fe50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678265"
---
# <a name="whats-new-in-sql-server-2019"></a>SQL Server 2019 中的新增功能

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] 在早期版本的基础上构建，旨在将 SQL Server 发展成一个平台，以提供开发语言、数据类型、本地或云以及操作系统选项。 本文汇总了 SQL Server 2019 的新增功能。 有关详细信息和已知问题，请参阅 [SQL Server 2019 发行说明](sql-server-ver15-release-notes.md)。

试用 SQL Server 2019！
- [![从评估中心下载](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [下载 SQL Server 2019 以在 Windows 上安装](http://go.microsoft.com/fwlink/?LinkID=862101)
- 在 Linux 上针对 [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md) 安装。
- [在 Docker 上运行 SQL Server 2019](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-20"></a>CTP 2.0 

社区技术预览版 (CTP) 2.0 是 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] 的第一个公开发行版。 以下是 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] CTP 2.0 的新增功能或增强功能。

- [大数据群集](#bigdatacluster)
  - 在 Kubernetes 上部署带 SQL 和 Spark Linux 容器的大数据群集
  - 从 HDFS 访问大数据
  - 使用 Spark 运行高级分析和机器学习
  - 使用 Spark 将数据流式传输到 SQL 数据池
  - 使用 Azure Data Studio 运行提供 notebook 体验的查询书籍

- [数据库引擎](#databaseengine)
  - UTF-8 支持
  - 可恢复联机索引创建允许索引创建，以在发生中断后恢复
  - 聚集列存储联机索引生成和重新生成
  - 具有安全 Enclave 的 Always Encrypted
  - 智能查询处理
  - Java 语言可编程性扩展
  - SQL 图形功能
  - 针对联机和可恢复 DDL 操作的数据库范围的配置设置
  - AlwaysOn 可用性组 - 辅助副本连接重定向
  - 数据发现和分类 - 本机内置于 SQL Server
  - 对永久性内存设备的扩展支持
  - 支持 `DBCC CLONEDATABASE` 中的列存储统计信息
  - 向 `sp_estimate_data_compression_savings` 添加的新选项
  - SQL Server 机器学习服务故障转移群集
  - 默认情况下启用轻量查询分析基础结构
  - 新 Polybase 连接器
  - 新 `sys.dm_db_page_info` 系统函数返回页面信息

- [Linux 上的 SQL Server](#sqllinux)
  - 复制支持
  - 支持 Microsoft 分布式事务处理协调器 (MSDTC)
  - Docker 容器上使用 Kubernetes 的 AlwaysOn 可用性组
  - OpenLDAP 支持第三方 AD 提供商
  - Linux 上的机器学习
  - 新建容器注册表
  - 新的基于 RHEL 的容器映像
  - 内存压力通知

- [Master Data Services](#mds)
  - 已替换 Silverlight 控件

- [Security](#security)
  - SQL Server 配置管理器中的证书管理

- [工具](#tools)
  - SQL Server Management Studio (SSMS) 18.0（预览版）
  - Azure Data Studio

请继续阅读了解有关这些功能的详细信息。

## <a id="bigdatacluster"></a>大数据群集

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [大数据群集](../big-data-cluster/big-data-cluster-overview.md)支持新方案，包括以下内容：

- 在 Kubernetes 上部署带 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Spark Linux 容器的大数据群集
- 从 HDFS 访问大数据
- 使用 Spark 运行高级分析和机器学习
- 使用 Spark 将数据流式传输到 SQL 数据池
- 在 [Azure Data Studio](../sql-operations-studio/what-is.md) 中运行提供 notebook 体验的查询书籍。
  
[!INCLUDE [Big Data Clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 数据库引擎

CTP 2.0 引入或增强以下 [!INCLUDE[ssdeNoVersion](../includes/ssdenoversion_md.md)] 新功能。

### <a name="database-compatibility-level"></a>Database 兼容级别

已添加数据库“COMPATIBILITY_LEVEL 150”。 若要启用特定用户数据库，请执行：

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support"></a>UTF-8 支持

完全支持广泛使用的 UTF-8 字符编码作为导入或导出编码，或作为文本数据的数据库级或列级排序规则。 `CHAR` 和 `VARCHAR` 数据类型中允许 UTF-8，并在创建对象的排序规则或将其更改为带 `UTF8` 后缀的排序规则时启用。 

例如：将 `LATIN1_GENERAL_100_CI_AS_SC` 更改为 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 仅适用于支持增补字符的 Windows 排序规则，如 SQL Server 2012 中所引入的。 `NCHAR` 和 `NVARCHAR` 仅允许 UTF-16 编码，并保持不变。

此功能可能会节省大量存储空间，具体取决于正在使用的字符集。 例如，使用已启用 UTF-8 的排序规则将带 ASCII 字符串的现有列数据类型从 `NCHAR(10)` 更改为 `CHAR(10)`，意味着将减少近 50% 的存储需求。 存储需求减少是因为 `NCHAR(10)` 需要 22 个字节进行存储，而 `CHAR(10)` 需要 12 个字节存储相同的 Unicode 字符串。

### <a name="resumable-online-index-create"></a>可恢复联机索引创建

- 可恢复联机索引创建允许索引创建操作暂停并稍后从操作暂停或失败的位置恢复，而不是从头开始重新启动。

  可恢复联机索引创建支持以下方案：
  - 在索引创建失败后恢复索引创建操作，例如在数据库故障转移后或磁盘空间不足后。
  - 暂停正在进行的索引创建操作并稍后恢复，以便根据需要允许暂时释放系统资源，并稍后恢复此操作。
  - 在无需使用过多日志空间和阻止其他维护活动的长时间运行事务以及不允许日志截断的情况下创建大型索引。

  如果没有此功能，当索引创建失败，则必须再次执行联机索引创建操作，且必须从头开始重新启动该操作。

在此版本中，我们将扩展可恢复功能，以将此功能添加到可用的[可恢复联机索引重新生成](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)。

此外，可以使用[面向联机和可恢复 DDL 操作的数据库范围的默认设置](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)，将此功能设置为特定数据库的默认设置。

有关详细信息，请参阅[可恢复联机索引创建](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)。

### <a name="build-and-rebuild-clustered-columnstore-indexes-online"></a>生成和重新生成聚集列存储索引联机

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

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted

使用就地加密和丰富计算来扩展 Always Encrypted。 扩展来自在服务器端的安全 enclave 内对纯文本数据启用计算。

加密操作包括列加密和列加密密钥轮换。 现在可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 来发布这些操作，并且它们不需要将该数据移出数据库。 安全 enclave 向一组更广泛的方案提供 Always Encrypted，包括以下两个要求：  

- 其中一个要求是保护敏感数据，以防具有高特权但未经授权的用户对其进行访问，包括数据库管理员、系统管理员、云操作员或恶意软件。
- 另一个要求是数据库系统支持对受保护数据的丰富计算。

有关详细信息，请参阅[具有安全 Enclave 的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。

> [!NOTE]
> 具有安全 enclave 的 Always Encrypted 仅可在 Windows OS 上使用。

### <a name="intelligent-query-processing"></a>智能查询处理

- 通过调整批处理模式和行模式运算符的内存授予大小，行模式内存授予反馈扩展了 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中引入的内存授予反馈功能。  对于内存授予过量的情况，如果授予的内存是实际使用内存大小的两倍，内存授予反馈将重新计算内存授予。 然后，连续执行将请求更少的内存。 对于造成到磁盘的溢出的大小不足的内存授予，内存授予反馈将触发重新计算内存授予。 然后，连续执行将请求更多的内存。 在数据库兼容性级别 150 下默认启用此功能。

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

- 表变量延迟编译功能提升了计划质量和引用表变量的查询的整体性能。 在优化和初始编译期间，此功能会传播基于实际表变量行计数的基数估计。  这种准确的行计数信息将用于优化下游计划操作。 在数据库兼容性级别 150 下默认启用此功能。

若要使用智能查询处理功能，设置数据库 `COMPATIBILITY_LEVEL = 150`。

### <a id="programmability"></a> Java 语言可编程性扩展

- Java 语言扩展（预览版）：使用 Java 语言扩展来执行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 Java 代码。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，向 SQL Server 实例添加“机器学习服务（数据库内）”功能时，将安装此扩展。

### <a id="sqlgraph"></a> SQL 图形功能

- 与 `MERGE` DML 中的支持匹配允许你指定单个语句中的图形关系，而不是单独的 `INSERT`、`UPDATE` 或 `DELETE` 语句。 使用 `MERGE` 语句中的 `MATCH` 谓词将节点或边界表中的当前图形数据与新数据合并。 此功能启用边界表上的 `UPSERT` 方案。 用户现在可以使用单个合并语句在两个节点之间插入一个新的边界或更新现有边界。

- 对 SQL 图形中的边界表引入了边缘约束。 边界表可以将任何节点连接到数据库中的任何其他节点。 引入边缘约束后，现在可以对此行为应用一些限制。 新 `CONNECTION` 约束可用于指定将允许给定边缘表在架构中连接的节点类型。

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations"></a>针对联机和可恢复 DDL 操作的数据库范围的默认设置 

- 联机和可恢复 DDL 操作的数据库范围的默认设置允许对数据库级别的 `ONLINE` 和 `RESUMABLE` 的默认行为设置，而不是为每个单独的索引 DDL 语句（比如 index create 或 rebuild）定义这些选项。

- 使用 `ELEVATE_ONLINE` 和 `ELEVATE_RESUMABLE` 数据库范围的配置选项设置这些默认值。 这两个选项都会导致引擎自动将支持操作提升为索引联机或可恢复执行。 可以使用这些选项启用以下行为：

  - `FAIL_UNSUPPORTED` 选项允许所有联机或可恢复的索引操作，并使不支持联机或可恢复的索引操作失败。
  - `WHEN_SUPPPORTED` 选项允许支持的联机或可恢复操作并运行索引不支持的脱机或不可恢复操作。
  - `OFF` 选项允许执行所有脱机且不可恢复索引操作的当前行为，除非在 DDL 语句中显式指定。

若要替代默认设置，请在 index create 和 rebuild 命令中包含“联机”或“可恢复”选项。  

如果没有此功能，则必须直接在索引 DDL 语句（如 index create 和 rebuild）中指定“联机”和“可恢复”选项。

详细信息：有关可恢复的索引操作的详细信息，请参阅[可恢复联机索引创建](http://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/)。

### <a id="ha"></a>AlwaysOn 可用性组 - 更多同步副本 

- 最多五个同步副本：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 将同步副本的最大数目从 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中的 3 增加到 5。 可以配置此组的 5 个副本在该组中进行自动故障转移。 有 1 个主要副本，以及 4 个同步的次要副本。

- 次要副本到主要副本连接重定向：它允许客户端应用程序连接定向到主要副本，而不考虑在连接字符串中指定的目标服务器。 此功能允许在不使用侦听器的情况下进行连接重定向。 在以下情况下使用次要副本到主要副本连接重定向：

  - 群集技术不提供侦听器功能。
  - 重定向较为复杂的多子网配置。
  - 读取扩展或灾难恢复场景，其群集类型为 `NONE`。

有关详细信息，请参阅[次要副本到主要副本读/写连接重定向（AlwaysOn 可用性组）](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。

### <a name="data-discovery-and-classification"></a>数据发现和分类

数据发现和分类提供本机内置于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的高级功能。 对最敏感的数据进行分类和标记提供以下优势：
- 帮助满足数据隐私标准和法规遵从性要求。
- 支持安全方案，如监视（审核），以及对敏感数据异常访问的警报。
- 可以更轻松地识别企业中敏感数据所在的位置，以便管理员采取正确措施来保护数据库。

有关详细信息，请参与 [SQL 数据发现和分类](../relational-databases/security/sql-data-discovery-and-classification.md)。

对[审核](../relational-databases/security/auditing/sql-server-audit-database-engine.md)进行了强化处理，在审核日志中包含了名为 `data_sensitivity_information` 的新字段，其中记录查询返回的实际数据的敏感度分类（标签）。 有关详细信息和示例，请参阅[添加敏感度分类](../t-sql/statements/add-sensitivity-classification-transact-sql.md)。

>[!NOTE]
>就审核启用方式方面没有任何更改。 在审核日志中包含了新字段 `data_sensitivity_information`，该字段记录查询返回的实际数据的敏感度分类（标签）。 请参阅[审核对敏感数据的访问](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3)。

### <a name="expanded-support-for-persistent-memory-devices"></a>对永久性内存设备的扩展支持

任何置于永久性内存设备上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件现在都可以在启用模式下运行。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 直接访问设备，使用高效的 memcpy 操作绕过操作系统的存储堆栈。 此模式可以提高性能，因为它允许针对此类设备的低延迟输入/输出。
    - 示例 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 文件包括：
        - 数据库文件
        - 事务日志文件
        - 内存中 OLTP 检查点文件
    - 永久性内存也称为“存储类内存”。
    - 在一些非 Microsoft 网站上，永久性内存有时会通俗地称为“pmem”。

> [!NOTE]
> 对于此预览版，永久性内存设备上的文件启用只在 Linux 上可用。 Windows 上的 SQL Server 支持从 SQL Server 2016 开始的永久性内存设备。

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase"></a>支持 DBCC CLONEDATABASE 中的列存储统计信息

`DBCC CLONEDATABASE` 创建仅限架构的数据库副本，其中包括在不复制数据的情况下对查询性能问题进行故障排除所需的所有元素。  在以前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，该命令不会复制所需的统计信息来准确地对列存储索引查询进行故障排除，且需要手动步骤来捕获此信息。 现在，在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，DBCC CLONEDATABASE 自动捕获列存储索引的统计信息 blob，因此不再需要任何手动步骤。

### <a name="new-options-added-to-spestimatedatacompressionsavings"></a>添加到 sp_estimate_data_compression_savings 的新选项

`sp_estimate_data_compression_savings` 返回所请求对象的当前大小并估算对象在所请求的压缩状态下的大小。  此过程当前支持三个选项：`NONE`、`ROW` 和 `PAGE`。 SQL Server 2019 引入了两个新选项：`COLUMNSTORE` 和 `COLUMNSTORE_ARCHIVE`。 如果使用标准或存档列存储压缩在表中创建列存储索引，可以使用这些新选项来估计节省的空间。

### <a id="ml"></a> SQL Server 机器学习服务故障转移群集和基于分区的建模

- 基于分区的建模：使用添加到 `sp_execute_external_script` 的新参数来处理每个数据分区的外部脚本。 此功能支持训练多个小型模型（每个数据分区一个模型）而不是一个大型模型。

- Windows Server 故障转移群集：在 Windows Server 故障转移群集上配置机器学习服务的高可用性。

有关详细信息，请参阅 [SQL Server 机器学习服务中的新增功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default"></a>默认情况下启用轻量查询分析基础结构

相比标准分析技术，轻量查询分析基础结构 (LWP) 能够更有效地提供查询性能数据。 现在，默认情况下启用轻量分析。 已在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 中引入此功能。 轻量分析提供查询执行统计信息集合机制，预期开销为 2% CPU，而标准查询分析机制的开销高达 75% CPU。 在早期版本中，默认禁用此功能。 数据库管理员可通过[跟踪标志 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 来启用它。 

有关轻量分析的详细信息，请参阅[开发人员选择：随时随地查询进度](http://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)。

### <a id="polybase"></a> 新 Polybase 连接器

- 面向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的新连接器：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的外部数据引入了新连接器。

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information"></a>新 sys.dm_db_page_info 系统函数返回页面信息

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

- 复制支持：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支持 Linux 上的 SQL Server 复制。 使用 SQL 代理的 Linux 虚拟机可以是发布服务器、分发服务器上或订阅服务器。 

  创建以下类型的发布：
  - 事务性
  - 快照
  - 合并

  配置复制 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或使用[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

- 支持 Microsoft 分布式事务处理协调器 (MSDTC)：Linux 上的 SQL Server 2019 支持 Microsoft 分布式事务处理协调器 (MSDTC)。 有关详细信息，请参阅[如何在 Linux 上配置 MSDTC](../linux/sql-server-linux-configure-msdtc.md)。

- Docker 容器上使用 Kubernetes 的 AlwaysOn 可用性组：Kubernetes 可以协调运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的容器，以提供一组高度可用的数据库，其中包含 SQL Server AlwaysOn 可用性组。 Kubernetes 运算符部署一个 StatefulSet，其中包括带 mssql-server container 的容器和运行状况监视器。

- **OpenLDAP 支持第三方 AD 提供商**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支持 OpenLDAP，以便第三方提供商加入 Active Directory。

- Linux 上的机器学习：Linux 现支持 SQL Server 2019 机器学习服务（数据库内）。 支持包括 `sp_execute_external_script` 存储过程。 有关如何在 Linux 上安装机器学习服务的说明，请参阅[在 Linux 上安装 SQL Server 2019 机器学习服务 R 和 Python 支持](../linux/sql-server-linux-setup-machine-learning.md)。

- 新容器注册表：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的所有容器映像现在均位于 Microsoft 容器注册表。 Microsoft 容器注册表是用于分发 Microsoft 产品容器的官方容器注册表。 此外，现发布了已认证的基于 RHEL 映像。

  - Microsoft 容器注册表：`mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 经认证的基于 RHEL 的容器映像：`mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> Master Data Services (MDS)

- 用 HTML 替代 Silverlight 控件：Master Data Services (MDS) 门户不再依赖 Silverlight。 所有以前的 Silverlight 组件均已替换为 HTML 控件。

## <a id="security"></a>安全性

- SQL Server 配置管理器中的证书管理：SSL/TLS 证书被广泛用于保护对 SQL Server 实例的访问。 证书管理现已集成到 SQL Server 配置管理器，以简化诸如以下常见任务：

  - 查看和验证安装在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上的证书。 
  - 查看即将到期的证书。
  - 在参与到 AlwaysOn 可用性组的机器之间部署证书（从包含主要副本的节点）。
  - 在参与到故障转移群集实例的机器之间部署证书（从活动节点）。

  > [!NOTE]
  > 用户必须拥有所有群集节点的管理员权限。

## <a id="tools"></a>工具

- [Azure Data Studio](../azure-data-studio/what-is.md)：此前以预览版名称 SQL Operations Studio 发布，Azure Data Studio 是一个轻量、新式、开源的跨平台桌面工具，用于数据开发和管理中的最常见任务。 使用 Azure Data Studio，可以在 Windows、macOS 和 Linux 上连接到本地和云中的 SQL Server。 使用 Azure Data Studio，可以：

  - 在现代开发环境中使用快如闪电的 Intellisense、代码段和源代码管理集成编辑和运行查询。  
  - 快速使用结果集的内置图表来可视化数据。  
  - 使用可自定义小组件为服务器和数据库创建自定义仪表板。  
  - 使用内置终端轻松管理更广泛的环境。  
  - 在基于 Jupyter 构建的集成 notebook 体验中分析数据。  
  - 使用自定义主题和扩展增强体验。  
  - 并通过内置订阅和资源浏览器探索 Azure 资源。
  - 支持使用 SQL Server 大数据群集方案。


- [SQL Server Management Studio (SSMS) 18.0（预览版）](../ssms/sql-server-management-studio-ssms.md)

  - 支持 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。
  - 支持具有安全 enclave 的 Always Encrypted。
  - 减小了下载大小。
  - 现基于 Visual Studio 2017 独立 Shell。
  - 有关完整列表，请参阅 [SSMS 更改日志](../ssms/sql-server-management-studio-changelog-ssms.md)。

## <a name="other-services"></a>其他服务

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 不会为以下服务引入新功能：

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>后续步骤

- [SQL Server 2019 发行说明](sql-server-ver15-release-notes.md)

- [Microsoft SQL Server 2019：技术白皮书](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />于 2018 年 9 月发布。 适用于面向 Windows、Linux 和 Docker 容器的 Microsoft SQL Server 2019 CTP 2.0。


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
