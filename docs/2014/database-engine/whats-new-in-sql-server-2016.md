---
title: 什么&#39;s 新 （数据库引擎） |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ac9a6a1b2d4107d420bab68659b6d05f25805a38
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067020"
---
# <a name="what39s-new-database-engine"></a>什么&#39;s 新 （数据库引擎）
  这一最新版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]引入了一些新功能和增强功能，这些功能可以提高设计、开发和维护数据存储系统的架构师、开发人员和管理员的能力和工作效率。 以下是[!INCLUDE[ssDE](../includes/ssde-md.md)]已增强的方面。  
  
##  <a name="Feature"></a> 数据库引擎的增强功能  
  
###  <a name="MemoryOpt"></a> 内存优化表  
 内存中 OLTP 是一种内存优化的数据库引擎，它集成到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 引擎中。 内存中 OLTP 已针对 OLTP 进行优化。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
 
  
###  <a name="DataFiles"></a> 在 Windows Azure 中的 SQL Server 数据文件  
 [在 Windows Azure 中的 SQL Server 数据文件](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)可提供本机支持的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库作为 Windows Azure Blob 存储的文件。 通过此功能，您可以在本地或 Windows Azure 中虚拟机上运行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中创建数据库，而将数据存储在 Windows Azure Blob 存储中的专用存储位置。  
  
  
###  <a name="AzureVM"></a> 承载 SQL Server 数据库，在 Windows Azure 虚拟机  
 使用[将 SQL Server 数据库部署到 Windows Azure 虚拟机](http://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx)向导来承载数据库的实例从[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Windows Azure 虚拟机中。  
  
  
###  <a name="Backup"></a> 备份和还原增强功能  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含针对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原的以下增强功能：  
  
-   **SQL Server 备份到 URL**  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份到 URL 功能是在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 中引入的，只有 [!INCLUDE[tsql](../includes/tsql-md.md)]、PowerShell 和 SMO 支持这一功能。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 来备份到 Windows Azure Blob 存储服务或从中还原。 “备份”任务和维护计划都可使用该新选项。 有关详细信息，请参阅[使用 SQL Server Management Studio 中的备份任务](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS)， [SQL Server 备份到 URL 使用的维护计划向导](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz)，和[从 Windows Azure 存储还原使用 SQLServer Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS)。  
  
-   **针对 Microsoft Azure 的 SQL Server 托管备份**  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 是基于 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 备份到 URL 这一功能构建的服务，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供这种服务来管理和安排数据库和日志的备份。 在本版本中，只支持备份到 Windows Azure 存储。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可在数据库和实例级别同时进行配置，从而既能实现在数据库级别的精细控制，又能实现实例级别的自动化。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]既可在本地运行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上配置，也可在 Windows Azure 虚拟机上运行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上配置。 建议对在 Windows Azure 虚拟机上运行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例使用此服务。 有关详细信息，请参阅[SQL Server 托管备份到 Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)。  
  
-   **备份加密**  
  
     您现在可以选择在备份过程中对备份文件进行加密。  目前支持的加密算法包括 AES 128、AES 192、AES 256 和 Triple DES。 要在备份过程中执行加密，您必须使用证书或非对称密钥。 有关详细信息，请参阅[备份加密](../relational-databases/backup-restore/backup-encryption.md)。  
  
  
