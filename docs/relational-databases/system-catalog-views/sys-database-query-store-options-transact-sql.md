---
title: sys.database_query_store_options (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1c048c66e20e210f84d26dbff492aede56839fe2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回此数据库的查询存储选项。  
  
**适用范围**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**int**|指示 Query Store，由用户显式设置的所需的操作模式。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(64)**|查询存储的所需的操作模式的文本说明：<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**int**|指示 Query Store 的操作模式。 除了所需的用户的所需状态的列表，实际状态可以是错误状态。<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = 错误|  
|**actual_state_desc**|**nvarchar(64)**|查询存储的实际操作模式的文本说明。<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> 当实际状态不同于所需的状态时在一些情况下：<br /><br /> Query Store 可能运行在只读模式下，即使由用户指定了读写。 例如，可能会发生如果数据库处于只读模式或 Query Store 大小超出了配额。<br /><br /> 极罕见，查询 Store 最终可能会处于错误状态由于内部错误。 如果发生这种情况，可以通过执行恢复 Query Store **sp_query_store_consistency_check**存储内受影响的数据库的过程。|  
|**readonly_reason**|**int**|当**desired_state_desc**为 READ_WRITE 和**actual_state_desc**为 READ_ONLY， **readonly_reason**返回有点映射以指示查询存储为何中只读模式。<br /><br /> 1 – 数据库处于只读模式<br /><br /> 2 – 数据库处于单用户模式<br /><br /> 4 - 数据库处于紧急模式<br /><br /> 8 - 数据库是辅助副本（适用于Always On和Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 地理复制）。 此值仅在上可以有效地观察到**可读**辅助副本<br /><br /> 65536 – Query Store 已达到 MAX_STORAGE_SIZE_MB 选项设置的大小限制。<br /><br /> 131072-查询存储中的不同语句的数量已达到内部内存限制。 请考虑删除不需要的查询或升级到更高版本的服务层，以便将查询存储传输到读写模式。<br />仅适用于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br /> 262144 – 内存中等待的项在磁盘上保存大小已达到内部内存限制。 内存中的项将保留在磁盘之前暂时，查询存储将处于只读模式。 <br />仅适用于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br />524288 – 数据库已达到磁盘大小限制。 查询存储是的一部分用户数据库中，因此如果没有更多可用空间的数据库，意味着 Query Store 无法进一步增长不再。<br />仅适用于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 <br /> <br /> 若要切换的查询存储操作模式后，读写，请参阅**验证 Query Store 持续收集查询数据是**部分[Query store 最佳实践](../../relational-databases/performance/best-practice-with-the-query-store.md)。|  
|**current_storage_size_mb**|**bigint**|单位为兆字节的磁盘上的 Query Store 大小。|  
|**flush_interval_seconds**|**bigint**|定义用于磁盘到正则刷新 Query Store 数据的时间段。 默认值为 900 （15 分钟）。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)`语句。|  
|**interval_length_minutes**|**bigint**|统计信息聚合时间间隔。 不允许任意值。 使用以下项之一： 1、 5、 10、 15、 30、 60 和 1440年分钟。 默认值为 60 分钟。|  
|**max_storage_size_mb**|**bigint**|查询存储的最大磁盘大小。 默认值为 100 MB。<br />对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 高级版，默认值为 1 Gb，对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 基本版，默认值则为 10 Mb。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)`语句。|  
|**stale_query_threshold_days**|**bigint**|任何策略设置的查询查询存储中保留的天数。 默认值为 30。 设置为 0 以禁用保留策略。<br />对于 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 基本版，默认值为 7 天。<br /><br /> 通过更改`ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )`语句。|  
|**max_plans_per_query**|**bigint**|限制存储计划的最大数目。 默认值为 200。 如果达到最大值后，Query Store 停止捕获新查询的计划。 设置为 0 中删除在捕获计划数方面的限制。<br /><br /> 通过更改`ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)`语句。|  
|**query_capture_mode**|**int**|当前处于活动状态的查询捕获模式：<br /><br /> 1 = ALL-捕获所有查询。 这是默认配置值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。<br /><br /> 2 = AUTO-基于执行计数和资源消耗捕获相关查询。 这是默认配置值[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。<br /><br /> 3 = NONE-停止捕获新查询。 查询存储将继续为已经捕获的查询收集编译和运行时统计信息。 谨慎使用此配置，因为可能会丢失捕获重要的查询。|  
|**query_capture_mode_desc**|**nvarchar(60)**|查询存储的实际捕获模式的文本说明：<br /><br /> 所有 (默认为[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> 自动 (默认为[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> 无|  
|**size_based_cleanup_mode**|**int**|控制当数据总量接近最大大小时是否自动激活清除：<br /><br /> 1 = OFF – 大小不会自动激活基于的清理。<br /><br /> 2 = AUTO 的大小在大小上的磁盘达到 90%时，基于的清理将被自动激活**max_storage_size_mb**。 这是默认的配置值。<br /><br />基于大小的清除首先会删除成本最低和最旧的查询。 在大约 80%的 max_storage_size_mb 处停止。|  
|**size_based_cleanup_mode_desc**|**int**|查询存储的实际基于大小的清理模式的文本说明：<br /><br /> OFF <br /><br /> 自动 （默认值）|  
|**wait_stats_capture_mode**|**int**|控制是否 Query Store 执行捕获等待统计信息： <br /><br /> 0 = OFF <br /><br /> 1 = ON<br /> **适用范围**： [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|实际等待统计信息捕获模式的文本说明： <br /><br /> OFF <br /><br /> （默认值）<br /> **适用范围**： [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。| 
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.query_context_settings &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
