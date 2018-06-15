---
title: sys.query_store_runtime_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 85bb7aa5bf91f8d357556adac9e58fb6ab83df24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182353"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含有关运行时执行统计信息查询信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|表示运行时执行统计信息的行标识符**plan_id**， **execution_type**和**runtime_stats_interval_id**。 它是唯一的仅为过去的运行时统计信息时间间隔。 对于当前处于活动状态的间隔可能会有表示引用的计划的运行时统计信息的多个行**plan_id**，与执行类型由**execution_type**。 通常情况下，一行表示运行时统计信息，将被刷新到磁盘，而其他 (s) 表示内存中状态。 因此，若要获得每个间隔的实际状态需要聚合度量值，通过分组**plan_id**， **execution_type**和**runtime_stats_interval_id**。 |  
|**plan_id**|**bigint**|外键。 将联接到[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外键。 将联接到[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**execution_type**|**tinyint**|确定类型的查询执行：<br /><br /> 0 – 常规执行 （成功完成）<br /><br /> 3 – 启动的客户端已中止执行<br /><br /> 4-异常已中止执行|  
|**execution_type_desc**|**nvarchar(128)**|执行类型字段的文本说明：<br /><br /> 0-常规<br /><br /> 3 – 中止<br /><br /> 4-异常|  
|**first_execution_time**|**datetimeoffset**|聚合间隔内的查询计划的第一个执行时间。|  
|**last_execution_time**|**datetimeoffset**|上次执行时间为查询计划在聚合时间间隔内。|  
|**count_executions**|**bigint**|个聚合间隔内的查询计划的执行的总计数。|  
|**avg_duration**|**float**|平均聚合时间间隔 （以微秒为单位报告） 的查询计划的持续时间。|  
|**last_duration**|**bigint**|在聚合时间间隔 （以微秒为单位报告） 内计划的查询的最后一个持续时间。|  
|**min_duration**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最小持续时间。|  
|**max_duration**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最长持续时间。|  
|**stdev_duration**|**float**|聚合时间间隔 （以微秒为单位报告） 的查询计划的持续时间标准偏差。|  
|**avg_cpu_time**|**float**|CPU 的平均时间 （以微秒为单位报告） 的聚合间隔的查询计划。|  
|**last_cpu_time**|**bigint**|在聚合时间间隔 （以微秒为单位报告） 内计划的查询的最后一个 CPU 时间。|  
|**min_cpu_time**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最小 CPU 时间。|  
|**max_cpu_time**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最长 CPU 时间。|  
|**stdev_cpu_time**|**float**|聚合时间间隔 （以微秒为单位报告） 的查询计划的 CPU 时间标准偏差。|  
|**avg_logical_io_reads**|**float**|平均的逻辑 IO 读取数为聚合间隔内的查询计划。 （表示为大量的读取的 8 KB 页数）。|  
|**last_logical_io_reads**|**bigint**|最后一个的逻辑 IO 读取数为聚合间隔内的查询计划。 （表示为大量的读取的 8 KB 页数）。|  
|**min_logical_io_reads**|**bigint**|最小的逻辑 IO 读取数为聚合间隔内的查询计划。 （表示为大量的读取的 8 KB 页数）。|  
|**max_logical_io_reads**|**bigint**|最大的逻辑 IO 读取数为聚合间隔内的查询计划。（表示为大量的读取的 8 KB 页数）。 |  
|**stdev_logical_io_reads**|**float**|逻辑 IO 读取数聚合间隔内的查询计划的标准偏差。 （表示为大量的读取的 8 KB 页数）。|  
|**avg_logical_io_writes**|**float**|聚合间隔内的查询计划为编写逻辑 IO 的平均数。|  
|**last_logical_io_writes**|**bigint**|最后一个的逻辑 IO 写入次数的聚合间隔内的查询计划。|  
|**min_logical_io_writes**|**bigint**|最小的逻辑 IO 写入次数的聚合间隔内的查询计划。|  
|**max_logical_io_writes**|**bigint**|最大的逻辑 IO 写入次数的聚合间隔内的查询计划。|  
|**stdev_logical_io_writes**|**float**|聚合间隔内的查询计划的标准偏差写入次数逻辑 IO。|  
|**avg_physical_io_reads**|**float**|平均的物理 IO 读取数为聚合时间间隔 （以 8 KB 页读取数为单位表示） 的查询计划。|  
|**last_physical_io_reads**|**bigint**|最后一个的物理 IO 读取数为聚合时间间隔 （以 8 KB 页读取数为单位表示） 的查询计划。|  
|**min_physical_io_reads**|**bigint**|最小数量的物理 IO 读取聚合时间间隔 （以 8 KB 页读取数为单位表示） 的查询计划。|  
|**max_physical_io_reads**|**bigint**|最大的物理 IO 读取数为聚合时间间隔 （以 8 KB 页读取数为单位表示） 的查询计划。|  
|**stdev_physical_io_reads**|**float**|物理 IO 读取数聚合时间间隔 （以 8 KB 页读取数为单位表示） 的查询计划的标准偏差。|  
|**avg_clr_time**|**float**|CLR 的平均时间 （以微秒为单位报告） 的聚合间隔的查询计划。|  
|**last_clr_time**|**bigint**|查询的最后一个 CLR 时间计划在聚合时间间隔 （以微秒为单位报告） 内。|  
|**min_clr_time**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最小 CLR 时间。|  
|**max_clr_time**|**bigint**|聚合时间间隔 （以微秒为单位报告） 的查询计划的最大 CLR 时间。|  
|**stdev_clr_time**|**float**|聚合时间间隔 （以微秒为单位报告） 的查询计划的 CLR 时间标准偏差。|  
|**avg_dop**|**float**|聚合间隔内的查询计划的平均 DOP （并行度）。|  
|**last_dop**|**bigint**|聚合间隔内的查询计划持续 DOP （并行度）。|  
|**min_dop**|**bigint**|聚合间隔内的查询计划的最小 DOP （并行度）。|  
|**max_dop**|**bigint**|聚合间隔内的查询计划的最大 DOP （并行度）。|  
|**stdev_dop**|**float**|聚合间隔内的查询计划的 DOP （并行度） 标准偏差。|  
|**avg_query_max_used_memory**|**float**|平均内存授予 （报告为的 8 KB 页数） 聚合间隔内的查询计划。 始终 0 表示查询使用本机编译内存优化过程。|  
|**last_query_max_used_memory**|**bigint**|最后一个内存授予 （报告为的 8 KB 页数） 聚合间隔内的查询计划。 始终 0 表示查询使用本机编译内存优化过程。|  
|**min_query_max_used_memory**|**bigint**|最小内存授予 （报告为的 8 KB 页数） 聚合间隔内的查询计划。 始终 0 表示查询使用本机编译内存优化过程。|  
|**max_query_max_used_memory**|**bigint**|最大内存授予 （报告为的 8 KB 页数） 聚合间隔内的查询计划。 始终 0 表示查询使用本机编译内存优化过程。|  
|**stdev_query_max_used_memory**|**float**|内存授予 （报告为的 8 KB 页数） 的标准偏差为聚合间隔内的查询计划。 始终 0 表示查询使用本机编译内存优化过程。|  
|**avg_rowcount**|**float**|返回行中的聚合间隔内的查询计划的平均数。|  
|**last_rowcount**|**bigint**|聚合间隔内的查询计划一次执行返回行数。|  
|**min_rowcount**|**bigint**|在聚合时间间隔内计划的查询返回的行的最小数。|  
|**max_rowcount**|**bigint**|在聚合时间间隔内计划的查询返回的行的最大数。|  
|**stdev_rowcount**|**float**|返回的行聚合间隔内的查询计划的标准偏差数。|
|**avg_log_bytes_used**|**float**|平均由查询计划，在聚合时间间隔内数据库日志中的字节数。 适用**仅到 Azure SQL Database**。|    
|**last_log_bytes_used**|**bigint**|使用上一次执行的查询计划，在聚合时间间隔内的数据库日志中的字节数。 适用**仅到 Azure SQL Database**。|  
|**min_log_bytes_used**|**bigint**|最小的查询计划，在聚合时间间隔内所使用的数据库日志中的字节数。  适用**仅到 Azure SQL Database**。|  
|**max_log_bytes_used**|**bigint**|最大的查询计划，在聚合时间间隔内所使用的数据库日志中的字节数。  适用**仅到 Azure SQL Database**。| 
|**stdev_log_bytes_used**|**float**|使用查询计划，在聚合时间间隔内的数据库日志中的字节数的标准偏差。  适用**仅到 Azure SQL Database**。|
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
