---
title: ALTER DATABASE 兼容级别 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: 89
author: CarlRabeler
ms.author: carlrab
manager: craigg'
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 57bafde547e9c2705d55308187fd53e241594d5f
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088369"
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE (Transact-SQL) 兼容级别
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

将某些数据库行为设置为与指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本兼容。 有关其他 ALTER DATABASE 选项，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  

有关语法约定的详细信息，请参阅 [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。
  
## <a name="syntax"></a>语法  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要修改的数据库的名称。  
  
 COMPATIBILITY_LEVEL { 150 | 140 | 130 | 120 | 110 | 100 | 90 | 80 }  
 要使数据库与之兼容的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 可以配置以下兼容级别值（并非所有版本都支持所有以上列出的兼容级别）：  
  
|Product|数据库引擎版本|兼容级别指定|支持的兼容级别值|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140、130、120、110、100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 逻辑服务器|12|130|150、140、130、120、110、100|  
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 托管实例|12|130|150、140、130、120、110、100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130、120、110、100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120、110、100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110、100、90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100、90、80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100、90、80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90、80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> 从 2018 年 1 月起，在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，新创建的数据库的默认兼容性级别为 140。 我们不会更新现有数据库的数据库兼容性级别。 这是由客户自行决定的。 不过，强烈建议客户计划转到最新的兼容性级别，以便利用最新的改进。
> 
> 如果想要对整个数据库利用数据库兼容性级别 140，但有理由优先选择映射到数据库兼容性级别 110 的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的基数估计模型，请参阅 [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)，尤其是其关键字 `LEGACY_CARDINALITY_ESTIMATION = ON`。
>  
> 有关如何评估 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]上两个兼容级别之间最重要查询的性能差异的详细信息，请参阅 [Improved Query Performance with Compatibility Level 130 in Azure SQL Database（在 Azure SQL 数据库中使用兼容级别 130 提高了查询性能）](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。 注意，本文是指兼容性级别 130 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但同样的方法也适用于转到 140 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

执行以下查询可确定连接到的[!INCLUDE[ssDE](../../includes/ssde-md.md)]的版本。  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]上并不支持所有功能（因兼容级别而异）。  

 若要确定当前兼容级别，请查询 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 的 **compatibility_level** 列。  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Remarks  
对于所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，默认兼容级别都设置为[!INCLUDE[ssDE](../../includes/ssde-md.md)]的版本。 除非数据库具有更低的兼容级别，否则数据库会设置为此级别。 在将数据库从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何早期版本进行升级时，如果数据库至少是该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所允许的最低级别，则它会保留现有兼容性级别。 升级兼容性级别低于允许级别的数据库会将数据库自动设置为允许的最低兼容性级别。 这既适用于系统数据库也适用于用户数据库。   

