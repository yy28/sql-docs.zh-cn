---
title: sys.query_store_wait_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 18
author: AndrejsAnt
ms.author: AndrejsAnt
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d5a1744aa772664376ef91fc8dd82191d35f7272
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549977"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>sys.query_store_wait_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  包含有关查询的等待信息的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|表示 plan_id、 runtime_stats_interval_id、 execution_type 和 wait_category 的等待统计信息的行的标识符。 它是唯一的仅为过去的运行时统计信息时间间隔。 当前处于活动状态的时间间隔都可能有多个行表示引用的 plan_id，与表示 execution_type 和由 wait_category 等待此等待类别的执行类型的计划的等待统计信息。 通常情况下，一行表示等待统计信息将被刷新到磁盘，而其他 (s) 表示内存中状态。 因此，若要获取的每个时间间隔的实际状态需要聚合指标按 plan_id、 runtime_stats_interval_id、 execution_type 和 wait_category 分组。 |  
|**plan_id**|**bigint**|外键。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外键。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**wait_category**|**tinyint**|等待类型进行分类使用下表，然后等待时间汇总跨这些等待类别。 不同的等待类别需要不同的后续分析才能解决此问题，但相同类别的等待类型可引起非常相似的故障排除体验，并假定基于等待的受影响的查询会成为用于成功完成此类调查的大部分内容的缺少的部分。|
|**wait_category_desc**|**nvarchar(128)**|等待类别字段的文本说明，请查看下表。|
|**execution_type**|**tinyint**|确定类型的查询执行：<br /><br /> 0 – 常规执行 （成功完成）<br /><br /> 3 – 客户端启动已中止执行<br /><br /> 4-异常已中止执行|  
|**execution_type_desc**|**nvarchar(128)**|执行类型字段的文本说明：<br /><br /> 0 – 常规<br /><br /> 3 – 已中止<br /><br /> 4-异常|  
|**total_query_wait_time_ms**|**bigint**|总 CPU 的聚合时间间隔内的查询计划的等待时间，并等待类别 （以毫秒为单位报告）。|
|**avg_query_wait_time_ms**|**float**|平均等待每次执行 （以毫秒为单位报告） 在聚合时间间隔和等待类别中的查询计划的持续时间。|
|**last_query_wait_time_ms**|**bigint**|上次等待持续时间内聚合间隔的查询计划，然后等待类别 （以毫秒为单位报告）。|
|**min_query_wait_time_ms**|**bigint**|最小 CPU 聚合间隔内的查询计划的等待时间，并等待类别 （以毫秒为单位报告）。|
|**max_query_wait_time_ms**|**bigint**|最高 CPU 等待聚合间隔内的查询计划的时间，并等待类别 （以毫秒为单位报告）。|
|**stdev_query_wait_time_ms**|**float**|查询等待持续时间内聚合间隔的查询计划的标准偏差，并等待类别 （以毫秒为单位报告）。|

 ## <a name="wait-categories-mapping-table"></a>等待类别映射表  
  *"%"用作通配符*
  
|整数值|等待类别|在类别中包括等待类型|  
|-----------------|---------------|-----------------|  
|**0**|**Unknown**|Unknown |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**工作线程**|THREADPOOL|
|**3**|**锁**|LCK_M_%|
|**4**|**闩锁**|LATCH_ %|
|**5**|**缓冲区闩锁**|PAGELATCH_ %|
|**6**|**缓冲区 IO**|PAGEIOLATCH_%|
|**7**|**编译***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR %、 SQLCLR %|
|**9**|**镜像**|DBMIRROR %|
|**10**|**事务**|XACT %、 DTC %、 TRAN_MARKLATCH_ %、 MSQL_XACT_ %、 TRANSACTION_MUTEX|
|**11**|**空闲**|SLEEP_ %，LAZYWRITER_SLEEP、 SQLTRACE_BUFFER_FLUSH、 SQLTRACE_INCREMENTAL_FLUSH_SLEEP、 SQLTRACE_WAIT_ENTRIES、 FT_IFTS_SCHEDULER_IDLE_WAIT、 XE_DISPATCHER_WAIT、 REQUEST_FOR_DEADLOCK_SEARCH、 LOGMGR_QUEUE、 ONDEMAND_TASK_QUEUE、 CHECKPOINT_队列 XE_TIMER_EVENT|
|**12**|**抢先式**|PREEMPTIVE_ %|
|**13**|**Service Broker**|BROKER_ % **（但不是 BROKER_RECEIVE_WAITFOR）**|
|**14**|**事务日志 IO**|数据库、 LOGBUFFER、 LOGMGR_RESERVE_APPEND、 LOGMGR_FLUSH、 LOGMGR_PMM_LOG、 CHKPT、 WRITELOGF|
|**15**|**网络 IO**|ASYNC_NETWORK_IO，NET_WAITFOR_PACKET，PROXY_NETWORK_IO EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET EXCHANGE|
|**17**|**内存**|RESOURCE_SEMAPHORE、 CMEMTHREAD、 CMEMPARTITIONED、 EE_PMOLOCK、 MEMORY_ALLOCATION_EXT、 RESERVED_MEMORY_ALLOCATION_EXT、 MEMORY_GRANT_UPDATE|
|**18**|**用户等待**|WAITFOR 子句，WAIT_FOR_RESULTS，BROKER_RECEIVE_WAITFOR|
|**19**|**跟踪**|TRACEWRITE、 SQLTRACE_LOCK、 SQLTRACE_FILE_BUFFER、 SQLTRACE_FILE_WRITE_IO_COMPLETION、 SQLTRACE_FILE_READ_IO_COMPLETION、 SQLTRACE_PENDING_BUFFER_WRITERS、 SQLTRACE_SHUTDOWN、 QUERY_TRACEOUT、 TRACE_EVTNOTIFF|
|**20**|**全文搜索**|FT_RESTART_CRAWL、 全文收集器、 MSSEARCH、 FT_METADATA_MUTEX、 FT_IFTSHC_MUTEX、 FT_IFTSISM_MUTEX、 FT_IFTS_RWLOCK、 FT_COMPROWSET_RWLOCK、 FT_MASTER_MERGE、 FT_PROPERTYLIST_CACHE、 FT_MASTER_MERGE_COORDINATOR、 PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**21**|**其他磁盘 IO**|ASYNC_IO_COMPLETION、 IO_COMPLETION、 BACKUPIO、 WRITE_COMPLETION、 IO_QUEUE_LIMIT、 IO_RETRY|
|**22**|**复制**|SE_REPL_ %、 REPL_ %、 HADR_ % **（但不是 HADR_THROTTLE_LOG_RATE_GOVERNOR）**，PWAIT_HADR_ %，REPLICA_WRITES、 FCB_REPLICA_WRITE、 FCB_REPLICA_READ、 PWAIT_HADRSIM|
|**23**|**日志速率调控器**|LOG_RATE_GOVERNOR，POOL_LOG_RATE_GOVERNOR，HADR_THROTTLE_LOG_RATE_GOVERNOR INSTANCE_LOG_RATE_GOVERNOR|

***编译**目前不支持等待类别。 

  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
