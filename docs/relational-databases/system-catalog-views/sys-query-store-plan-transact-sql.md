---
title: sys.query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc6eca7f1b28434c42579181c04d0fe9cb2f2922
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56231104"
---
# <a name="sysquerystoreplan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关与查询关联的每个执行计划信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|主键。|  
|**query_id**|**bigint**|外键。 加入[sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)。|  
|**plan_group_id**|**bigint**|计划组的 ID。 游标查询通常需要多个 （填充和提取） 计划。 编译在一起的提取计划都在同一个组，然后填充。<br /><br /> 0 表示计划不在组中。|  
|**engine_version**|**nvarchar(32)**|用于编译中的计划引擎版本**的 major.minor.build.revision**格式。|  
|**compatibility_level**|**smallint**|在查询中引用的数据库的数据库兼容性级别。|  
|**query_plan_hash**|**binary(8)**|MD5 哈希值的单个计划。|  
|**query_plan**|**nvarchar(max)**|查询计划的显示计划 XML。|  
|**is_online_index_plan**|**bit**|计划的联机索引生成期间使用。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**is_trivial_plan**|**bit**|计划是一个简单的计划 （在阶段 0 中的查询优化器的输出）。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**is_parallel_plan**|**bit**|并行计划。 <br/>**注意：** Azure SQL 数据仓库将始终返回一 (1)。|  
|**is_forced_plan**|**bit**|计划标记为当用户执行存储的过程时，强制**sys.sp_query_store_force_plan**。 强制机制*不能保证*完全此计划将用于引用查询**query_id**。 强制执行计划将导致重新编译查询，并通常生成完全相同或类似计划到引用的计划**plan_id**。 如果强制执行计划不成功， **force_failure_count**会递增并**last_force_failure_reason**填充含失败原因。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**is_natively_compiled**|**bit**|计划包括本机编译的内存优化的过程。 (0 = FALSE,1 = TRUE)。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**force_failure_count**|**bigint**|强制执行此计划已失败的次数。 仅当重新编译查询时，可以递增它 (*不在每次执行*)。 它将重置为 0 每次都**is_plan_forced**从更改**FALSE**到**TRUE**。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**last_force_failure_reason**|**int**|计划强制失败的原因。<br /><br /> 0： 无故障，否则为错误导致强制失败的错误数<br /><br /> 8637:ONLINE_INDEX_BUILD<br /><br /> 8683:INVALID_STARJOIN<br /><br /> 8684:TIME_OUT<br /><br /> 8689:NO_DB<br /><br /> 8690:HINT_CONFLICT<br /><br /> 8691:SETOPT_CONFLICT<br /><br /> 8694:DQ_NO_FORCING_SUPPORTED<br /><br /> 8698:NO_PLAN<br /><br /> 8712:NO_INDEX<br /><br /> 8713:VIEW_COMPILE_FAILED<br /><br /> \<其他值 >:GENERAL_FAILURE <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Last_force_failure_reason_desc 的文本说明。<br /><br /> ONLINE_INDEX_BUILD： 尝试修改数据，而目标表正在联机生成一个索引查询<br /><br /> INVALID_STARJOIN： 计划包含无效的 StarJoin 规范<br /><br /> TIME_OUT:搜索指定的强制计划的计划时允许的操作的优化器超出了数<br /><br /> NO_DB:在计划中指定的数据库不存在<br /><br /> HINT_CONFLICT:无法编译查询，因为计划冲突使用查询提示<br /><br /> DQ_NO_FORCING_SUPPORTED:无法执行查询，因为计划使用分布式的查询或全文操作的冲突。<br /><br /> NO_PLAN:查询处理器无法生成查询计划，因为无法验证强制的计划保持有效的查询<br /><br /> NO_INDEX:存在不再计划中指定的索引<br /><br /> VIEW_COMPILE_FAILED:无法强制实施查询计划，由于在计划中引用的索引视图中的问题<br /><br /> GENERAL_FAILURE： 常规强制错误 （不涉及与上述原因） <br/>**注意：** Azure SQL 数据仓库将始终返回*NONE*。|  
|**count_compiles**|**bigint**|计划编译统计信息。|  
|**initial_compile_start_time**|**datetimeoffset**|计划编译统计信息。|  
|**last_compile_start_time**|**datetimeoffset**|计划编译统计信息。|  
|**last_execution_time**|**datetimeoffset**|上次执行时间的最后一个引用查询计划的结束的时间。|  
|**avg_compile_duration**|**float**|计划编译统计信息。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**last_compile_duration**|**bigint**|计划编译统计信息。 <br/>**注意：** Azure SQL 数据仓库将始终返回零 (0)。|  
|**plan_forcing_type**|**int**|计划强制类型。<br /><br />0：无<br /><br />1：MANUAL<br /><br />2：AUTO|  
|**plan_forcing_type_desc**|**nvarchar(60)**|Plan_forcing_type 的文本说明。<br /><br />NONE:没有计划强制<br /><br />手动：由用户强制执行的计划<br /><br />自动：计划强制进行自动优化|  

## <a name="plan-forcing-limitations"></a>计划强制限制
查询存储中具有一种可用于强制查询优化器使用特定执行计划的机制。 但是，有些限制可能会阻止计划强制执行。 

首先，计划是否包含以下构造：
* INSERT BULK 语句。
* 对外部表的引用
* 分布式查询或全文操作
* 使用全局查询 
* 游标
* 无效的星型联接规范 

其次，计划依赖的对象何时不再可用：
* 数据库（计划来自的数据库不再存在时）
* 索引（不再存在或已禁用）

最后，计划本身的问题：
* 用于查询不合法
* 查询优化器超出了允许的操作数
* 格式不正确的计划 XML

## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
