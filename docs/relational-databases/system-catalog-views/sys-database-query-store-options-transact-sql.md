---
title: sys.database_query_store_options (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8f1169e430a9ab6295862a3434f08967e01f33f
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087776"
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回此数据库的查询存储选项。  
  
适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|指示查询存储，由用户显式设置的所需的操作模式。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(60)**|查询存储的所需的操作模式的文本说明：<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|指示查询存储的操作模式。 除了所需的用户的所需状态的列表，实际状态可以是错误状态。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 错误|  
|**actual_state_desc**|**nvarchar(60)**|查询存储的实际操作模式的文本说明。<br />OFF<br />READ_ONLY<br />READ_WRITE<br />error<br /><br /> 当实际状态为不同于所需的状态时，有些情况下：<br />-如果将数据库设置为只读模式，或如果查询存储大小超过其配置的配额，即使用户已指定读写，Query Store 可能会在只读模式下操作。<br />-在极端情况下查询存储可以因内部错误而进入错误状态。 如果发生这种情况，可以通过执行恢复查询存储`sp_query_store_consistency_check`受影响的数据库中的存储过程。|  
|**readonly_reason**|**int**|当**desired_state_desc**为 READ_WRITE 和**actual_state_desc**为 READ_ONLY， **readonly_reason**返回有点映射以指示查询存储中原因只读模式。<br /><br /> **1** -数据库处于只读模式<br /><br /> **2** -数据库处于单用户模式<br /><br /> **4** -数据库处于紧急模式<br /><br /> **8** -数据库是辅助副本 (适用于 Always On 和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]异地复制)。 此值可以有效地观察到仅在上**可读**辅助副本<br /><br /> **65536** -查询存储已达到 MAX_STORAGE_SIZE_MB 选项设置的大小限制。<br /><br /> **131072** -查询存储中的不同语句的数量已达到内部内存限制。 请考虑删除不需要的查询或升级到更高版本的服务层，若要启用将查询存储传输到读写模式。<br />**适用于：** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> **262144** -等待保留在磁盘上的内存中项的大小已达到内部内存限制。 查询存储将在只读模式下，暂时直到内存中的项保留在磁盘上。 <br />**适用于：** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> **524288** -数据库已达到磁盘大小限制。 查询存储是一部分的用户数据库中，因此如果对于数据库，这意味着没有更多可用空间查询存储无法增加，进一步不再。<br />**适用于：** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 <br /> <br /> 若要切换的查询存储操作模式后，要读写，请参阅**验证查询存储持续收集查询数据是否**一部分[Query store 最佳做法](../../relational-databases/performance/best-practice-with-the-query-store.md#Verify)。|  
|**current_storage_size_mb**|**bigint**|查询存储的大小以兆字节的磁盘上。|  
|**flush_interval_seconds**|**bigint**|用于查询的常规刷新期间将数据存储到磁盘以秒为单位。 默认值是**900** （15 分钟）。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)`语句。|  
|**interval_length_minutes**|**bigint**|统计信息聚合间隔以分钟为单位。 不允许任意值。 使用下列其中一个：1、 5、 10、 15、 30、 60 和 1440年分钟。 默认值是**60**分钟。|  
|**max_storage_size_mb**|**bigint**|兆字节 (MB) 中的查询存储的最大磁盘大小。 默认值是**100** MB。<br />有关[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]高级版，默认值为 1 GB 和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]基本版，默认值为 10 MB。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)`语句。|  
|**stale_query_threshold_days**|**bigint**|查询存储中保留任何策略设置的查询的天数。 默认值是**30**。 设置为 0 以禁用保留策略。<br />对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 基本版，默认值为 7 天。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )`语句。|  
|**max_plans_per_query**|**bigint**|限制存储计划的最大数量。 默认值是**200**。 如果达到最大值，Query Store 停止捕获新查询的计划。 设置为 0 会删除在捕获计划的数量方面的限制。<br /><br /> 通过更改`ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)`语句。|  
|**query_capture_mode**|**smallint**|当前处于活动状态查询捕获模式：<br /><br /> **1** = ALL-捕获所有查询。 这是默认配置值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。<br /><br /> 2 = AUTO-基于执行计数和资源消耗捕获相关查询。 这是默认配置值[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。<br /><br /> 3 = 无-停止捕获新查询。 查询存储将继续为已经捕获的查询收集编译和运行时统计信息。 谨慎使用此配置，因为你可能会错过捕获重要的查询。|  
|**query_capture_mode_desc**|**nvarchar(60)**|查询存储的实际捕获模式的文本说明：<br /><br /> 所有 (默认为[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> **自动**(默认为[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> 无|  
|**size_based_cleanup_mode**|**smallint**|控制当数据总量接近最大大小时是否自动激活清除：<br /><br /> 0 = OFF 的大小不会自动激活基于的清除。<br /><br /> **1** = AUTO-基于的清理将自动激活时磁盘上的大小达到的大小**90%** 的*max_storage_size_mb*。 这是默认的配置值。<br /><br />基于大小的清除首先会删除成本最低和最旧的查询。 它将停止时大约**百分之八十**的*max_storage_size_mb*为止。|  
|**size_based_cleanup_mode_desc**|**nvarchar(60)**|查询存储的实际基于大小的清理模式的文本说明：<br /><br /> OFF <br /> **自动**（默认值）|  
|**wait_stats_capture_mode**|**smallint**|控制查询存储是否执行捕获等待统计信息： <br /><br /> 0 = OFF <br /> **1** = ON<br /> **适用范围**： [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|
|**wait_stats_capture_mode_desc**|**nvarchar(60)**|实际等待统计信息捕获模式的文本说明： <br /><br /> OFF <br /> **ON** （默认值）<br /> **适用范围**： [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
  
## <a name="permissions"></a>权限  
 需要 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