###  <a name="CE"></a> 新基数估计过程的设计  
 称作基数估计器的基数估计逻辑已重新设计中[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]以便改进查询计划质量，因此若要提高查询性能。 新的基数估计器纳入在新型 OLTP 和数据仓库工作负荷中表现优异的假设和算法。 它基于针对新型工作负荷的深入基数估计研究，以及我们在过去 15 年在改进 SQL Server 基数估计器方面的学习。 客户反馈表明，尽管大多数查询将会从更改或保持不更改中受益，但与以前的基数估计器相比，少数查询可能会显得退步。 性能优化和测试建议，请参阅[基数估计&#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md)。  
   
  
###  <a name="Durability"></a> 延迟持续性  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 将部分或所有事务指定为延迟持久事务，从而能够缩短延迟。 延迟持久事务在事务日志记录写入磁盘之前将控制权归还给客户端。 持续性可在数据库级别、提交级别或原子块级别进行控制。  
  
 有关详细信息，请参阅主题[控制事务持续性](../relational-databases/logs/control-transaction-durability.md)。  
  
  
###  <a name="AlwaysOn"></a> AlwaysOn 增强功能  
 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含针对 AlwaysOn 故障转移群集实例和 AlwaysOn 可用性组的以下增强功能：  
  
-   “添加 Azure 副本向导”简化了用于 AlwaysOn 可用性组的混合解决方案创建。 有关详细信息，请参阅[使用添加 Azure 副本向导&#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md)。  
  
-   辅助副本的最大数目从 4 增加到 8。  
  
-   断开与主副本的连接时，或者在缺少群集仲裁期间，可读辅助副本现在保持可用于读取工作负荷。  
  
-   故障转移群集实例 (FCI) 现在可使用群集共享卷 (CSV) 作为群集共享磁盘。 有关详细信息，请参阅[Alwayson 故障转移群集实例](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   新的系统函数[sys.fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql)，和一个新的 DMV [sys.dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql)，可用。  
  
-   以下 Dmv 已增强，现在返回 FCI 信息： [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)， [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)，并[sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)。  
  
  
###  <a name="OIR"></a> 分区切换和索引  
 现在可以重新生成已分区表的单独分区。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
   
  
###  <a name="Lock"></a> 管理联机操作的锁优先级  
 `ONLINE = ON` 选项现在包含 `WAIT_AT_LOW_PRIORITY` 选项，该选项允许您指定重新生成过程对于所需锁应等待多长时间。 `WAIT_AT_LOW_PRIORITY` 选项还允许您配置与该重新生成语句相关的阻止过程的终止。 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL) ](/sql/t-sql/statements/alter-table-transact-sql) 和 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。 故障排除信息的锁状态的新类型现已推出[sys.dm_tran_locks &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)并[sys.dm_os_wait_stats &#40;-&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)。  
 
  
###  <a name="CCI"></a> 列存储索引  
 这些新功能可供列存储索引使用：  
  
-   **聚集列存储索引**  
  
     使用聚集列存储索引可提高主要执行大容量加载和只读查询的数据仓库工作负荷的数据压缩和查询性能。 由于聚集列存储索引是可更新的，因此工作负荷可执行许多插入、更新和删除操作。 有关详细信息，请参阅[列存储索引介绍](../relational-databases/indexes/columnstore-indexes-described.md)并[Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)。  
  
-   **显示计划**  
  
     SHOWPLAN 显示有关列存储索引的信息。 **EstimatedExecutionMode**并**ActualExecutionMode**属性具有两个可能值：**批处理**或者**行**。  **存储**属性具有两个可能值：**行存储**并**列存储**。  
  
-   **存档的数据压缩**  
  
     ALTER INDEX … REBUILD 提供新的 COLUMNSTORE_ARCHIVE 数据压缩选项，可进一步压缩列存储索引的指定分区。 这可用于存档，或者用于要求更小数据存储大小并且可以付出更多时间来进行存储和检索的其他情形。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
   
  
###  <a name="Buffer"></a> 缓冲池扩展  
 [缓冲池扩展](configure-windows/buffer-pool-extension.md)提供的非易失性随机存取内存 (NvRAM) 扩展为固态硬盘 (SSD) 的无缝集成[!INCLUDE[ssDE](../includes/ssde-md.md)]缓冲池，从而显著提高 I/O 吞吐量。  
   
  
###  <a name="Stats"></a> 增量统计信息  
 CREATE STATISTICS 和相关统计信息语句现在允许通过使用 INCREMENTAL 选项创建按分区的统计信息。 相关语句允许或报告增量统计信息。 受影响的语法包括 UPDATE STATISTICS、sp_createstats、CREATE INDEX、ALTER INDEX、ALTER DATABASE SET 选项、DATABASEPROPERTYEX、sys.databases 和 sys.stats。有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
  
###  <a name="RG"></a> 物理 IO 控制的资源调控器增强功能  
 通过资源调控器，您可以指定针对传入应用程序请求可在资源池内使用的 CPU、物理 IO 和内存的使用量的限制。 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，您可以使用新的 MIN_IOPS_PER_VOLUME 和 MAX_IOPS_PER_VOLUME 设置控制某一给定资源池向用户线程发出的物理 IO 数。 有关详细信息，请参阅[Resource Governor Resource Pool](../relational-databases/resource-governor/resource-governor-resource-pool.md)并[CREATE RESOURCE POOL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)。  
  
 ALTER RESOURCE GOVENOR 的 MAX_OUTSTANDING_IO_PER_VOLUME 设置可设置每个磁盘卷的最大待定 I/O 操作数 (IOPS)。 可以使用此设置根据某一磁盘卷的 IO 特性调整 IO 资源控制，并且可用于在 SQL Server 实例边界限制发出的 IO 数目。 有关详细信息，请参阅 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)。  
  
  
###  <a name="OnlineEvent"></a> Online Index Operation 事件类  
 针对联机索引操作事件类的进度报告现在具有两个新的数据列： **PartitionId**并**PartitionNumber**。 有关详细信息，请参阅[Progress Report: Online Index Operation 事件类](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md)。  
  
  
###  <a name="Compat"></a> 数据库兼容性级别  
 90 兼容性级别在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中无效。 有关详细信息，请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a> Transact-SQL 增强功能  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>CLUSTERED 和 NONCLUSTERED 的内联规范  
 对于基于磁盘的表，现在允许 `CLUSTERED` 和 `NONCLUSTERED` 索引的内联规范。 创建具有内联索引的表等效于发布一个 create table 命令，后随 `CREATE INDEX` 语句。 内联索引不支持包含列和筛选条件。  
  
### <a name="select--into"></a>SELECT … INTO  
 `SELECT … INTO` 语句得到了改进，现在可以并行操作。 数据库的兼容性级别必须至少为 110。  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>针对内存中 OLTP 的 [!INCLUDE[tsql](../includes/tsql-md.md)] 增强功能  
 璝惠[!INCLUDE[tsql](../includes/tsql-md.md)]更改为支持内存中 OLTP，请参阅[内存中 OLTP 的 TRANSACT-SQL 支持](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)。  
  
  
##  <a name="SystemTable"></a>系统视图增强功能  
  
### <a name="sysxmlindexes"></a>sys.xml_indexes  
 [sys.xml_indexes &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql)具有 3 个新列： `xml_index_type`， `xml_index_type_description`，并`path_id`。  
  
### <a name="sysdmexecqueryprofiles"></a>sys.dm_exec_query_profiles  
 [sys.dm_exec_query_profiles &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql)在执行查询时监视实时查询进度。  
  
### <a name="syscolumnstorerowgroups"></a>sys.column_store_row_groups  
 [sys.column_store_row_groups &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)每个段的基础来帮助管理员作出系统管理决定上提供聚集列存储索引信息。  
  
### <a name="sysdatabases"></a>sys.databases  
 [sys.databases &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)具有 3 个新列： `is_auto_create_stats_incremental_on`， `is_query_store_on`，并`resource_pool_id`。  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>针对内存中 OLTP 的系统视图增强功能  
 有关支持内存中 OLTP 的系统视图增强功能的信息，请参阅[系统视图、 存储过程、 Dmv 和内存中 OLTP 的等待类型](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)。  
   
  
##  <a name="Security"></a> 安全性改进  
  
### <a name="connect-any-database-permission"></a>CONNECT ANY DATABASE 权限  
 新的服务器级权限。 将 CONNECT ANY DATABASE 授予某个登录名，该登录名必须连接到当前存在的所有数据库和将来可能创建的任何新数据库。 不要在任何数据库中授予超过连接的任何权限。 结合**SELECT ALL USER SECURABLES**或`VIEW SERVER STATE`以允许审核进程查看所有数据或所有数据库状态的实例上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
### <a name="impersonate-any-login-permission"></a>IMPERSONATE ANY LOGIN 权限  
 新的服务器级权限。 授予后，当连接到数据库时，允许中间层进程模拟连接到它的客户端帐户。 被拒绝时，高特权的登录名可以阻止模拟其他登录名。 例如，可通过模拟其他登录名来阻止具有 CONTROL SERVER 权限的登录名。  
  
### <a name="select-all-user-securables-permission"></a>SELECT ALL USER SECURABLES 权限  
 新的服务器级权限。 授予后，作者等登录名可以查看用户可连接到的所有数据库中的数据。  
  
  
##  <a name="Deployment"></a> 部署增强功能  
### <a name="azure-vm"></a>Azure VM
[将 SQL Server 数据库部署到 Microsoft Azure 虚拟机](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)支持部署[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库添加到 Windows Azure 虚拟机。  

### <a name="refs"></a>ReFS
现在支持 ReFS 上的数据库的部署。   
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   
