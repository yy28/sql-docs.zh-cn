---
title: sys.query_store_runtime_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ba19045d0184e498b559da0b97b3cd4d95d30c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067935"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关查询的运行时执行统计信息的信息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|表示运行时执行统计信息的行的标识符**plan_id**， **execution_type**并**runtime_stats_interval_id**。 它是唯一的仅为过去的运行时统计信息时间间隔。 当前处于活动状态的间隔内可能有多个行表示引用的计划的运行时统计信息**plan_id**，与表示的执行类型**execution_type**。 通常情况下，一行表示运行时统计信息将被刷新到磁盘，而其他 (s) 表示内存中状态。 因此，若要获取的每个时间间隔的实际状态需要聚合指标，通过对分组**plan_id**， **execution_type**并**runtime_stats_interval_id**。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**plan_id**|**bigint**|外键。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外键。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**execution_type**|**tinyint**|确定类型的查询执行：<br /><br /> 0-常规执行 （成功完成）<br /><br /> 3-客户端启动已中止执行<br /><br /> 4-异常已中止执行|  
|**execution_type_desc**|**nvarchar(128)**|执行类型字段的文本说明：<br /><br /> 0-常规<br /><br /> 3-已中止<br /><br /> 4-异常|  
|**first_execution_time**|**datetimeoffset**|第一个聚合间隔内的查询计划的执行时间。 这是指执行查询的结束时间。|  
|**last_execution_time**|**datetimeoffset**|上次执行时间的查询计划的聚合间隔内。 这是指执行查询的结束时间。|  
|**count_executions**|**bigint**|聚合间隔内的查询计划执行数的总计数。|  
|**avg_duration**|**float**|平均持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**last_duration**|**bigint**|查询的最后一个持续时间 （以微秒为单位报告） 在聚合时间间隔内计划。|  
|**min_duration**|**bigint**|最小持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**max_duration**|**bigint**|最大持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。|  
|**stdev_duration**|**float**|持续时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。|  
|**avg_cpu_time**|**float**|CPU 的平均时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_cpu_time**|**bigint**|最后一个查询的 CPU 时间 （以微秒为单位报告） 在聚合时间间隔内计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_cpu_time**|**bigint**|聚合间隔 （以微秒为单位报告） 内的查询计划的最小 CPU 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_cpu_time**|**bigint**|聚合间隔 （以微秒为单位报告） 内的查询计划的最大 CPU 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_cpu_time**|**float**|CPU 时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_logical_io_reads**|**float**|平均逻辑 IO 读取次数聚合间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_logical_io_reads**|**bigint**|最后一个的逻辑 IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_logical_io_reads**|**bigint**|最小的逻辑 IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_logical_io_reads**|**bigint**|最大的逻辑 IO 读取数的聚合时间间隔内的查询计划。（表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_logical_io_reads**|**float**|逻辑 IO 读取数的聚合时间间隔内的查询计划的标准偏差。 （表示为 8 KB 页读取数）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_logical_io_writes**|**float**|聚合间隔内的查询计划将写入平均逻辑 IO 数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_logical_io_writes**|**bigint**|上次逻辑 IO 数写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_logical_io_writes**|**bigint**|最小数目的逻辑 IO 写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_logical_io_writes**|**bigint**|最大数量的逻辑 IO 写入聚合间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_logical_io_writes**|**float**|聚合间隔内的查询计划的标准偏差写入次数逻辑 IO。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_physical_io_reads**|**float**|平均物理 IO 读取次数聚合间隔 （以 8 KB 页读取数表示） 内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_physical_io_reads**|**bigint**|最后一个的物理 IO 读取数的聚合间隔 （以 8 KB 页读取数表示） 内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_physical_io_reads**|**bigint**|最小的物理 IO 读取数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_physical_io_reads**|**bigint**|最大物理 IO 读取次数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_physical_io_reads**|**float**|物理 IO 读取次数 （以 8 KB 页读取数表示） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_clr_time**|**float**|CLR 的平均时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_clr_time**|**bigint**|查询的最后一个 CLR 时间 （以微秒为单位报告） 在聚合时间间隔内计划。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_clr_time**|**bigint**|聚合间隔 （以微秒为单位报告） 内的查询计划的最短 CLR 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_clr_time**|**bigint**|聚合间隔 （以微秒为单位报告） 内的查询计划的最大 CLR 时间。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_clr_time**|**float**|CLR 时间 （以微秒为单位报告） 的聚合时间间隔内的查询计划的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_dop**|**float**|聚合间隔内的查询计划的平均 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_dop**|**bigint**|聚合间隔内的查询计划将持续 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_dop**|**bigint**|聚合间隔内的查询计划的最小 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_dop**|**bigint**|聚合间隔内的查询计划的最大 DOP （并行度）。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_dop**|**float**|聚合间隔内的查询计划的 DOP （并行度） 标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_query_max_used_memory**|**float**|平均内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_query_max_used_memory**|**bigint**|最后一个内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_query_max_used_memory**|**bigint**|最小内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_query_max_used_memory**|**bigint**|最大内存授予 （报告为 8 KB 页数） 内的聚合时间间隔的查询计划。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_query_max_used_memory**|**float**|内存授予的聚合时间间隔内的查询计划的标准偏差 （报告为 8 KB 页数）。 始终 0 的查询使用本机编译内存优化过程。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**avg_rowcount**|**float**|返回行中的查询计划的聚合时间间隔内的平均数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_rowcount**|**bigint**|返回由上一次执行的聚合时间间隔内的查询计划的行数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_rowcount**|**bigint**|聚合间隔内计划的查询返回的行的最小数目。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_rowcount**|**bigint**|聚合间隔内计划的查询返回的行的最大数目。|  
|**stdev_rowcount**|**float**|返回的行聚合间隔内的查询计划的标准偏差的数量。|
|**avg_log_bytes_used**|**float**|查询计划，聚合间隔内所使用的数据库日志中的字节的平均数量。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**last_log_bytes_used**|**bigint**|使用上一次执行的查询计划，聚合间隔内的数据库日志中的字节数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**min_log_bytes_used**|**bigint**|最小查询计划，聚合间隔内所使用的数据库日志的字节数。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**max_log_bytes_used**|**bigint**|查询计划，聚合间隔内所使用的数据库日志中的字节的最大数目。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|
|**stdev_log_bytes_used**|**float**|查询计划，聚合间隔内所使用的数据库日志中的字节数的标准偏差。<br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**avg_page_server_io_reads**|**float**|平均页 server IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br><br/>**注意：** 适用于：Azure SQL 数据库的超大规模</br> Azure SQL 数据仓库，Azure SQL DB MI （非超大规模） 将始终返回零 (0)。|
|**last_page_server_io_reads**|**bigint**|最后一页 server IO 读取次数聚合间隔内的查询计划。 （表示为 8 KB 页读取数）。<br><br/>**注意：** 适用于：Azure SQL 数据库的超大规模 </br> Azure SQL 数据仓库，Azure SQL DB MI （非超大规模） 将始终返回零 (0)。|
|**min_page_server_io_reads**|**bigint**|最小的页 server IO 读取数的聚合时间间隔内的查询计划。 （表示为 8 KB 页读取数）。<br><br/>**注意：** 适用于：Azure SQL 数据库的超大规模 </br> Azure SQL 数据仓库，Azure SQL DB MI （非超大规模） 将始终返回零 (0)。|
|**max_page_server_io_reads**|**bigint**|最大页 server IO 读取数聚合间隔内的查询计划。（表示为 8 KB 页读取数）。<br><br/>**注意：** 适用于：Azure SQL 数据库的超大规模 </br> Azure SQL 数据仓库，Azure SQL DB MI （非超大规模） 将始终返回零 (0)。|
|**stdev_page_server_io_reads**|**float**|页 server IO 读取数的聚合时间间隔内的查询计划的标准偏差。 （表示为 8 KB 页读取数）。<br><br/>**注意：** 适用于：Azure SQL 数据库的超大规模 </br> Azure SQL 数据仓库，Azure SQL DB MI （非超大规模） 将始终返回零 (0)。|
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
