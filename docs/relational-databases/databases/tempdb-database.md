---
title: tempdb 数据库 | Microsoft Docs
description: 本主题提供有关在 SQL Server 和 Azure SQL 数据库中配置和使用 tempdb 数据库的详细信息
ms.custom: P360
ms.date: 02/14/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 65a1afa2bf72c53f2ce656afb7f397dd10be9ef6
ms.sourcegitcommit: 01e17c5f1710e7058bad8227c8011985a9888d36
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56265364"
---
# <a name="tempdb-database"></a>tempdb 数据库

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

tempdb 系统数据库是一个全局资源，可供连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或 SQL 数据库的所有用户使用。 tempdb 用于保留：  
  
- 显式创建的临时用户对象，例如：全局或局部临时表及索引、临时存储过程、表变量、表值函数返回的表或游标。  
- 由数据库引擎创建的内部对象。 其中包括：
  - 用于储存假脱机、游标、排序和临时大型对象 (LOB) 存储的中间结果的工作表。
  - 用于哈希联接或哈希聚合操作的工作文件。
  - 用于创建或重新生成索引等操作（如果指定了 SORT_IN_TEMPDB）的中间排序结果，或者某些 GROUP BY、ORDER BY 或 UNION 查询的中间排序结果。

  > [!NOTE]
  > 每个内部对象至少使用九页；一个 IAM 页，一个八页的区。 有关页和区的详细信息，请参阅[页和区](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents)。
  > [!IMPORTANT]
  > Azure SQL 数据库单一数据库和弹性池支持存储在 tempdb 中并且作用域为数据库级别的全局临时表和全局临时存储过程。 全局临时表和全局临时存储过程供同一 Azure SQL 数据库中的所有用户会话共享。 其他 Azure SQL 数据库中的用户会话无法访问全局临时表。 有关详细信息，请参阅[数据库作用域内全局临时表（Azure SQL 数据库）](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database)。 [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)与 SQL Server 支持相同的临时对象。
  > 对于 Azure SQL 数据库单一数据库和弹性池，仅 master 数据库和 tempdb 数据库适用。 有关详细信息，请参阅[什么是 Azure SQL 数据库服务器](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server)。 有关 Azure SQL 数据库单一数据库和弹性池上下文中 tempdb 的讨论，请参阅 [Azure SQL 数据库单一数据库和弹性池中的 tempdb 数据库](#tempdb-database-in-sql-database)。 对于 Azure SQL 数据库托管实例，所有系统数据库都适用。

- 版本存储区是数据页的集合，它包含支持使用行版本控制的功能所需的数据行。 共有两个版本存储区：公用版本存储区和联机索引生成版本存储区。 版本存储区包含：
  - 由使用已提交读（使用行版本控制隔离或快照隔离事务）的数据库中数据修改事务生成的行版本。  
  - 由数据修改事务为实现联机索引操作、多个活动的结果集 (MARS) 以及 AFTER 触发器等功能而生成的行版本。  
  
**tempdb** 中的操作是最小日志记录操作，以便回滚事务。 每次启动**时都会重新创建** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，从而在系统启动时总是具有一个干净的数据库副本。 在断开联接时会自动删除临时表和存储过程，并且在系统关闭后没有活动连接。 因此 **tempdb** 中不会有什么内容从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话保存到另一个会话。 不允许对 **tempdb**进行备份和还原操作。  
  
## <a name="physical-properties-of-tempdb-in-sql-server"></a>SQL Server 中 tempdb 的物理属性

下表列出了 SQL Server 中 tempdb 数据和日志文件的初始配置值（基于模型数据库的默认设置）。 对于不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，这些文件的大小可能略有不同。  
  
|文件|逻辑名称|物理名称|初始大小|文件增长|  
|----------|------------------|-------------------|------------------|-----------------|  
|主数据|tempdev|tempdb.mdf|8 MB|以 64 MB 的速度自动增长直到磁盘已满|  
|次要数据文件*|temp#|tempdb_mssql_#.ndf|8 MB|以 64 MB 的速度自动增长直到磁盘已满|  
|日志|templog|templog.ldf|8 MB|以 64 MB 的速度自动增长直到达到上限 2 TB|  
  
\*文件数取决于计算机上的（逻辑）处理器数。 一般而言，如果逻辑处理器数目小于或等于 8，则使用的数据文件数与逻辑处理器数相同。 如果逻辑处理器数目大于 8，则使用 8 个数据文件，如果仍然存在争用，则以 4 的倍数增加数据文件的数量，直到争用减少到可接受的级别或对工作负荷/代码进行更改。

> [!NOTE]
> 数据文件数的默认值遵循 [KB 2154845](https://support.microsoft.com/kb/2154845/)中的一般准则。  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>在 SQL Server 中移动 tempdb 数据和日志文件

若要移动 **tempdb** 数据和日志文件，请参阅 [移动系统数据库](../../relational-databases/databases/move-system-databases.md)。  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>SQL Server 中 tempdb 的数据库选项

下表列出了 **tempdb** 数据库中每个数据库选项的默认值，以及是否可以修改该选项。 若要查看这些选项的当前设置，请使用 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目录视图。  
  
|数据库选项|默认值|是否可修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|是|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT|GLOBAL|是|  
|数据库可用性选项|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|MIXED_PAGE_ALLOCATION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|对于新安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，为 CHECKSUM。<br /><br /> 对于升级的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，为 NONE。|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|否|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 选项|ENABLE_BROKER|是|  
|TRUSTWORTHY|OFF|否|  
  
有关这些数据库选项的说明，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
## <a name="tempdb-database-in-sql-database"></a>SQL 数据库中的 Tempdb 数据库

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>基于 DTU 的服务层的 tempdb 大小

|SLO|最大 Tempdb 数据文件大小 (GB)|tempdb 数据文件数|最大 tempdb 数据大小 (GB)|
|---|---:|---:|---:|
|“基本”|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|高级弹性池（所有 DTU 配置）|13|12|156|
|标准弹性池 (S0-S2)|13|12|156|
|标准弹性池（S3 及更高版本） |32|12|384|
|基本弹性池（所有 DTU 配置）|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>基于 vCore 的服务层的 tempdb 大小

请参阅[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits)

## <a name="restrictions"></a>限制

不能对 **tempdb** 数据库执行以下操作：  
  
- 添加文件组
- 备份或还原数据库
- 更改排序规则。 默认排序规则为服务器排序规则
- 更改数据库所有者。 tempdb 的所有者是 sa
- 创建数据库快照
- 删除数据库
- 从数据库中删除 guest 用户
- 启用变更数据捕获
- 参与数据库镜像
- 删除主文件组、主数据文件或日志文件
- 重命名数据库或主文件组
- 运行 DBCC CHECKALLOC
- 运行 DBCC CHECKCATALOG
- 将数据库设置为 OFFLINE
- 将数据库或主文件组设置为 READ_ONLY
  
## <a name="permissions"></a>Permissions

任何用户都可以在 tempdb 中创建临时对象。 用户只能访问自己的对象，除非他们获得更多的权限。 可以撤消对 tempdb 的连接权限以阻止用户使用 tempdb，但是不建议这样做，因为一些例行操作需要使用 tempdb。  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>在 SQL Server 中优化 tempdb 性能

tempdb 数据库的大小和物理位置可能会影响系统的性能。 例如，如果定义的 tempdb 大小过小，那么每次重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，都可能会占用部分系统处理负载，让 tempdb 自动增长到支持工作负载所需的大小。

如果可以，请使用[数据库即时文件初始化](../../relational-databases/databases/database-instant-file-initialization.md)来提高数据文件增长操作的性能。

通过将文件大小设置为足够容纳环境中典型工作负荷的值来预分配所有 tempdb 文件的空间。 预先分配可避免 tempdb 因扩展得过于频繁而影响性能。 tempdb 数据库应设置为自动增长，但是在出现意外情况时此设置将用于增加磁盘空间。

每个[文件组](../../relational-databases/databases/database-files-and-filegroups.md#filegroups)中的数据文件应大小一致，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用比例填充算法，这种算法可增加可用空间，便于文件分配。 将 tempdb 分割成大小相等的多个数据文件，可以为使用 tempdb 的操作提供更高的并行效率。

将文件增量设置为合理的大小以避免 tempdb 数据库文件的增量过小。 如果文件的增量与写入 tempdb 的数据量相比过小，则 tempdb 可能需要不断扩大，并且会影响性能。

要检查当前 tempdb 大小和增长参数，请使用以下查询：

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

将 tempdb 数据库放置在快速 I/O 子系统中。 如果有许多直接连接的磁盘，则请使用磁盘条带化。 单个或成组的 tempdb 数据文件并不一定要位于不同的磁盘或主轴上，除非存在 I/O 瓶颈。

将 tempdb 数据库放置在用户数据库使用的磁盘以外的磁盘中。

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>SQL Server 中 tempdb 的性能提高

从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，已通过以下方式进一步优化 tempdb 性能：  
  
- 已缓存的临时表和表变量。 缓存允许删除和创建临时对象的操作非常快速地执行，并减少页分配的争用问题。  
- 改进了分配页闩锁协议，减少了所用 UP（更新）闩锁的数量。  
- 减少了 tempdb 的日志记录开销，从而减少了 tempdb 日志文件的磁盘 I/O 带宽消耗。  
- 在新的实例安装过程中，安装程序会添加多个 tempdb 数据文件。 可以使用“数据库引擎配置”部分中新增的 UI 输入控件和命令行参数 /SQLTEMPDBFILECOUNT 来完成此任务。 默认情况下，安装程序添加的 tempdb 数据文件数为逻辑处理器计数或 8，以较小者为准。  
- 如果有多个 tempdb 数据文件，那么所有文件都会同时自动增长相同的量，具体取决于增长设置。 不再需要跟踪标志 1117。  
- **tempdb** 中的所有分配使用统一盘区。 不再需要[跟踪标志 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
- 对于主文件组，AUTOGROW_ALL_FILES 属性已启用，且不能修改此属性。

要详细了解 tempdb 中的性能改进，请参阅以下博客文章：

[TEMPDB - 文件和跟踪标志以及更新，天哪！](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/)

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>SQL Server 中的 tempdb 容量规划

确定 tempdb 在 SQL Server 生产环境中的适当大小取决于多种因素。 如本文中前面所述，这些因素包括现有工作负荷以及使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 建议你通过在 SQL Server 测试环境中执行下列任务来分析现有的工作负荷：

- 设置 tempdb 的自动增长。
- 执行单独的查询或工作负荷跟踪文件，并监视 tempdb 空间使用。
- 执行索引维护操作（例如重新生成索引），并监视 tempdb 空间。
- 使用前面步骤中的空间使用值来预测总的工作负荷使用情况；针对计划的并发活动调整此值，然后相应地设置 tempdb 的大小。

## <a name="how-to-monitor-tempdb-use"></a>如何监视 tempdb 的使用

如果 tempdb 中磁盘空间不足，则可能会严重破坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生产环境，并会使正在运行的应用程序无法完成操作。 可以使用 [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 动态管理视图来监视 tempdb 文件中使用的磁盘空间：

```sql
 -- Determining the Amount of Free Space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

此外，若要在会话级或任务级监视 tempdb 中的页分配或页释放活动，可以使用 [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) 和 [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) 动态管理视图。 这些视图可用于标识使用 tempdb 中大量磁盘空间的大型查询、临时表或表变量。 还可以使用若干个计数器来监视 tempdb 中的可用空间以及正在使用 tempdb 的资源。 有关详细信息，请参阅下一节。

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>相关内容

- [用于索引的 SORT_IN_TEMPDB 选项](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
- [系统数据库](../../relational-databases/databases/system-databases.md)  
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [移动数据库文件](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>另请参阅

- [在 SQL Server 2005 中使用 tempdb](https://technet.microsoft.com/library/cc966545.aspx)  
- [解决 tempdb 中磁盘空间不足的问题](https://msdn.microsoft.com/library/ms176029.aspx)
