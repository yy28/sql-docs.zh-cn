---
title: sys.query_store_runtime_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3392bcde00439981a401c908ca7a1898d9d026f5
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242305"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关查询的运行时执行统计信息的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**BIGINT**|表示运行时执行统计信息的行的标识符**plan_id**， **execution_type**并**runtime_stats_interval_id**。 它是唯一的仅为过去的运行时统计信息时间间隔。 当前处于活动状态的间隔内可能有多个行表示引用的计划的运行时统计信息**plan_id**，与表示的执行类型**execution_type**。 通常情况下，一行表示运行时统计信息将被刷新到磁盘，而其他 (s) 表示内存中状态。 因此，若要获取的每个时间间隔的实际状态需要聚合指标，通过对分组**plan_id**， **execution_type**并**runtime_stats_interval_id**。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**plan_id**|**BIGINT**|外键。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**BIGINT**|外键。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**execution_type**|**TINYINT**|确定类型的查询执行：<br /><br /> 0-常规执行 （成功完成）<br /><br /> 3-客户端启动已中止执行<br /><br /> 4-异常已中止执行|  
|**execution_type_desc**|**nvarchar(128)**|执行类型字段的文本说明：<br /><br /> 0-常规<br /><br /> 3-已中止<br /><br /> 4-异常|  
|**first_execution_time**|**datetimeoffset**|第一个聚合间隔内的查询计划的执行时间。|  
|**last_execution_time**|**datetimeoffset**|上次执行时间的查询计划的聚合间隔内。|  
|**count_executions**|**BIGINT**|聚合间隔内的查询计划执行数的总计数。|  
|**avg_duration**|**FLOAT**|平均持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**last_duration**|**BIGINT**|查询的最后一个持续时间 （以微秒为单位报告） 在聚合时间间隔内计划。|  
|**min_duration**|**BIGINT**|最小持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**max_duration**|**BIGINT**|最大持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**stdev_duration**|**FLOAT**|持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。|  
|**avg_cpu_time**|**FLOAT**|CPU 的平均时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_cpu_time**|**BIGINT**|最后一个查询的 CPU 时间 （以微秒为单位报告） 在聚合时间间隔内计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_cpu_time**|**BIGINT**|聚合间隔 （以微秒为单位报告） 内的查询计划的最小 CPU 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_cpu_time**|**BIGINT**|聚合间隔 （以微秒为单位报告） 内的查询计划的最大 CPU 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_cpu_time**|**FLOAT**|CPU 时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_logical_io_reads**|**FLOAT**|平均逻辑 IO 读取次数聚合间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_logical_io_reads**|**BIGINT**|最后一个的逻辑 IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_logical_io_reads**|**BIGINT**|最小的逻辑 IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_logical_io_reads**|**BIGINT**|最大的逻辑 IO 读取数的聚合时间间隔内的查询计划。（表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_logical_io_reads**|**FLOAT**|逻辑 IO 读取数的聚合时间间隔内的查询计划的标准偏差。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_logical_io_writes**|**FLOAT**|聚合间隔内的查询计划将写入平均逻辑 IO 数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_logical_io_writes**|**BIGINT**|上次逻辑 IO 数写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_logical_io_writes**|**BIGINT**|最小数目的逻辑 IO 写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_logical_io_writes**|**BIGINT**|最大数量的逻辑 IO 写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_logical_io_writes**|**FLOAT**|聚合间隔内的查询计划的标准偏差写入次数逻辑 IO。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_physical_io_reads**|**FLOAT**|平均物理 IO 读取次数聚合间隔 （以 8 KB 页读取数表示） 内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_physical_io_reads**|**BIGINT**|最后一个的物理 IO 读取数的聚合间隔 （以 8 KB 页读取数表示） 内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_physical_io_reads**|**BIGINT**|最小的物理 IO 读取数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_physical_io_reads**|**BIGINT**|最大物理 IO 读取次数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_physical_io_reads**|**FLOAT**|物理 IO 读取次数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_clr_time**|**FLOAT**|CLR 的平均时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_clr_time**|**BIGINT**|查询的最后一个 CLR 时间 （以微秒为单位报告） 在聚合时间间隔内计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_clr_time**|**BIGINT**|聚合间隔 （以微秒为单位报告） 内的查询计划的最短 CLR 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_clr_time**|**BIGINT**|聚合间隔 （以微秒为单位报告） 内的查询计划的最大 CLR 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_clr_time**|**FLOAT**|CLR 时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_dop**|**FLOAT**|聚合间隔内的查询计划的平均 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_dop**|**BIGINT**|聚合间隔内的查询计划将持续 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_dop**|**BIGINT**|聚合间隔内的查询计划的最小 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_dop**|**BIGINT**|聚合间隔内的查询计划的最大 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_dop**|**FLOAT**|聚合间隔内的查询计划的 DOP （并行度） 标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_query_max_used_memory**|**FLOAT**|平均内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_query_max_used_memory**|**BIGINT**|最后一个内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_query_max_used_memory**|**BIGINT**|最小内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_query_max_used_memory**|**BIGINT**|最大内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_query_max_used_memory**|**FLOAT**|内存授予的聚合时间间隔内的查询计划的标准偏差 （报告为 8 KB 页数）。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_rowcount**|**FLOAT**|返回行中的查询计划的聚合时间间隔内的平均数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_rowcount**|**BIGINT**|返回由上一次执行的聚合时间间隔内的查询计划的行数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_rowcount**|**BIGINT**|聚合间隔内计划的查询返回的行的最小数目。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_rowcount**|**BIGINT**|聚合间隔内计划的查询返回的行的最大数目。|  
|**stdev_rowcount**|**FLOAT**|返回的行聚合间隔内的查询计划的标准偏差的数量。|
|**avg_log_bytes_used**|**FLOAT**|查询计划，聚合间隔内所使用的数据库日志中的字节的平均数量。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_log_bytes_used**|**BIGINT**|使用上一次执行的查询计划，聚合间隔内的数据库日志中的字节数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_log_bytes_used**|**BIGINT**|最小查询计划，聚合间隔内所使用的数据库日志的字节数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_log_bytes_used**|**BIGINT**|查询计划，聚合间隔内所使用的数据库日志中的字节的最大数目。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_log_bytes_used**|**FLOAT**|查询计划，聚合间隔内所使用的数据库日志中的字节数的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_query_store_options (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
