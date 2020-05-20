---
title: sys. database_query_store_options （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 752b8780b810f20e2fb71f2a5b8c55fad044981c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828180"
---
# <a name="sysdatabase_query_store_options-transact-sql"></a>sys. database_query_store_options （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回此数据库的查询存储选项。  
  
**适用**于： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本）、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 。
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|指示查询存储所需的操作模式，由用户显式设置。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|查询存储所需操作模式的文本说明：<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|指示查询存储的操作模式。 除了用户需要的所需状态的列表之外，实际状态可能是错误状态。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 错误|  
|**actual_state_desc**|**nvarchar(60)**|查询存储实际操作模式的文本说明。<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 在某些情况下，实际状态与所需状态不同：<br />-如果数据库设置为只读模式，或者查询存储大小超过其配置的配额，则查询存储可能会在只读模式下运行（即使用户指定了读写）。<br />-在极端方案中查询存储可能会由于内部错误而进入错误状态。 如果发生这种情况，对于 SQL 2017 及更高版本，可以通过 `sp_query_store_consistency_check` 在受影响的数据库中执行存储过程来恢复查询存储。 如果运行 `sp_query_store_consistency_check` 不适用于 SQL 2016，你将需要通过运行`ALTER DATABASE [YourDatabaseName] SET QUERY_STORE CLEAR ALL;`|  
|**readonly_reason**|**int**|当 READ_WRITE **desired_state_desc**并且**actual_state_desc** READ_ONLY 时， **readonly_reason**返回一个位图以指示查询存储处于只读模式的原因。<br /><br /> **1** -数据库处于只读模式<br /><br /> **2** -数据库处于单用户模式<br /><br /> **4** -数据库处于紧急模式<br /><br /> **8** -数据库为辅助副本（适用于 Always On 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 异地复制）。 只能在**可读**辅助副本上有效观察此值<br /><br /> **65536** -查询存储已达到 MAX_STORAGE_SIZE_MB 选项设置的大小限制。<br /><br /> **131072** -查询存储中的不同语句数已达到内部内存限制。 请考虑删除不需要的查询或升级到更高的服务层，以允许将查询存储传输到读写模式。<br />适用对象：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  。<br /><br /> **262144** -等待保留在磁盘上的内存中项的大小已达到内部内存限制。 查询存储将暂时处于只读模式，直到内存中的项保留在磁盘上。 <br />适用对象：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  。<br /><br /> **524288** -数据库已达到磁盘大小限制。 查询存储是用户数据库的一部分，因此，如果数据库没有更多的可用空间，这意味着查询存储不能再进一步增长。<br />适用对象：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  。 <br /> <br /> 若要将查询存储操作模式改回为读写模式，请参阅验证查询存储是否正在[与查询存储的最佳实践](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify)**持续收集查询数据**部分。|  
|**current_storage_size_mb**|**bigint**|磁盘上的查询存储大小（以 mb 为单位）。|  
|**flush_interval_seconds**|**bigint**|将查询存储数据定期刷新到磁盘的时间（以秒为单位）。 默认值为**900** （15分钟）。<br /><br /> 使用语句进行更改 `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` 。|  
|**interval_length_minutes**|**bigint**|统计信息聚合间隔（分钟）。 不允许使用任意值。 使用以下项之一：1、5、10、15、30、60和1440分钟。 默认值为**60**分钟。|  
|**max_storage_size_mb**|**bigint**|查询存储的最大磁盘大小，以兆字节（MB）为单位。 默认值为**100** MB。<br />对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 高级版，默认值为 1 GB，对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 基本版，默认值为 10 MB。<br /><br /> 使用语句进行更改 `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` 。|  
|**stale_query_threshold_days**|**bigint**|不包含策略设置的查询保留在查询存储中的天数。 默认值为 **30**。 设置为0可禁用保留策略。<br />对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 基本版，默认值为 7 天。<br /><br /> 使用语句进行更改 `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` 。|  
|**max_plans_per_query**|**bigint**|限制最大存储计划数。 默认值为**200**。 如果达到最大值，查询存储将停止捕获该查询的新计划。 如果设置为0，则将删除已捕获计划数的限制。<br /><br /> 使用语句进行更改 `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` 。|  
|**query_capture_mode**|**smallint**|当前处于活动状态的查询捕获模式：<br /><br /> **1** = 所有-捕获所有查询。 这是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本）的默认配置值。<br /><br /> 2 = 根据执行计数和资源消耗自动捕获相关查询。 这是 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 的默认配置值。<br /><br /> 3 = 无-停止捕获新查询。 查询存储将继续为已经捕获的查询收集编译和运行时统计信息。 请谨慎使用此配置，因为可能会遗漏捕获重要的查询。|  
|**query_capture_mode_desc**|**nvarchar(60)**|查询存储实际捕获模式的文本说明：<br /><br /> 全部（默认值 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ）<br /><br /> **自动**（默认值 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ）<br /><br /> 无|  
|**size_based_cleanup_mode**|**smallint**|控制当数据总量接近最大大小时是否自动激活清除：<br /><br /> 0 = 不会自动激活基于大小的清理。<br /><br /> **1** = 如果磁盘上的大小达到*max_storage_size_mb*的**90%** ，将自动激活自动大小的清理。 这是默认的配置值。<br /><br />基于大小的清除首先会删除成本最低和最旧的查询。 达到约**80%** 的*max_storage_size_mb*时，它将停止。|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|查询存储的实际基于大小的清理模式的文本说明：<br /><br /> OFF <br /> **自动**（默认值）|  
|**wait_stats_capture_mode**|**smallint**|控制查询存储是否执行等待统计信息的捕获： <br /><br /> 0 = OFF <br /> **1** = 开启<br /> **适用于**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 及更高版本。|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|实际等待统计信息捕获模式的文本说明： <br /><br /> OFF <br /> **启用**（默认值）<br /> **适用于**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 及更高版本。| 
  
## <a name="permissions"></a>权限  
 需要 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys. query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys. query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. fn_stmt_sql_handle_from_sql_stmt &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
