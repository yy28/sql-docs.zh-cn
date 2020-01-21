---
title: 性能中心
ms.custom: seo-dt-2019
ms.date: 12/11/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- Performance (SQL Server)
- Performance (SQL Database)
helpviewer_keywords:
- SQL Server, performance
- performance (SQL Server)
- database performance (SQL Server)
- SQL Database (Performance)
- performance (SQL Database)
- database performance (SQL Database)
ms.assetid: 301204b2-140d-4495-98ed-021a9b5025f5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c58546e4b87e0d52175124263e53b54a912689d1
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2019
ms.locfileid: "74164941"
---
# <a name="performance-center-for-sql-server-database-engine-and-azure-sql-database"></a>SQL Server 数据库引擎和 Azure SQL 数据库的性能中心
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本页提供的链接可帮助你找到有关 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]中的性能的必要信息。  
  
 **图例**  
  
 ![security-center-legend](../../relational-databases/performance/media/security-center-legend.PNG "security-center-legend")  
  
## <a name="configuration-options-for-performance"></a>性能的配置选项  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过许多 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 级别的配置选项，提供了可影响数据库引擎性能的功能。 通过 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]，Microsoft 可为你执行这些优化中的大多数（不是全部）。  
  
|||  
|-|-|  
|**磁盘配置选项**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [磁盘条带化和 RAID](https://technet.microsoft.com/library/ms190764\(v=sql.105\).aspx)|  
|**数据和日志文件配置选项**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref3::|") [将数据和日志文件放到不同的驱动器上](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref4::|") [查看或更改数据文件和日志文件的默认位置 (SQL Server Management Studio)](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|**TempDB 配置选项**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [TempDB 的性能改进](../databases/tempdb-database.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [数据库引擎配置 - TempDB](https://msdn.microsoft.com/library/7aabd304-f3c9-4c2d-bf9d-5479ee2498da)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref7::|") [使用 Azure VM 中的 SSD 存储 SQL Server TempDB 和缓冲池扩展](https://blogs.technet.com/b/dataplatforminsider/archive/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions.aspx)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref8::|") [Azure 虚拟机中 SQL Server 的临时磁盘的磁盘和性能最佳做法](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)|  
|**服务器配置选项**|**处理器配置选项**<br /><br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [“关联掩码”服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref10::|") [“关联输入/输出掩码”服务器配置选项](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [“affinity64 掩码”服务器配置选项](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref12::|") [“affinity64 输入/输出掩码”服务器配置选项](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref13::|") [配置“最大工作线程数”服务器配置选项](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br /><br />**内存配置选项**<br /><br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)<br /><br />**索引配置选项**<br /><br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref15::|") [配置“填充因子”服务器配置选项](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md)<br /><br />**查询配置选项**<br /><br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref16::|") [配置“每次查询占用的最小内存”服务器配置选项](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref17::|") [配置“查询调控器开销限制”服务器配置选项](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref18::|") [配置“最大并行度”服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref19::|") [配置“并行的开销阈值”服务器配置选项](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref20::|") [“针对即席工作负荷进行优化”服务器配置选项](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)<br /><br />**备份配置选项**<br /><br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref21::|") [查看或配置“备份压缩默认值”服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)|  
|**数据库配置优化选项**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [数据压缩](../../relational-databases/data-compression/data-compression.md)<br />![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref23::|") [查看或更改数据库的兼容级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)<br />![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref24::|") [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|**表配置优化**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [已分区表和索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md)|  
|**Azure 虚拟机中的数据库引擎性能**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [快速检查列表](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "|::ref27::|") [虚拟机大小和存储帐户注意事项](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [磁盘和性能注意事项](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [I/O 性能注意事项](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [功能特定的性能注意事项](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-performance-best-practices/)| 
|**性能最佳做法和 Linux 上的 SQL Server 的配置准则**|![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [SQL Server 配置](../../linux/sql-server-linux-performance-best-practices.md#sql-server-configuration)<br />![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [Linux OS 配置](../../linux/sql-server-linux-performance-best-practices.md#linux-os-configuration)|

> [!IMPORTANT]
> 其他注意事项请参阅：    
> -  [适用于具有高性能工作负载的 SQL Server 2012 和 SQL Server 2014 的推荐更新和配置选项](https://support.microsoft.com/help/2964518)
> -  [适用于具有高性能工作负载的 SQL Server 2017 和 SQL Server 2016 的推荐更新和配置选项](https://support.microsoft.com/help/4465518)

## <a name="query-performance-options"></a>查询性能选项  
  
|||  
|-|-|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [索引](../../relational-databases/indexes/indexes.md) |[重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)<br />[为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)<br />[配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)<br />[用于索引的 SORT_IN_TEMPDB 选项](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)<br />[改进全文索引的性能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)<br />[配置“每次查询占用的最小内存”服务器配置选项](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)<br />[配置 index create memory 服务器配置选项](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [已分区表和索引](../../relational-databases/partitions/partitioned-tables-and-indexes.md) |[分区的优点](../partitions/partitioned-tables-and-indexes.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [联结](../../relational-databases/performance/joins.md) |[联接基础知识](../../relational-databases/performance/joins.md#fundamentals)<br />[嵌套循环联接](../../relational-databases/performance/joins.md#nested_loops)<br />[合并联接](../../relational-databases/performance/joins.md#merge)<br />[联接](../../relational-databases/performance/joins.md#hash)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [子查询](../../relational-databases/performance/subqueries.md) |[子查询基础知识](../../relational-databases/performance/subqueries.md#fundamentals)<br />[相关子查询](../../relational-databases/performance/subqueries.md#correlated)<br />[子查询类型](../../relational-databases/performance/subqueries.md#types)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [存储过程](../stored-procedures/stored-procedures-database-engine.md) |[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md#best-practices)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") **[用户定义的函数](../user-defined-functions/user-defined-functions.md)**|[CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md#best-practices)<br />[创建用户定义函数（数据库引擎）](../user-defined-functions/create-user-defined-functions-database-engine.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 并行优化 |[配置 max worker threads 服务器配置选项](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)<br />[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") 查询优化器优化 |[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)<br />[USE HINT 查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") [统计](../../relational-databases/statistics/statistics.md) |[何时更新统计信息](../statistics/statistics.md)<br />[更新统计信息](../../relational-databases/statistics/update-statistics.md)|  
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref42::|") [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) |[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)<br />[本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)<br />[通过本机编译的存储过程创建和访问 TempDB 中的表](../../relational-databases/in-memory-oltp/create-and-access-tables-in-tempdb-from-stored-procedures.md)<br />[对内存优化哈希索引的常见性能问题进行故障排除](https://msdn.microsoft.com/library/1954a997-7585-4713-81fd-76d429b8d095)<br />[演示：内存中 OLTP 的性能改进](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)|
|![security-center-both](../../relational-databases/performance/media/security-center-both.png "|::ref43::|") **[智能查询处理](../../relational-databases/performance/intelligent-query-processing.md)**|[智能查询处理](../../relational-databases/performance/intelligent-query-processing.md)|
  
## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [单一数据库的 Azure SQL 数据库性能指南](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)   
 [使用弹性池优化 Azure SQL 数据库性能](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-guidance/)   
 [Azure 查询性能见解](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)  
 [索引设计指南](../../relational-databases/sql-server-index-design-guide.md)  
 [内存管理体系结构指南](../../relational-databases/memory-management-architecture-guide.md)  
 [页和区体系结构指南](../../relational-databases/pages-and-extents-architecture-guide.md)  
 [迁移后验证和优化指南](../../relational-databases/post-migration-validation-and-optimization-guide.md)  
 [查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)  
 [SQL Server 事务锁定和行版本控制指南](https://msdn.microsoft.com/library/jj856598)  
 [SQL Server 事务日志体系结构和管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)  
 [线程和任务体系结构指南](../../relational-databases/thread-and-task-architecture-guide.md) 
  
