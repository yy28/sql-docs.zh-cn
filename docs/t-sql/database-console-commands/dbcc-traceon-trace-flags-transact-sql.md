---
title: "跟踪标志 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- trace flags [SQL Server], about trace flags
- trace flags [SQL Server]
- global trace flags [SQL Server]
- flags [SQL Server]
- session trace flags [SQL Server]
- performance [SQL Server], trace
- debugging [SQL Server], trace flags
ms.assetid: b971b540-1ac2-435b-b191-24399eb88265
caps.latest.revision: "171"
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d5c466e35f8e37d7f2559e6766886b5ef80e390e
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="dbcc-traceon---trace-flags-transact-sql"></a>DBCC TRACEON-跟踪标志 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

跟踪标志用于临时设置特定服务器的特征或关闭特定行为。 例如，如果启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一个实例时设置了跟踪标志 3205，将禁用磁带机的硬件压缩。 跟踪标志经常用于诊断性能问题，或调试存储过程或复杂的计算机系统。
  
下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的跟踪标志，并进行了说明。
 
> [!NOTE]
> 特定中引入了一些跟踪标志[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 适用的版本的详细信息，请参阅 Microsoft 支持文章与特定的跟踪标志。

> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本可能不支持跟踪标志行为。 

  
|跟踪标志|Description|  
|---|---|
|**139**| 强制正确 DBCC 的作用域中的转换语义检查命令，如[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)， [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)和[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)，当分析改进了精度和转换逻辑中引入的兼容性级别 130 针对特定数据类型具有较低的兼容性级别的数据库上。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/help/4010261)。<br /><br />**注意：**此跟踪标志适用于[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]RTM CU3 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 和更高版本的生成。<br /><br />**警告：**跟踪标志 139 并不是在生产环境中，连续启用并应该用于执行数据库验证的唯一目的检查这中所述[Microsoft 支持文章](http://support.microsoft.com/help/4010261). 应该立即禁用后完成验证检查。<br /><br />**作用域**： 全局仅|
|**174**|增加[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]在 64 位系统上计划从 40,009 到 160,001 缓存桶计数。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3026083)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局仅|
|**176**|重新生成分区联机包含计算分区依据列的表时，请启用以解决错误修复。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3213683)。<br /><br />**作用域**： 全局或会话|
|**205**|报表复制到错误日志的结果正在重新编译依赖于统计信息的存储的过程时自动更新统计信息。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/195565)。<br /><br />**作用域**： 全局仅|
|**260**|打印有关扩展存储过程动态链接库 (DLL) 的版本控制信息。 有关详细信息**GetXpVersion()**，请参阅[创建扩展存储过程](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)。<br /><br />**作用域：**全局或会话|
|**272**|禁用标识预分配，以避免的情况下服务器意外重新启动或故障转移到辅助服务器的位置中的标识列的值方面的差距。 请注意，该标识缓存用于改进对具有标识列的表的插入性能。<br /><br />**注意：**开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]，若要实现此目的在数据库级别，请参阅中的 IDENTITY_CACHE 选项[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />**作用域**： 全局仅|
|**610**|控件按最小方式记录到索引表的插入。 此跟踪标志不是所需启动 SQL Server 2016，如最小日志记录打开默认情况下，索引的表。 SQL Server 2016 中大容量加载操作将导致一个新的页，并将其分配的所有行按顺序填充该新页面将按最小方式记录如果满足所有其他先决条件最小日志记录。 仍然能够完全记录插入到现有页面 （没有新的页分配） 来维护索引顺序中的行，因为是为移动的行页拆分加载期间。 也很重要 ALLOW_PAGE_LOCKS 已打开的索引 （这是默认情况下的 ON） 的最小日志记录操作按页锁获取期间分配和从而仅页或记录扩展盘区分配方式工作。有关详细信息，请参阅[数据加载性能指南](https://msdn.microsoft.com/library/dd425070.aspx)。<br /><br />**作用域**： 全局或会话|
|**634**|禁用背景列存储压缩任务。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定期运行压缩具有未压缩的数据，一次一个此类的行组的列存储索引行组的元组发动机后台任务。<br /><br />列存储压缩可提高查询性能，但也会占用系统资源。 你可以对列存储压缩计时手动，通过禁用后台压缩任务使用跟踪标志 634，并控制然后显式调用 ALTER INDEX...重新组织或 ALTER INDEX...重新生成在你选择的时间。<br /><br />**作用域：**全局仅|
|**652**|禁用页预提取扫描。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局或会话|
|**661**|禁用虚影记录删除过程。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局仅|
|**692**|大容量加载到堆或聚集的索引的数据时禁用快速的插入。 启动[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，快速插入启用默认情况下利用最小日志记录时数据库处于简单或大容量日志记录的恢复模型，以优化插入到新页的记录的插入性能。 使用快速插入，每个批量负载批获取跳过具有可用空间来优化插入性能的现有范围内分配查找的新扩展。<br /><br /> 使用快速的插入、 大容量加载使用小的批大小可能会导致增加未使用的空间对象因此建议使用每个批处理的大型 batchsize 完全填充范围内使用的。 如果增加 batchsize 不可行，则此跟踪标志有助于减少未使用的空间保留这会降低性能。 <br /><br />**注意：**此跟踪标志适用于[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]RTM 和更高版本的生成。<br /><br />**作用域**： 全局或会话|
|**715**|启用到没有非聚集索引的堆大容量加载操作的表锁。 启用此跟踪标志后，大容量加载操作将获取大容量更新 (BU) 锁大容量复制数据到表时。 大容量更新 (BU) 锁允许多个线程能够在同一个表，同时批量加载数据，同时防止其他进程不是从访问该表中的大容量加载数据。<br /><br />行为类似于当用户显式指定 TABLOCK 提示执行大容量加载时或当 sp_tableoption 表锁而使大容量加载为给定的表启用。 但是，当启用此跟踪标志时，此行为将成为无任何查询或数据库更改的默认值。<br /><br />**作用域：**全局或会话|
|**834**|使用 Microsoft Windows 大型页分配的缓冲池。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3210239)。<br /><br />**注意：**如果你使用的列存储索引功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，我们不建议开启跟踪标志 834。<br /><br />**作用域**： 全局仅|
|**845**|启用锁定页上的标准 Sku[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时的服务帐户，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存权限启用已锁定页。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/970070)和上的文档页[服务器内存服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md#lock-pages-in-memory-lpim)。<br /><br />**注意：**开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]此行为已启用默认情况下标准 Sku，且不能使用跟踪标志 845。<br /><br />**作用域**： 全局仅|
|**902**|在安装累积更新或 Service Pack 时，会绕过数据库升级脚本的执行。 如果在脚本升级模式期间遇到错误，它被建议更多指导，请与 Microsoft SQL 客户服务和支持 (CSS) 联系。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2163980)。<br /><br />**警告：**此跟踪标志旨在用于在脚本升级模式下，故障排除失败的更新的和不支持在生产环境中连续运行。 数据库升级脚本需要对于完整安装的累积更新和 Service Pack 成功执行。 不执行此操作可能会导致意外的问题与您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。<br /><br />**作用域**： 全局仅|
|**1117**|如果文件组中的文件达到了自动增长阈值，增加的文件组中的所有文件。<br /><br />**注意：**开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由 ALTER DATABASE 的 AUTOGROW_SINGLE_FILE 和 AUTOGROW_ALL_FILES 选项控制此行为，因此跟踪标志 1117年已失效。 有关详细信息，请参阅[ALTER DATABASE 文件和文件组选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).<br /><br />**作用域：**全局仅|
|**1118**|删除服务器上的大多数单页分配，以减少 SGAM 页上的争用。 创建一个新的对象后，默认情况下，从不同 （混合扩展盘区） 的扩展盘区分配的前八页。 此后，如果需要更多的页，将从相同的片区（统一区）分配进行分配。 SGAM 页用于跟踪这些混合区，因此发生大量混合页分配时，可能会很快成为瓶颈。 创建新对象时，此跟踪标志从相同的片区分配所有 8 页，以最大限度降低扫描 SGAM 页的需求。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/328551)。<br /><br />**注意：**开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由 ALTER DATABASE 设置 MIXED_PAGE_ALLOCATION 选项控制此行为，因此跟踪标志 1118年已失效。 有关详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)。<br /><br />**作用域：**全局仅|  
|**1204**|返回参与死锁的锁的资源和类型，以及受影响的当前命令。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/832524)。<br /><br />**作用域：**全局仅|  
|**1211**|基于内存不足或基于锁数禁用锁升级。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]不会将行锁或页锁升级到表锁。<br /><br />使用此跟踪标志可生成过多的锁数目。 这样会降低[!INCLUDE[ssDE](../../includes/ssde-md.md)]的性能，或因为内存不足而导致 1204 错误（无法分配锁资源）。<br /><br />如果同时设置了跟踪标志 1211 和 1224，则 1211 优先于 1224。 但是，由于在所有情况下（甚至在内存紧张的情况下）跟踪标志 1211 都禁止升级，因此建议使用 1224。 这有助于在使用多个锁时避免“锁不足”错误。<br /><br />**作用域**： 全局或会话|  
|**1222**|以不符合任何 XSD 架构的 XML 格式，返回参与死锁的锁的资源和类型，以及受影响的当前命令。<br /><br />**作用域**： 全局仅|  
|**1224**|基于锁数禁用锁升级。 但是，内存不足仍可激活锁升级。 如果锁对象使用的内存量超出下列条件之一，[!INCLUDE[ssDE](../../includes/ssde-md.md)]会将行锁或页锁升级为表（或分区）锁：<br /><br />-40%的内存的使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]。 这是适用时，才**锁**sp_configure 参数设置为 0。<br />的通过使用配置的锁定内存 40%**锁**的 sp_configure 的参数。 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。<br /><br />如果同时设置了跟踪标志 1211 和 1224，则 1211 优先于 1224。 但是，由于在所有情况下（甚至在内存紧张的情况下）跟踪标志 1211 都禁止升级，因此建议使用 1224。 这有助于在使用多个锁时避免“锁不足”错误。<br /><br />**注意：**锁升级到 HoBT 级别粒度的表级别还可通过使用的 LOCK_ESCALATION 选项控制[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)语句。<br /><br />**作用域：**全局或会话|
|**1236**|使数据库锁分区。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2926217)。<br /><br />**注意：**开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP3 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP1 由引擎和跟踪标志 1236年控制此行为不起作用。<br /><br />**作用域**： 全局仅|
|**1237**|允许的 ALTER PARTITION FUNCTION 语句授予当前用户定义的会话死锁优先级，而不是默认情况下可能的死锁牺牲品。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/help/4025261)。<br /><br />**注意：**开头[!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]和数据库[兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)140 这是默认行为和跟踪标志 1237年不起作用。<br /><br />**作用域**： 全局或会话或查询|
|**1260**|禁用计划程序监视器转储。<br /><br />**作用域**： 全局仅|   
|**1448**|甚至在异步辅助数据库不确认接受更改的情况下，也使复制日志读取器前移。 甚至在此跟踪标志启用的情况下，日志读取器也始终等待同步辅助数据库。 日志读取器将不会超过同步辅助数据库的最小确认。 此跟踪标志应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，而不仅是可用性组、可用性数据库或日志读取器实例。 应用会立即生效，无需重新启动。 此跟踪标志可提前激活或在同步辅助数据库失败时激活。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/937041)。<br /><br />**作用域**： 全局仅|   
|**1462**|禁用日志流压缩为异步可用性组。 默认情况下，异步可用性组以优化网络带宽，启用此功能。 有关详细信息，请参阅 [Tune compression for availability group](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)（调整可用性组的压缩）。<br /><br />**作用域**： 全局仅| 
|**1800**|使[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]优化对主要和辅助副本的日志文件，在使用不同的扇区大小的磁盘时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Always On 和日志传送的环境。 此跟踪标志仅需要在 SQL Server 实例上启用与事务日志文件驻留在扇区大小为 512 字节的磁盘上。 它是**不**在具有 4 k 扇区大小的磁盘上启用所需。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3009974)。<br /><br />**作用域：**全局仅|
|**2301**|启用高级的决策支持优化。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局和会话和查询|
|**2312**|使您能够设置为查询优化器基数估计模型[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本，取决于数据库的兼容性级别。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/2801413)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 FORCE_DEFAULT_CARDINALITY_ESTIMATION[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**作用域**： 全局或会话或查询| 
|**2335**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假设在查询优化过程固定的内存量为可用。 它不会限制内存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]授予执行查询。 为配置的内存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将仍可使用数据缓存、 查询执行情况和其他使用者。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2413549)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话或查询|
|**2340**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不是使用排序操作 （批处理排序），对于生成计划时优化嵌套的循环联接的。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2009160)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 DISABLE_OPTIMIZED_NESTED_LOOP[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话或查询|
|**2371**|固定的自动更新统计信息阈值更改为动态的自动更新统计信息的阈值。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2754171)。<br /><br />**注意：**开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]并在列表视图[数据库兼容性级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)130 上，此行为由引擎控制和跟踪标志 2371年不起作用。<br /><br />**作用域**： 全局仅|
|**2389**|启用自动生成升序键 （直方图修正） 的快速统计的信息。 如果设置跟踪标志 2389年，并且起始的统计信息列标记为升序排序，然后在查询编译时用于估计基数直方图进行调整。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2801413)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**注意：**此跟踪标志不适用于 CE 版本 120 或更高版本。 改为使用跟踪标志 4139。<br /><br />**作用域**： 全局或会话或查询|
|**2390**|启用自动生成升序或未知键 （直方图修正） 的快速统计的信息。 如果设置了跟踪标志 2390年，并且起始的统计信息列标记为升序或未知，则将在查询编译时调整用于估计基数的直方图。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2801413)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**注意：**此跟踪标志不适用于 CE 版本 120 或更高版本。 改为使用跟踪标志 4139。<br /><br />**作用域**： 全局或会话或查询|
|**2422**|使[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中止请求时超出了资源调控器 REQUEST_MAX_CPU_TIME_SEC 配置设置的最大时间。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/help/4038419)。<br /><br />**注意：**此跟踪标志适用于[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3 和更高版本的生成。<br /><br />**作用域**： 全局|
|**2430**|启用备用锁类清理。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2754301)。<br /><br />**作用域**： 全局仅| 
|**2453**|允许表变量的行的数量不足发生更改时触发重新编译。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2952444)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话或查询|
|**2528**|禁用 DBCC CHECKDB、DBCC CHECKFILEGROUP 和 DBCC CHECKTABLE 执行的对象并行检查。 默认情况下，并行度由查询处理器自动确定。 最大并行度的配置就像并行查询的最大并行度一样。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。<br /><br />**注意：**并行 DBCC 检查通常应该是启用 （默认值）。 查询处理器重新评估，并自动调整每个表或批处理的 DBCC checkdb 检查表的并行。<br /><br />系统管理员知道该服务器负载会增加才能 DBCC CHECKDB 完成，因此选择手动或降低禁用并行度，为了提高与其他用户工作负荷的并发性时的典型使用方案。 但是，禁用在 DBCC CHECKDB 的并行检查会导致它执行长时间才能完成。<br /><br />**注意：**如果使用 TABLOCK 选项执行 DBCC CHECKDB 和并行下为禁用，表可能被锁定的时间更长时间。<br /><br />**注意：**开头[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2，MAXDOP 选项可覆盖 max degree of parallelism 配置选项的 sp_configure 语句。<br /><br />**作用域**： 全局或会话|
|**2549**|运行 DBCC CHECKDB 命令假定每个数据库文件唯一的磁盘驱动器上。 DBCC CHECKDB 命令生成的所有数据库文件中读取每个唯一的磁盘驱动器的页数的内部列表。 此逻辑确定基于每个文件的物理文件名称的驱动器号的磁盘驱动器的唯一性。<br /><br />**注意：**不使用此跟踪标志，除非你知道，唯一的物理磁盘上基于每个文件。<br /><br />**注意：**尽管此跟踪标志提高的性能 DBCC CHECKDB PHYSICAL_ONLY 选项为其目标使用的命令，但有些用户可能看不到任何性能改善。 尽管此跟踪标志改进了磁盘 I/O 资源使用情况，磁盘资源的基础性能可能会限制 DBCC CHECKDB 命令的整体性能。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/2634571)。<br /><br />**作用域**： 全局仅| 
|**2562**|运行 DBCC CHECKDB 命令在单个"批处理"而不考虑数据库中的索引数。 默认情况下，DBCC CHECKDB 命令尝试 tempdb 资源通过限制的索引或通过使用"批处理"概念，它生成的"事实"的数量降至最低。 此跟踪标志强制所有处理到一个批次。<br /><br />使用此跟踪标志的影响之一是 tempdb 空间要求可能会增加。 Tempdb 可能增长到多达 5%或更多的 DBCC CHECKDB 命令正在处理的用户数据库。<br /><br />**注意：**尽管此跟踪标志提高的性能 DBCC CHECKDB PHYSICAL_ONLY 选项为其目标使用的命令，但有些用户可能看不到任何性能改善。 尽管此跟踪标志改进了磁盘 I/O 资源使用情况，磁盘资源的基础性能可能会限制 DBCC CHECKDB 命令的整体性能。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/2634571)。<br /><br />**作用域**： 全局仅|
|**2566**|除非指定 DATA_PURITY 选项，请运行 DBCC CHECKDB 命令而无需数据纯度检查。<br /><br />**注意：**列值完整性检查默认情况下启用，并且不需要 DATA_PURITY 选项。 为升级从早期版本的 SQL Server 数据库，列值检查不会启用默认情况下，直到 DBCC CHECKDB 与 DATA_PURITY 已可用的错误上运行数据库至少一次。 然后，DBCC CHECKDB 将默认检查列值完整性。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/945770)。<br /><br />**作用域**： 全局仅|
|**3023**|启用为 BACKUP 命令的默认值的校验和选项。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2656988)。<br /><br />**注意：**开头[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过设置控制此行为**备份校验和默认值**配置选项。 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。<br /><br />**作用域**： 全局和会话|
|**3042**|绕过默认的备份压缩预先分配算法，以便允许备份文件仅根据需要增长以达到其最终大小。 如果您需要仅分配压缩的备份所需的实际大小以便节约空间，则此跟踪标志将很有用。 使用此跟踪标志可能会导致轻微的性能损失（在备份操作期间损失可能会增加）。 有关预先分配算法的详细信息，请参阅[备份压缩 &#40;SQL server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br />**作用域**： 全局仅|
|**3051**|启用 SQL Server 备份到 URL 登录到特定的错误日志文件。 有关详细信息，请参阅[SQL Server 备份到 URL 最佳实践和故障排除](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)。<br /><br />**作用域**： 全局仅|  
|**3205**|默认情况下，如果磁带机支持硬件压缩，则 DUMP 或 BACKUP 语句会使用该功能。 利用此跟踪标志，可以禁用磁带机的硬件压缩。 此选项在您需要与不支持压缩的其他站点或磁带机交换磁带时很有用。<br /><br />**作用域**： 全局或会话|  
|**3226**|默认情况下，每个成功的备份操作都会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和系统事件日志中添加一个条目。 如果创建非常频繁的日志备份，这些成功消息会迅速累积，从而产生一个巨大的错误日志中查找其他消息会产生问题。<br /><br />使用这一跟踪标志，可以取消这些日志条目。 如果您频繁地运行日志备份，并且没有任何脚本依赖于这些条目，则这种做法非常有用。<br /><br />**作用域**： 全局仅|   
|**3427**|将数据插入到 temp 的多个连续事务表中时，启用修复问题[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]占用比在多个 CPU [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/help/3216543)<br /><br />**作用域**： 全局仅|  
|**3608**|阻止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动启动和恢复除之外的任何数据库**master**数据库。 如果活动，需要**tempdb**启动，然后**模型**恢复和**tempdb**创建。 在访问数据库时将启动并恢复其他数据库。 可能无法运行某些功能，如快照隔离和读提交快照。 用于[移动系统数据库](../../relational-databases/databases/move-system-databases.md)和[移动用户数据库](../../relational-databases/databases/move-user-databases.md)。<br /><br />**注意：**不在正常操作期间使用。<br /><br />**作用域**： 全局仅|   
|**3625**|限制的用户通过使用某些错误消息的参数不是 sysadmin 固定的服务器角色的成员返回的信息量\*\*\*\*\*\*。 这可以帮助阻止披露敏感信息。<br /><br />**作用域**： 全局仅|  
|**4136**|禁用参数截取除非 OPTION(RECOMPILE)、 WITH RECOMPILE 或 OPTIMIZE FOR\<值 > 使用。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/980653)。 若要实现此目的在数据库级别，请参阅中的 PARAMETER_SNIFFING 选项[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). 若要实现此目的在查询级别，添加 OPTIMIZE FOR UNKNOWN[查询提示](../../t-sql/queries/hints-transact-sql-query.md)。 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，第二个选项来实现此目的在查询级别是添加使用提示 PARAMETER_SNIFFING[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话|  
|**4137**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成使用最小选择性估计 AND 筛选器谓词时帐户进行关联，查询优化器基数估计模型的下一个计划[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更早版本。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2658214)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用旧 CE 时使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**注意：**此跟踪标志不适用于 CE 版本 120 或更高版本。 改为使用跟踪标志 9471。<br /><br />**作用域**： 全局或会话或查询| 
|**4138**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以生成不使用在中，使用包含 TOP，选项 (FAST N) 的查询的行目标调整或存在关键字的计划。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2667211)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 DISABLE_OPTIMIZER_ROWGOAL[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话或查询| 
|**4139**|启用自动生成而不考虑键列状态的快速统计信息 （直方图修正）。 如果设置跟踪标志 4139，而不考虑前导统计信息列状态 （升序、 降序或静态），用于估计基数直方图将调整在查询编译时。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2952101)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**注意：**此跟踪标志不适用于 CE 版本 70。 改为使用跟踪标志 2389年和 2390年。<br /><br />**作用域**： 全局或会话或查询|
|**4199**|启用查询优化器 (QO) 更改发布[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]累积更新和 Service Pack。<br /><br />版本进行到前一节 QO 更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]默认情况下最新的数据库启用[兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)在给定的产品版本中，而无需跟踪标志 4199 启用。<br /><br />下表汇总了在使用特定的数据库兼容性级别和跟踪标志 4199 时的行为。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/974006)。<br /><br /><table border="1" frame="void" width="550"><tr valign="middle" align="center"><td>**数据库兼容级别**</td><td>**TF 4199**</td><td>**从以前的数据库兼容性级别更改 QO**</td><td>**当前版本的 QO 更改 post RTM**</td></tr><tr valign="middle" align="center"><td rowspan="2">**100 到 120**</td><td>Off</td><td>禁用</td><td>禁用</td></tr><tr valign="middle" align="center"><td>On</td><td>已启用</td><td>已启用</td></tr><tr valign="middle" align="center"><td rowspan="2">**130**</td><td>Off</td><td>已启用</td><td>禁用</td></tr><tr valign="middle" align="center"><td>On</td><td>已启用</td><td>已启用</td></tr><tr valign="middle" align="center"><td rowspan="2">**140**</td><td>Off</td><td>已启用</td><td>禁用</td></tr><tr valign="middle" align="center"><td>On</td><td>已启用</td><td>已启用</td></tr></table><br /><br />若要实现此目的在数据库级别，请参阅中的 QUERY_OPTIMIZER_HOTFIXES 选项[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 ENABLE_QUERY_OPTIMIZER_HOTFIXES[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**作用域**： 全局或会话或查询|
|**4610**|将缓存条目存储的 8 倍哈希表的大小增加。 如果一起用于跟踪标志 4618 会增加到 8,192 TokenAndPermUserStore 缓存存储区中的项数。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/959823)。<br /><br />**作用域：**全局仅|
|**4616**|使应用程序角色可以看到服务器级元数据。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，应用程序角色无法访问自身数据库以外的元数据，因为应用程序角色与服务器级别主体不相关联。 这是对早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的行为的更改。 设置此全局标志将禁用新的限制，并允许应用程序角色访问服务器级元数据。<br /><br />**作用域**： 全局仅|
|**4618**|限制为 1,024 存储 TokenAndPermUserStore 缓存中的项数。 如果一起用于跟踪标志 4610 会增加到 8,192 TokenAndPermUserStore 缓存存储区中的项数。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/959823)。<br /><br />**作用域：**全局仅|
|**5004**|暂停 TDE 加密扫描，并会导致加密扫描工作线程退出而不执行任何操作。 数据库将继续处于加密状态 （正在进行加密）。 若要继续重新加密扫描，禁用跟踪标志 5004 并运行 ALTER DATABASE < database_name > 设置 ENCRYPTION ON。 <br /><br />**作用域：**全局仅|
|**6498**|启用多个大型查询编译时没有足够的内存可用来访问大型网关。 它基于 SQL Server 目标内存的 80 百分比，它允许进行一次每 25 千兆字节 (GB) 的内存的大型查询编译。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3024815)。<br /><br />**注意：**开头[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由引擎控制此行为和跟踪标志 6498 不起作用。<br /><br />**作用域**： 全局仅|
|**6527**|禁止在 CLR 集成中第一次发生内存不足异常时生成内存转储。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR 中生成上的内存不足异常的第一个匹配项的小的内存转储。 该跟踪标志的行为如下所示：<br /><br />-如果这用作启动跟踪标志，将永远不会生成内存转储。 但是，如果使用了其他跟踪标志，则可能会生成内存转储。<br />-如果正在运行的服务器上启用了此跟踪标志，内存转储将不会自动生成从该点上。 但是，如果已经由于 CLR 中的内存不足异常生成了内存转储，则此跟踪标志将没有任何效果。<br /><br />**作用域**： 全局仅|
|**6532**|启用与中的空间数据类型的查询操作的性能改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 根据配置、 的查询类型和对象，性能提升会有所不同。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3107399)。<br /><br />**注意：**开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由引擎控制此行为和跟踪标志 6532 不起作用。<br /><br />**作用域**： 全局和会话|
|**6533**|启用与中的空间数据类型的查询操作的性能改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 根据配置、 的查询类型和对象，性能提升会有所不同。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3107399)。<br /><br />**注意：**开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由引擎控制此行为和跟踪标志 6533 不起作用。<br /><br />**作用域**： 全局和会话| 
|**6534**|启用与中的空间数据类型的查询操作的性能改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 根据配置、 的查询类型和对象，性能提升会有所不同。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3107399)。<br /><br />**作用域**： 全局和会话|
|**7314**|强制使用被视为与 OLE DB 提供程序的双精度值的未知精度/缩放的数值。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3051993)。<br /><br />**作用域**： 全局和会话|  
|**7412**|启用分析基础结构的轻量的查询执行统计信息。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3170113)。<br /><br />**作用域**： 全局仅|
|**7471**|启用运行多个[更新统计信息](../../t-sql/statements/update-statistics-transact-sql.md)对单个表同时不同统计信息。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3156157)。<br /><br />**作用域**： 全局仅|
|**7745**|强制查询存储不将数据刷新到磁盘上的数据库关闭。<br /><br />**注意：**使用此跟踪可能会导致以前未刷新到磁盘以在关闭时会丢失的 Query Store 数据。 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]关闭，命令关闭与 NOWAIT 可以代替此跟踪标志用于强制立即关闭。<br /><br />**作用域**： 全局仅|
|**7752**|启用 Query store 的异步加载。<br /><br />**注意：**如果使用此跟踪标志[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]遇到大量 QDS_LOADDB 等待与 Query Store 同步负载 （默认行为）。<br /><br />**作用域**： 全局仅|
|**7806**|在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]上启用专用管理员连接 (DAC)。 默认情况下，在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上不保留 DAC 资源。 有关详细信息，请参阅 [用于数据库管理员的诊断连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。<br /><br />**作用域**： 全局仅|  
|**8011**|禁用资源监视器环形缓冲区。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局和会话|
|**8012**|为计划程序中禁用环形缓冲区。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局仅|
|**8015**|禁用自动检测和 NUMA 设置。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2813214)。<br /><br />**作用域**： 全局仅|
|**8018**|禁用异常环形缓冲区。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局仅|
|**8019**|禁用异常环形缓冲区的堆栈集合。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局仅|
|**8020**|禁用工作集监视。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**作用域**： 全局仅|
|**8032**|将缓存限制参数还原为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]RTM 设置，此设置通常允许更大的缓存。 当频繁重复使用的缓存条目不适合缓存时，以及当 [“针对即席工作负荷进行优化”服务器配置选项](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) 未能解决与计划缓存相关的问题时，请使用此设置。<br /><br />**警告：**跟踪标志 8032 可能导致性能不佳，如果大缓存使较少的内存可用于其他内存消耗者，如缓冲池。<br /><br />**作用域**： 全局仅|   
|**8048**|将 NUMA 划分为分区的 CPU 内存对象。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2809338)。<br /><br />**注意：**开头[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由引擎控制此行为和跟踪标志 8048 不起作用。<br /><br />**作用域**： 全局仅|  
|**8079**|允许[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 来询问硬件布局和报告每个 NUMA 节点 8 或多个 Cpu 的系统上自动配置 SOFT-NUMA。 自动 SOFT-NUMA 行为是超线程 （超线程/逻辑处理器），注意。 分区和创建其他节点缩放后台处理通过增加的数量的侦听器，缩放和网络和加密功能。<br /><br />**注意：**此跟踪标志适用于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2。 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]由引擎控制此行为和跟踪标志 8048 不起作用。<br /><br />**作用域**： 全局仅| 
|**8207**|允许事务复制的单独更新。 可以为删除和插入对复制到订阅服务器的更新。 这可能无法满足业务规则，如触发更新触发器。 使用跟踪标志 8207 作为更新，而不是删除或插入对复制对影响只有一行 （singleton 更新） 的唯一列的更新。 如果更新影响在其具有 unique 约束的列或更新影响多行，更新将仍复制为删除或插入对。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/302341)。<br /><br />**作用域**： 全局仅|
|**8721**|错误日志时自动更新统计信息执行报表。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/195565)。<br /><br />**作用域**： 全局仅|
|**8744**|禁用对嵌套循环运算符预提取功能。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/920093)。<br /><br />**注意：**此跟踪标志的使用不当可能会导致其他物理读取次数时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行包含 Nested Loops 运算符的计划。<br /><br />**作用域**： 全局和会话|
|**9024**|将全局日志池内存对象转换为 NUMA 节点分区的内存对象。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/2809338)。<br /><br />**注意：**开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP3 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP1 由引擎和跟踪标志 9024 控制此行为不起作用。<br /><br />**作用域**： 全局仅|
|**9347**|禁用批处理模式排序运算符。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]引入了许多分析查询的性能提高了一个新的批处理模式排序运算符。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3172787)。<br /><br />**作用域**： 全局或会话或查询|
|**9349**|禁用批处理模式下的 top N sort 运算符。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]引入了许多分析查询的性能提高了一个新的批处理模式顶部排序运算符。<br /><br />**作用域**： 全局或会话或查询|
|**9389**|启用批处理模式运算符的动态内存授予。 如果查询不会获取它需要的所有内存，它会溢出到 tempdb，会产生额外的 I/O 并可能会影响查询性能的数据。 如果启用动态内存授予跟踪标志，批处理模式运算符可能要求更多的内存，并避免提供额外的内存时，将对 tempdb 溢出。<br /><br />**作用域**： 全局或会话| 
|**9453**|禁用批处理模式执行。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/help/4016902)。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域：**全局和会话和查询|
|**9471**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成使用单表下的筛选器，查询优化器基数估计模型的最小选择性计划[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**注意：**此跟踪标志不适用于 CE 版本 70。 改为使用跟踪标志 4137。<br /><br />**作用域**： 全局或会话或查询| 
|**9476**|导致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成简单的包含假设使用而不默认基包含假设，查询优化器基数估计模型的下一个计划[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/3189675)。<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**注意：**请确保先进行全面测试此选项，然后将它应用到生产环境。<br /><br />**作用域**： 全局或会话或查询| 
|**9481**|使您能够设置为查询优化器基数估计模型[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更早版本，而不考虑数据库的兼容性级别。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/2801413)。 若要实现此目的在数据库级别，请参阅中的 LEGACY_CARDINALITY_ESTIMATION 选项[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 中，为实现此目的在查询级别中，添加使用提示 FORCE_LEGACY_CARDINALITY_ESTIMATION[查询提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用此跟踪标志。<br /><br />**作用域**： 全局或会话或查询|  
|**9485**|对 DBCC SHOW_STATISTICS 禁用 SELECT 权限。<br /><br />**作用域**： 全局仅|
|**9488**|将表值函数的固定的估计设置为默认值 1 (对应于在查询优化器基数估计模型的默认[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]及更早版本)、 使用的查询优化器基数估计模型时[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。<br /><br />**作用域**： 全局或会话或查询|
|**9495**|在插入过程中禁用并行...选择操作和它适用于用户和临时表。 有关详细信息，请参阅[Microsoft 支持文章](http://support.microsoft.com/kb/3180087)<br /><br />**作用域**： 全局或会话| 
|**9567**|启用压缩数据流的 Alwayson 可用性组的自动种子设定过程。 压缩可以显著减少自动种子设定过程的传输时间，将增加处理器上的负载。 有关详细信息，请参阅[自动初始化 Alwayson 可用性组](../../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)和[调整可用性组的压缩](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)。<br /><br />**作用域**： 全局或会话|
|**9591**|禁用 Alwayson 可用性组中日志块压缩。 日志块压缩是对包含同步和异步副本中使用的默认行为[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，压缩仅用于异步副本。 <br /><br />**作用域**： 全局或会话|
|**9592**|启用日志流压缩为同步的可用性组。 默认情况下，同步的可用性组禁用此功能，因为压缩为增加延迟。 有关详细信息，请参阅 [Tune compression for availability group](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)（调整可用性组的压缩）。<br /><br />**作用域**： 全局或会话| 
|**9939**|启用并行计划和内存优化表和表变量中引用内存优化表或表变量的 DML 操作的并行扫描，只要它们不在 DML 操作的目标[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/4013877)。<br /><br />**注意：**如果还可以显式启用跟踪标志 4199，则不需要跟踪标志 9939。<br /><br />**作用域**： 全局或会话或查询|   
|**10204**|禁用合并/重新压缩在列存储索引重组过程。 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，当列存储索引进行重组，自动将任何小压缩行组合并为更大压缩行组，以及为重新压缩拥有大量的任何行组已删除行的新功能。<br /><br />**注意：**跟踪标志 10204 不适用于在内存优化表上创建列存储索引。<br /><br />**作用域**： 全局或会话|   
|**10316**|在可以创建其他索引[内部内存优化临时临时表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)，默认旁边。 如果你有包含不受默认索引的列的特定查询模式可能希望添加其他的。<br /><br />**注意：**系统版本控制临时表的内存优化表旨在提供高事务吞吐量。 请注意，创建附加索引可能会引入的更新或删除当前表中的行的 DML 操作的开销。 与其他索引应旨在右之间找到平衡点临时查询的性能和其他 DML 开销。<br /><br />**作用域**： 全局或会话|
|**11023**|禁用其中一个的采样率未显式指定作为的一部分的所有后续的统计信息更新的最后一个持久的采样率，用于[更新统计信息](../../t-sql/statements/update-statistics-transact-sql.md)语句。 有关详细信息，请参阅此[Microsoft 支持文章](http://support.microsoft.com/kb/4039284)。<br /><br />**作用域**： 全局| 
  
## <a name="remarks"></a>Remarks  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，有三种类型的跟踪标志： 查询、 会话和全局。 查询跟踪标志处于活动状态的特定查询的上下文。 会话跟踪标志处于活动状态的连接，并且仅对该连接可见。 全局跟踪标志在服务器级别上进行设置，对服务器上的每一个连接都可见。 某些标志只能作为全局标志启用，而某些标志在全局或会话作用域都可以启用。  
  
 下列规则适用：  
-   全局跟踪标志必须全局启用。 否则，跟踪标志无效。 我们建议你通过使用启用全局跟踪标志启动时， **-T**命令行选项。 这可确保在服务器重启后，跟踪标志保持活动状态。  
-   如果跟踪标志任一全局、 会话或查询作用域，它可以启用与相应的作用域。 在会话级别启用的跟踪标志永远不会影响另一个会话，并且当打开会话的 SPID 注销时，该跟踪标志将失效。  
  
使用以下方法之一可将跟踪标志设置为开或关：
-   使用 DBCC TRACEON 和 DBCC TRACEOFF 命令。  
     例如，若要全局启用 2528年跟踪标志，请使用 DBCC TRACEON 使用-1 的参数： `DBCC TRACEON (2528, -1)`。 启用与 DBCC TRACEON 全局跟踪标志的效果上重新启动服务器，丢失。 若要关闭全局跟踪标志，请在使用 DBCC TRACEOFF 时使用 -1 参数。  
-   使用**-T**启动选项以指定在启动期间上设置跟踪标志。  
     **-T**启动选项全局启用跟踪标志。 使用启动选项无法启动会话级别的跟踪标志。 这可确保在服务器重启后，跟踪标志保持活动状态。 有关启动选项的详细信息，请参阅 [数据库引擎服务启动选项](../../database-engine/configure-windows/database-engine-service-startup-options.md)。
-   在查询级别，通过使用 QUERYTRACEON[查询提示](http://support.microsoft.com/kb/2801413)。
  
使用`DBCC TRACESTATUS`命令，以确定哪些跟踪标志是当前处于活动状态。
  
## <a name="examples"></a>示例  
 下面的示例设置跟踪标志 3205 上的所有会话在服务器级别使用 DBCC TRACEON。  
  
```sql  
DBCC TRACEON (3205,-1);  
```

你可以启用所有计划影响修补程序由跟踪标志 4199 和特定查询的 4137 控制。
  
```sql
SELECT x FROM correlated WHERE f1 = 0 AND f2 = 1 OPTION (QUERYTRACEON 4199, QUERYTRACEON 4137)
``` 
 
## <a name="see-also"></a>另请参阅  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[DBCC INPUTBUFFER (Transact-SQL)](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
[DBCC OUTPUTBUFFER &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)  
[DBCC TRACEOFF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)  
[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
[设置 NOCOUNT &#40;Transact SQL &#41;](../../t-sql/statements/set-nocount-transact-sql.md)  
[ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
[查询提示 (TRANSACT-SQL)](../../t-sql/queries/hints-transact-sql-query.md)