附加或还原数据库时以及就地升级后，[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 应出现以下行为： 
- 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。    
- 如果升级前用户数据库的兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 支持的最低兼容级别。    
- 升级后，tempdb、model、msdb 和 Resource 数据库的兼容性级别将设置为当前兼容性级别。  
- master 系统数据库保留它在升级之前的兼容性级别。

使用 `ALTER DATABASE` 更改数据库的兼容性级别。 当发出 `USE <database>` 命令或使用该数据库作为默认数据库上下文来处理新登录时，数据库的新兼容性级别设置会生效。     
若要查看数据库的当前兼容级别，请查询 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目录视图中的 **compatibility_level** 列。  

> [!NOTE]  
> 在早期版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建并已升级到 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM 或 Service Pack 1 的[分发数据库](../../relational-databases/replication/distribution-database.md)采用兼容性级别 90，其他数据库不支持该级别。 这并不影响复制功能。 升级到更高版本的服务包和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本将导致分发数据库的兼容性级别增加到可与主数据库匹配。

## <a name="compatibility-levels-and-sql-server-upgrades"></a>兼容性级别和 SQL Server 升级  
数据库兼容性级别是一个重要的工具，可通过允许升级 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，同时通过维持相同的升级前数据库兼容性级别保持连接应用程序功能状态，从而帮助实现数据库现代化。 只要应用程序不需要利用仅在更高数据库兼容性级别中可用的增强功能，它就是升级 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和维护之前的数据库兼容性级别的有效方法。 有关利用兼容性级别获取后向兼容性的详细信息，请参阅后文的[利用兼容性级别获得后向兼容性](#using-compatibility-level-for-backward-compatibility)。    

对于新的开发工作，或当现有应用程序需要使用新功能以及查询优化器空间中完成的性能改进时，计划将数据库兼容性级别升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的最新级别，并验证应用程序可与该兼容性级别一起使用。 有关升级数据库兼容性级别的更多详细信息，请参阅后文的[升级数据库兼容性级别的最佳做法](#best-practices-for-upgrading-database-compatibility-level)。     

> [!TIP] 
> 如果在给定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本上测试和验证应用程序，则应用程序在该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本本机数据库兼容性级别上隐式测试和验证。
> 
> 因此，在使用对应于已测试 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的数据库兼容性级别时，数据库兼容性级别可为现有应用程序提供简易的认证途径。
>
> 有关兼容性级别之间的差异的详细信息，请参阅后文相应的部分。 

若要将 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 升级到最新版，同时将数据库兼容性级别维持在升级前的级别并维持其可支持性状态，建议在数据库中使用 [Microsoft 数据迁移助手](http://www.microsoft.com/download/details.aspx?id=53595)工具 (DMA) 对应用程序代码执行静态函数外围应用验证。 DMA 工具输出中没有关于缺失或不兼容功能的错误，可保护应用程序免受新目标版本上的任何功能回归影响。 有关 DMA 工具的详细信息，请参阅[此处](http://blogs.msdn.microsoft.com/datamigration/dma)。

> [!NOTE] 
> DMA 支持数据库兼容性级别 100 及更高级别。 排除 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 作为源版本。 

> [!IMPORTANT] 
> Microsoft 建议执行一些最小测试来验证更新是否成功，同时维持之前的数据库兼容性级别。 应该确定适用于自己的应用程序和场景的最小测试。 

> [!NOTE] 
> Microsoft 在下列情况下提供查询计划形状保护：
> - 新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（目标）在相当于之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本（源）运行的硬件上运行。 
> - 目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 均使用同一[支持的数据库兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#remarks)。 
> 
> 上述情况下发生的任何查询计划形状回归（与源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相比）将得到解决。 如果出现这种情况，请与 Microsoft 客户支持服务部门联系。

## <a name="using-compatibility-level-for-backward-compatibility"></a>利用兼容性级别获得向后兼容  
数据库兼容性级别设置只影响指定数据库的行为，而不影响整个服务器的行为。 数据库兼容性级别只实现与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本保持部分后向兼容。   

> [!TIP]
> 因为数据库兼容级别是数据库级设置，所以在较新的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 上运行但使用较旧的数据库兼容级别的应用程序仍可利用服务器级增强功能，无需对应用程序进行任何更改。
>
> 其中包括丰富的监控和故障排除改进，并提供新的[系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)和[扩展事件](../../relational-databases/extended-events/extended-events.md)。 此外，还提升了可伸缩性，例如，提供[自动 Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)。

从兼容性模式 130 开始，任何影响功能的新查询计划都有意仅添加到新兼容性级别中。 这样做是为了在由于查询计划更改导致性能降低而引发的升级过程中尽量减少风险。   
从应用程序的角度来看，目标仍应在某个时间点升级到最新兼容性级别以便继承某些新功能，以及在查询优化器空间中完成的性能改进，不过是采用可控方式实现此目标。 通过将较低兼容性级别用作更安全的迁移辅助工具，可解决相关兼容性级别设置控制的行为之间存在的版本差异问题。 有关更多详细信息，包括升级数据库兼容性级别的建议工作流，请参阅后文的[升级数据库兼容性级别的最佳做法](#best-practices-for-upgrading-database-compatibility-level)。  
  
> [!IMPORTANT]
> 给定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中引入的废止功能不受兼容级别保护。 这指的是从 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中删除的功能。
> 
> 例如，`FASTFIRSTROW` 提示在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中废止，并替换为 `OPTION (FAST n )` 提示。 将数据库兼容级别设置为 110 不会恢复废止的提示。
> 有关废止功能的详细信息，请参阅 [SQL Server 2016 中废止的数据库引擎功能](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)、[SQL Server 2014 中废止的数据库引擎功能](http://msdn.microsoft.com/library/ms144262(v=sql.120))、[SQL Server 2012 中废止的数据库引擎功能](http://msdn.microsoft.com/library/ms144262(v=sql.110))和 [SQL Server 2008 中废止的数据库引擎功能](http://msdn.microsoft.com/library/ms144262(v=sql.100))。

> [!IMPORTANT]
> 给定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版 本中引入的重大更改**可能**不受兼容级别保护。 这指的是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本之间的行为变更。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 行为通常受兼容级别保护。 但是，已更改或删除的系统对象**不**受兼容级别保护。
>
> 受兼容级别**保护**的一个重大更改示例是从 datetime 到 datetime2 数据类型的隐式转换。 在数据库兼容级别 130 以下，通过考虑导致不同转换值的毫秒小数部分，这些转换显得更加准确。 若要还原以前的转换行为，请将数据库兼容级别设置为 120 或更低。
>
> 兼容级别**不保护**的重大更改示例有：
> -  系统对象中更改了列名。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，sys.dm_os_sys_info 中的列 single_pages_kb 已重命名为 pages_kb。 无论兼容级别如何，查询 `SELECT single_pages_kb FROM sys.dm_os_sys_info` 都会生成错误 207（列名无效）。
> -  删除了系统对象。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，`sp_dboption` 已删除。 无论兼容级别如何，语句 `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` 都会生成错误 2812（找不到存储过程“sp_dboption”）。
>
> 有关重大更改的详细信息，请参阅 [SQL Server 2017 中数据库引擎功能的重大更改](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md)、[SQL Server 2016 中数据库引擎功能的重大更改](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)[SQL Server 2014 中数据库引擎功能的重大更改](http://msdn.microsoft.com/library/ms143179(v=sql.120))、[SQL Server 2012 中数据库引擎功能的重大更改](http://msdn.microsoft.com/library/ms143179(v=sql.110))和 [SQL Server 2008 中数据库引擎功能的重大更改](http://msdn.microsoft.com/library/ms143179(v=sql.100))。
  
## <a name="best-practices-for-upgrading-database-compatibility-level"></a>升级数据库兼容性级别的最佳做法 
有关用于升级兼容级别的建议工作流，请参阅[更改数据库兼容性模式和使用查询存储](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。  

## <a name="compatibility-levels-and-stored-procedures"></a>兼容性级别和存储过程  
 执行某一存储过程时，该存储过程将使用定义它的数据库的当前兼容性级别。 在更改某一数据库的兼容性设置时，该数据库的所有存储过程都将随之自动重新编写。  

## <a name="differences-between-compatibility-level-140-and-level-150"></a>兼容性级别 140 和 150 的区别  
此部分介绍了随兼容性级别 150 一起引入的新行为。

对于 Azure SQL 数据库，数据库兼容性级别 150 目前是个人预览版。  除了数据库兼容性级别 140 中引入的改进之外，此数据库兼容性级别还将与下一代查询处理改进相关联。  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>兼容级别 130 与兼容级别 140 之间的差异  
本节介绍随兼容级别 140 引入的新行为。

|兼容级别设置为 130 或更低|兼容级别设置为 140|  
|--------------------------------------------------|-----------------------------------------|  
|引用多语句表值函数的语句的基数估计使用固定行猜测。|引用多语句表值函数的符合条件语句的基数估计会使用函数输出的实际基数。  这通过多语句表值函数的**交错执行**来实现。|
|请求会导致溢出到磁盘的不充足内存授予大小的批处理模式查询可能会继续对连续执行产生问题。|请求会导致溢出到磁盘的不充足内存授予大小的批处理模式查询可能会提高连续执行的性能。 这通过在对批处理模式运算符发生溢出时，会更新缓存计划内存授予大小的**批处理模式内存授予反馈**来实现。 |
|请求会导致并发问题的过多内存授予大小的批处理模式查询可能会继续对连续执行产生问题。|请求会导致并发问题的过多内存授予大小的批处理模式查询可能会改进连续执行的并发性。 这通过在最初请求了过多量时，会更新缓存计划内存授予大小的**批处理模式内存授予反馈**来实现。|
|包含联接运算符的批处理模式查询有资格使用三种物理联接算法，包括嵌套循环、哈希联接和合并联接。 如果基数估计对于联接输入不正确，则可能会选择不适当的联接算法。 如果发生这种情况，则性能会降低，并且不适当的联接算法会保持使用，直到缓存计划进行重新编译。|有一个名为**自适应联接**的其他联接运算符。 如果基数估计对于外部生成联接输入不正确，则可能会选择不适当的联接算法。 如果发生这种情况，并且语句有资格进行自适应联接，则会将嵌套循环用于较小联接输入，将哈希联接动态用于较大联接输入，而无需重新编译。 |
|引用列存储索引的普通计划没有资格进行批处理模式执行。 |引用列存储索引的普通计划会被放弃，以便支持有条件进行批处理模式执行的计划。|
|`sp_execute_external_script` UDX 运算符只能在行模式下运行。|`sp_execute_external_script` UDX 运算符有资格进行批处理模式执行。|  
|多语句表值函数 (TVF) 没有交错执行 |用于改进计划质量的多语句 TVF 交错执行。|

SQL Server 2017 之前的早期 SQL Server 版本中处于跟踪标志 4199 下的修补程序现在默认情况下会启用。 具有兼容性模式 140。 跟踪标志 4199 仍会适用于在 SQL Server 2017 之后发布的新查询优化器修补程序。 有关跟踪标志 4199 的信息，请参阅[跟踪标志 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)。  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>兼容级别 120 和兼容级别 130 之间的差异  
本节介绍随兼容级别 130 引入的新行为。   

|兼容级别设置为 120 或更低|兼容级别设置为 130|  
|--------------------------------------------------|-----------------------------------------|  
|INSERT-SELECT 语句中的 INSERT 是单线程。|INSERT-SELECT 语句中的 INSERT 是多线程，或者可以具有并行计划。|  
|内存优化表的查询执行单线程。|内存优化表的查询现在可以具有并行计划。|  
|引入了 SQL 2014 基数估算器 **CardinalityEstimationModelVersion="120"**|基数估计模型 130 带来了进一步基数估计 (CE) 改进（在查询计划中可见）。 **CardinalityEstimationModelVersion="130"**| 
|列存储索引的批处理模式与行模式更改：<br /><ul><li>具有列存储索引的表上的排序处于行模式 <li>开窗函数聚合在行模式（如 `LAG` 或 `LEAD`）下运行 <li>具有多个不同子句的列存储表的查询在行模式下运行 <li>在 MAXDOP 1 下运行或具有串行计划的查询在行模式下执行</li></ul>| 列存储索引的批处理模式与行模式更改：<br /><ul><li>具有列存储索引的表上的排序现在处于批处理模式 <li>开窗聚合现在在批处理模式（如 `LAG` 或 `LEAD`）下运行 <li>具有多个不同子句的列存储表的查询在批处理模式下运行 <li>在 MAXDOP 1 下运行或具有串行计划的查询在批处理模式下执行</li></ul>|  
|可以自动更新统计信息。 | 自动更新统计信息的逻辑对大型表更主动。  在实践中，这应减少以下情况：对于经常查询新插入的行，但是未更新统计信息以包括这些值的查询，客户遇到性能问题。 |  
|在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，跟踪 2371 默认情况下会关闭。 | 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中，[Trace 2371（跟踪 2371）](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/)默认情况下会打开。 跟踪标志 2371 告知自动统计信息更新程序在具有许多行的表中采样更小但更智能的行子集。 <br/> <br/> 一个重要改进是在采样中包括更多最近插入的行。 <br/> <br/> 另一个改进是让查询在更新统计信息进程运行期间运行，而不阻塞查询。 |  
|对于级别 120，统计信息通过单线程进程进行采样。|对于级别 130，统计信息通过多线程进程进行采样。 |  
|253 传入外键是限制。| 给定表可以通过最多 10,000 个传入外键或类似引用进行引用。 有关限制，请参阅 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)。 |  
|允许使用弃用的 MD2、MD4、MD5、SHA 和 SHA1 哈希算法。|只允许使用 SHA2_256 和 SHA2_512 哈希算法。|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 包括对某些数据类型转换和某些不常见操作的改进。 有关详细信息，请参阅 [SQL Server 2016 improvements in handling some data types and uncommon operations（SQL Server 2016 在处理某些数据类型和不常见操作方面所做的改进）](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon)。|
|STRING_SPLIT 函数不可用。|STRING_SPLIT 函数在兼容性级别 130 或更高级别下可用。 如果数据库兼容性级别低于 130，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将无法找到并执行 STRING_SPLIT 函数。|
  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 之前的早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中处于跟踪标志 4199 下的修补程序现在默认情况下会启用。 具有兼容性模式 130。 跟踪标志 4199 仍会适用于在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 之后发布的新查询优化器修补程序。 若要在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中使用较旧的查询优化器，必须选择兼容级别 110。 有关跟踪标志 4199 的信息，请参阅[跟踪标志 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)。  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>较低兼容性级别和级别 120 之间的差异  
 本节介绍随兼容性级别 120 引入的新行为。  
  
|兼容性级别设置为 110 或更低|兼容性级别设置为 120|  
|--------------------------------------------------|-----------------------------------------|  
|使用旧版查询优化器。|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 包括对创建和优化查询计划的组件的显著改进。 这个新的查询优化器功能依赖于使用数据库兼容性级别 120。 若要利用这些改进，应使用数据库兼容性级别 120 开发新的数据库应用程序。 应对从较早版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中迁移的应用程序进行仔细测试，以便确认保持或改进了好的性能。 如果性能下降，可以将数据库兼容性级别设置为 110 或更低，以便使用较早的查询优化器方法。<br /><br /> 数据库兼容级别 120 使用针对现代数据仓库和 OLTP 工作负荷进行优化的新基数估计器。 在因为性能问题将数据库兼容级别设置为 110 前，请参阅 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [数据库引擎中的新增功能](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)主题的“查询计划”一节中的建议。|  
|如果兼容级别低于 120，则在将 **date** 值转换为字符串值时语言设置将被忽略。 请注意，此行为仅特定于 **date** 类型。 请参阅下面“示例”部分中的“示例 B”。|将 **date** 值转换为字符串值时，不忽略语言设置。|  
|`EXCEPT` 子句右侧的递归引用产生无限循环。 下面“示例”部分中的示例 C 演示此行为。|`EXCEPT` 子句中的递归引用产生遵从 ANSI SQL 标准的错误。|  
|递归公用表表达式 (CTE) 允许重复的列名。|递归 CTE 不允许列名重复。|  
|如果更改触发器，则启用禁用的触发器。|更改触发器不更改触发器的状态（已启用或已禁用）。|  
|OUTPUT INTO 表子句忽略 `IDENTITY_INSERT SETTING = OFF`，并允许插入显式值。|将 `IDENTITY_INSERT` 设置为 OFF 后，不能为表中的标识列插入显式值。|  
|将数据库包含设置为部分包含后，验证 `MERGE` 语句的 `OUTPUT` 子句中的 `$action` 字段可能会返回排序规则错误。|`MERGE` 语句的 `$action` 子句返回的值的排序规则是数据库排序规则而非服务器排序规则，因此不会返回排序规则冲突错误。|  
|`SELECT INTO` 语句始终创建单线程插入操作。|`SELECT INTO` 语句可创建并行插入操作。 插入大量行时，并行操作可提高性能。|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>较低兼容性级别与级别 110 和 120 之间的差异  
 本节介绍随兼容性级别 110 引入的新行为。   此部分也适用于级别 120。  
  
|兼容性级别设置为 100 或更低|至少为 110 的兼容性级别设置|  
|--------------------------------------------------|--------------------------------------------------|  
|公共语言运行时 (CLR) 数据库对象用 CLR 的版本 4 执行。 但会避免在 CLR 的版本 4 中引入的某些行为更改。 有关详细信息，请参阅 [CLR 集成中的新增功能](../../relational-databases/clr-integration/clr-integration-what-s-new.md)。|CLR 数据库对象用 CLR 的版本 4 执行。|  
|XQuery 函数 **string-length** 和 **substring** 将每个代理项计为两个字符。|XQuery 函数 **string-length** 和 **substring** 将每个代理项计为一个字符。|  
|在递归公用表表达式 (CTE) 查询中允许 `PIVOT`。 然而，当每个分组有多个行时，该查询返回不正确的结果。|在递归公用表表达式 (CTE) 查询中不允许 `PIVOT`。 将返回错误。|  
|RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，可以通过任何兼容性级别对使用 RC4 或 RC4_128 加密的材料进行解密。|不能使用 RC4 或 RC4_128 加密新材料。 而是使用一种较新的算法，如 AES 算法之一。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中，可以通过任何兼容性级别对使用 RC4 或 RC4_128 加密的材料进行解密。|  
|对 **time** 和 **datetime2** 数据类型的 `CAST` 和 `CONVERT` 操作的默认样式为 121，当在计算列表达式中使用这些类型时除外。 对于计算列，默认样式为 0。 当创建用于涉及自动参数化的查询中或约束定义中的计算列时，此行为会影响计算列。<br /><br /> 下面“示例”部分中的示例 D 显示样式 0 与 121 之间的差异。 它并不演示上面所述的行为。 有关日期和时间样式的详细信息，请参阅 [CAST 和 CONVERT (Transact SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。|兼容级别为 110 时，对 **time** 和 **datetime2** 数据类型的 `CAST` 和 `CONVERT` 操作的默认样式始终为 121。 如果您的查询依赖旧行为，请使用低于 110 的兼容性级别或在受影响的查询中显式指定 0 样式。<br /><br /> 将数据库升级到兼容性级别 110 将不更改已存储到磁盘的用户数据。 您必须相应手动更正此数据。 例如，如果使用了 `SELECT INTO` 来从包含上述计算列表达式的源创建表，将存储数据（使用样式 0）而非存储计算列定义本身。 您需要手动更新此数据，以匹配样式 121。|  
|在分区视图中引用的远程表的所有 **smalldatetime** 类型的列都将映射为 **datetime**。 本地表中相应的列（在选择列表中的相同序号位置中）必须为 **datetime** 类型。|在分区视图中引用的远程表的所有 **smalldatetime** 类型的列都将映射为 **smalldatetime**。 本地表中相应的列（在选择列表中的相同序号位置中）必须为 **smalldatetime** 类型。<br /><br /> 在升级到 110 后，分布式分区视图将由于数据类型不匹配而失败。 可以通过将针对远程表的数据类型更改为 **datetime** 或者将本地数据库的兼容级别设置为 100 或更低，解决上述问题。|  
|`SOUNDEX` 函数实现以下规则：<br /><br /> 1) 当分隔两个具有相同 `SOUNDEX` 代码的辅音时，将忽略大写 H 或大写 W。<br /><br /> 2) 如果 *character_expression* 的前 2 个字符具有相同的 `SOUNDEX` 代码，则将包含这两个字符。 如果一组并行辅音具有相同的 `SOUNDEX` 代码，则将不包含它们，第一个辅音除外。|`SOUNDEX` 函数实现以下规则：<br /><br /> 1) 如果大写 H 或大写 W 分隔具有相同 `SOUNDEX` 代码的两个辅音，则将忽略右侧的辅音<br /><br /> 2) 如果一组并行辅音具有相同的 `SOUNDEX` 代码，则将不包含它们，第一个辅音除外。<br /><br /> <br /><br /> 其他规则可能导致由 `SOUNDEX` 函数计算的值不同于在更低数据库兼容级别时计算的值。 在升级到兼容级别 110 后，可能需要重新生成使用 `SOUNDEX` 函数的索引、堆或 CHECK 约束。 有关详细信息，请参阅 [SOUNDEX (Transact-SQL)](../../t-sql/functions/soundex-transact-sql.md)。|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>兼容性级别 90 和兼容性级别 100 之间的差异  
 本节介绍随兼容性级别 100 引入的新行为。  
  
|兼容性级别设置为 90|兼容性级别设置为 100|影响的可能性|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|对于多语句表值函数，在创建它们时，无论会话级别设置如何，QUOTED_IDENTIFER 设置始终为 ON。|在创建多语句表值函数时，会遵循 QUOTED IDENTIFIER 会话设置。|Medium|  
|在创建或更改分区函数时，会评估函数中的 **datetime** 和 **smalldatetime** 文字，并假定语言设置为 US_English。|使用当前语言设置来评估该分区函数中的 **datetime** 和 **smalldatetime** 文字。|Medium|  
|允许在 `INSERT` 和 `SELECT INTO` 语句中使用（并忽略）`FOR BROWSE` 子句。|不允许在 `INSERT` 和 `SELECT INTO` 语句中使用 `FOR BROWSE` 子句。|Medium|  
|`OUTPUT` 子句中允许使用全文谓词。|`OUTPUT` 子句中不允许使用全文谓词。|Low|  
|`CREATE FULLTEXT STOPLIST`、`ALTER FULLTEXT STOPLIST` 和 `DROP FULLTEXT STOPLIST` 不受支持。 系统非索引字表自动与新的全文检索相关联。|`CREATE FULLTEXT STOPLIST`、`ALTER FULLTEXT STOPLIST` 和 `DROP FULLTEXT STOPLIST` 受支持。|Low|  
|`MERGE` 不作为保留关键字强制应用。|MERGE 是完全保留的关键字。 在 100 和 90 兼容级别下，都支持 `MERGE` 语句。|Low|  
|使用 INSERT 语句的 \<dml_table_source> 参数会引发语法错误。|您可以捕获嵌套的 INSERT、UPDATE、DELETE 或 MERGE 语句中 OUTPUT 子句的结果，然后将这些结果插入目标表或视图。 这通过使用 INSERT 语句的 \<dml_table_source> 参数来实现。|Low|
|除非指定 `NOINDEX`，否则 `DBCC CHECKDB` 或 `DBCC CHECKTABLE` 将对单个表或索引视图及其所有非聚集索引和 XML 索引同时执行物理和逻辑一致性检查。 不支持空间索引。|除非指定 `NOINDEX`，否则 `DBCC CHECKDB` 或 `DBCC CHECKTABLE` 将对单个表及其所有非聚集索引同时执行物理和逻辑一致性检查。 但是，在默认情况下，仅对 XML 索引、空间索引和索引视图执行物理一致性检查。<br /><br /> 如果指定了 `WITH EXTENDED_LOGICAL_CHECKS`，则将对索引视图、XML 索引和空间索引（如果存在）执行逻辑检查。 默认情况下，先执行物理一致性检查，然后执行逻辑一致性检查。 如果还指定了 `NOINDEX`，则仅执行逻辑检查。|Low|  
|如果将 OUTPUT 子句和数据操作语言 (DML) 语句一起使用，并且在语句执行过程中发生运行时错误，则会终止并回滚整个事务。|如果将 `OUTPUT` 子句和数据操作语言 (DML) 语句一起使用，并且在语句执行过程中发生运行时错误，则行为取决于 `SET XACT_ABORT` 设置。 如果 `SET XACT_ABORT` 设置为 OFF，则由使用 `OUTPUT` 子句的 DML 语句所生成的语句中止错误将终止该语句，但批处理的执行仍会继续，并且不会回滚事务。 如果 `SET XACT_ABORT` 设置为 ON，则由使用 OUTPUT 子句的 DML 语句所生成的全部运行时错误都将终止批处理，并回滚事务。|Low|  
|CUBE 和 ROLLUP 不作为保留关键字强制应用。|`CUBE` 和 `ROLLUP` 是 GROUP BY 子句中的保留关键字。|Low|  
|对 XML **anyType** 类型的元素应用严格验证。|对 **anyType** 类型的元素应用宽松验证。 有关详细信息，请参阅[通配符组成部分和内容验证](../../relational-databases/xml/wildcard-components-and-content-validation.md)。|Low|  
|数据操作语言语句不能查询或修改特殊属性 **xsi:nil** 和 **xsi:type**。<br /><br /> 这意味着 `/e/@xsi:nil` 失败，同时 `/e/@*` 忽略 **xsi:nil** 和 **xsi:type** 属性。 但是，`/e` 返回 **xsi:nil** 和 **xsi:type** 属性，以保持与 `SELECT xmlCol` 的一致性，即使 `xsi:nil = "false"` 也是如此。|特殊属性 **xsi:nil** 和 **xsi:type** 作为常规属性存储，不能查询和修改。<br /><br /> 例如，执行查询 `SELECT x.query('a/b/@*')` 会返回包括 **xsi: nil** 和 **xsi: type** 在内的所有属性。 若要在查询中排除这些类型，请用 `@*[namespace-uri(.) != "`insert xsi namespace uri`"` 替换 `@*`，而不是用 `(local-name(.) = "type"` 或 `local-name(.) ="nil".` 来替换|Low|  
|用于将 XML 常量字符串值转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 类型的用户定义函数被标记为确定的。|用于将 XML 常量字符串值转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 类型的用户定义函数被标记为不确定的。|Low|  
|不完全支持 XML 联合和列表类型。|完全支持联合和列表类型，包括以下功能：<br /><br /> 列表的联合<br /><br /> 联合的联合<br /><br /> 原子类型的列表<br /><br /> 联合的列表|Low|  
|当视图或内联表值函数中包含 xQuery 方法时，不对该方法所需的 SET 选项进行验证。|当视图或内联表值函数中包含 xQuery 方法时，对该方法所需的 SET 选项进行验证。 如果该方法的 SET 选项设置不正确，将引发一个错误。|Low|  
|包含行尾字符（回车符和换行符）的 XML 属性值不根据 XML 标准进行规范化。 即返回回车符和换行符，而不是单个换行符。|包含行尾字符（回车符和换行符）的 XML 属性值会根据 XML 标准进行规范化。 也就是说，外部已分析实体（包括文档实体）中的所有换行符都会在输入时进行规范化，方法是将两字符序列 #xD #xA 和后面没有跟 #xA 的所有 #xD 都转换为单个 #xA 字符。<br /><br /> 使用属性来传输包含行尾字符的字符串值的应用程序接收到的这些字符将和提交时有所不同。 若要避免规范化过程，请使用 XML 数字字符实体对所有行尾字符进行编码。|Low|  
|`ROWGUIDCOL` 和 `IDENTITY` 列属性可能错误地命名为约束。 例如，`CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` 语句可以执行，但约束名不会保留，也无法让用户访问。|`ROWGUIDCOL` 和 `IDENTITY` 列属性不能命名为约束。 返回错误 156。|Low|  
|使用双向赋值（如 `UPDATE T1 SET @v = column_name = <expression>`）来更新列会产生意外后果，因为在语句执行过程中，可以在其他子句（如 `WHER` 和 `ON` 子句）中使用变量的实时值，而不是使用语句起始值。 这会导致谓词的含义无法预测地逐行变化。<br /><br /> 只有在兼容性级别设置为 90 时，此行为才适用。|使用双向赋值来更新列会产生预期的结果，因为在语句执行过程中，只会访问列的语句起始值。|Low|  
|请参阅下面“示例”部分中的“示例 E”。|请参阅下面“示例”部分中的“示例 F”。|Low|  
|ODBC 函数 {fn CONVERT()} 使用语言的默认日期格式。 对于有些语言，默认格式为 YDM，这会导致在将 CONVERT() 与要求使用 YMD 格式的其他函数（如 `{fn CURDATE()}`）结合使用时出现转换错误。|在转换为 ODBC 数据类型 SQL_TIMESTAMP、SQL_DATE、SQL_TIME、SQLDATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP 时，ODBC 函数 `{fn CONVERT()}` 使用样式 121（一种独立于语言的 YMD 格式）。|Low|  
|日期时间内部函数（如 DATEPART）不需要字符串输入值，即可成为有效的日期时间文字。 例如，`SELECT DATEPART (year, '2007/05-30')` 会编译成功。|日期时间内部函数（如 `DATEPART`）需要字符串输入值，才能成为有效的日期时间文字。 在使用无效的日期时间文字时，会返回错误 241。|Low|  
  
## <a name="reserved-keywords"></a>保留关键字  
 兼容性设置还确定了[!INCLUDE[ssDE](../../includes/ssde-md.md)]所保留的关键字。 下表显示了每个兼容性级别所引入的保留关键字。  
  
|兼容性级别设置|保留关键字|  
|----------------------------------|-----------------------|  
|130|待定。|  
|120|无。|  
|110|WITHIN GROUP、TRY_CONVERT、SEMANTICKEYPHRASETABLE、SEMANTICSIMILARITYDETAILSTABLE、SEMANTICSIMILARITYTABLE|  
|100|CUBE、MERGE、ROLLUP|  
|90|EXTERNAL、PIVOT、UNPIVOT、REVERT、TABLESAMPLE|  
  
 在给定兼容性级别，保留关键字包括在该级别或较低级别引入的所有关键字。 例如，对于兼容性级别为 110 的应用程序，将保留上表列出的所有关键字。 在较低的兼容性级别中，级别 100 的关键字仍保留有效的对象名，但与这些关键字相对应的级别 110 的语言功能将不可用。  
  
 一旦引入，关键字便会保持为保留关键字。 例如，在兼容性级别 90 中引入的保留关键字 PIVOT 在级别 100、110 和 120 中也被保留。  
  
 如果某一应用程序使用对其保留级别而言是关键字的标识符，则该应用程序将失败。 若要解决这一问题，请用方括号 (**[]**) 或引号 (**""**) 括起该标识符；例如，若要将使用标识符 **EXTERNAL** 的应用程序升级为兼容级别 90，可以将该标识符更改为 **[EXTERNAL]** 或 **"EXTERNAL"**。  
  
 有关详细信息，请参阅[保留关键字 (Transact-SQL) ](../../t-sql/language-elements/reserved-keywords-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-compatibility-level"></a>A. 更改兼容性级别  
 以下示例将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的兼容级别更改为 `110,`[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 以下示例返回当前数据库的兼容级别。  
  
```sql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>B. 忽略 SET LANGUAGE 语句（除非低于兼容级别 120）  
 只有兼容级别低于 120 时，以下查询才会忽略 SET LANGUAGE 语句。  
  
```sql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>C.  
 对于 110 或更低的兼容级别设置，EXCEPT 子句右侧的递归引用产生无限循环。  
  
```sql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>D.  
 此示例显示样式 0 和 121 之间的差异。 有关日期和时间样式的详细信息，请参阅 [CAST 和 CONVERT (Transact SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
```sql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>E.  
 在包含顶级 UNION 运算符的语句中，允许使用变量赋值，但会返回意外的结果。 例如，在以下语句中，将来自两个表的联合的 `@v` 列的值赋给局部变量 `BusinessEntityID`。 按照定义，如果 SELECT 语句返回多个值，则将返回的最后一个值赋给变量。 在这种情况下，会正确地将最后一个值赋给变量，但还会返回 SELECT UNION 语句的结果集。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 110;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>F.  
 在包含顶级 UNION 运算符的语句中不允许变量赋值。 返回错误 10734。 若要纠正该错误，请重写查询，如下例所示。  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [保留关键字 (Transact-SQL)](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [查看或更改数据库的兼容级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
