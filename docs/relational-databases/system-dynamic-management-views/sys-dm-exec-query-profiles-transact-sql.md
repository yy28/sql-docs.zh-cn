---
title: sys.dm_exec_query_profiles (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2598c37c60955a93f2aed426db705d2b2ca7f204
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  正执行查询时监视实时查询进度。 例如，使用此 DMV 确定运行缓慢的查询部分。 可使用说明字段中标识的列，将此 DMV 与其他系统 DMV 相联接。 或者，使用时间戳列，将此 DMV 与其他性能计数器（如性能计数器 xperf）相联接。  
  
## <a name="table-returned"></a>返回的表  
 返回的计数器基于每个运算符和每个线程。 结果是动态的，并且与仅在完成查询时创建输出的现有选项（如，SET STATISTICS XML ON）的结果不匹配。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|标识运行此查询的会话。 引用 dm_exec_sessions.session_id。|  
|request_id|**int**|确定目标请求。 引用 dm_exec_sessions.request_id。|  
|sql_handle|**varbinary(64)**|确定目标查询。 引用 dm_exec_query_stats.sql_handle。|  
|plan_handle|**varbinary(64)**|确定目标查询（引用 dm_exec_query_stats.plan_handle）。|  
|physical_operator_name|**nvarchar(256)**|物理运算符名称。|  
|node_id|**int**|标识查询树中的运算符节点。|  
|thread_id|**int**|区分属于同一个查询运算符节点的线程（针对并行查询）。|  
|task_address|**varbinary(8)**|确定此线程正在使用的 SQLOS 任务。 引用 dm_os_tasks.task_address。|  
|row_count|**bigint**|运算符迄今返回的行数。|  
|rewind_count|**bigint**|迄今为止的重绕数。|  
|rebind_count|**bigint**|迄今为止的重新绑定数。|  
|end_of_scan_count|**bigint**|迄今为止的扫描结束次数。|  
|estimate_row_count|**bigint**|估计的行数。 可用于将 estimated_row_count 与实际 row_count 进行比较。|  
|first_active_time|**bigint**|首次调用运算符的时间（毫秒）。|  
|last_active_time|**bigint**|上次调用运算符的时间（毫秒）。|  
|open_time|**bigint**|打开时的时间戳（毫秒）。|  
|first_row_time|**bigint**|打开第一行时的时间戳（毫秒）。|  
|last_row_time|**bigint**|打开最后一行时的时间戳（毫秒）。|  
|close_time|**bigint**|关闭时的时间戳（毫秒）。|  
|elapsed_time_ms|**bigint**|目标节点的操作迄今为止使用的总占用时间（毫秒）。|  
|cpu_time_ms|**bigint**|目标节点的操作迄今为止使用的总 CPU 时间（毫秒）。|  
|database_id|**int**|包含要对其进行读写的对象的数据库的 ID。|  
|object_id|**int**|要对其进行读写的对象的标识符。 引用 sys.objects.object_id。|  
|index_id|**int**|打开其行级的索引（如果有）。|  
|scan_count|**bigint**|迄今为止的表/索引扫描数。|  
|logical_read_count|**bigint**|迄今为止的逻辑读取数。|  
|physical_read_count|**bigint**|迄今为止的物理读取数。|  
|read_ahead_count|**bigint**|迄今为止的预读数。|  
|write_page_count|**bigint**|迄今为止由于溢出而导致的页写入数。|  
|lob_logical_read_count|**bigint**|迄今为止的 LOB 逻辑读取数。|  
|lob_physical_read_count|**bigint**|迄今为止的 LOB 物理读取数。|  
|lob_read_ahead_count|**bigint**|迄今为止的 LOB 预读数。|  
|segment_read_count|**int**|迄今为止的段预读数。|  
|segment_skip_count|**int**|迄今为止跳过的段数。| 
|actual_read_row_count|**bigint**|应用残留谓词之前读取运算符的行数。| 
|estimated_read_row_count|**bigint**|**适用于：**开头[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]SP1。 <br/>估计残留谓词应用之前，操作员要读取的行数。|  
  
## <a name="general-remarks"></a>一般备注  
 如果查询计划节点没有任何 IO，则所有与 IO 相关的计数器均设置为 NULL。  
  
 此 DMV 报告的与 IO 相关的计数器比 SET STATISTICS IO 报告的计数器更精细，这体现在以下两方面：  
  
-   SET STATISTICS IO 将所有 IO 的计数器组合到给定的表中。 通过此 DMV，你将获得对表执行 IO 的查询计划中每个节点的单独的计数器。  
  
-   如果存在并行扫描，则此 DMV 将报告处理扫描的每个并行线程的计数器。
 
 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，分析基础结构的标准查询执行统计信息存在并排显示具有分析基础结构轻量的查询执行统计信息。 新查询执行统计信息分析基础结构极大地减少了收集每个运算符查询执行统计信息，如的实际行数的性能开销。 可以使用全局启用此功能启动[跟踪标志 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，或使用 query_thread_profile 扩展的事件时自动打开。

>[!NOTE]
> 下的轻量的查询执行统计信息分析基础结构以减少对性能的影响不支持 CPU 和经过的时间。

 设置统计信息 XML ON 和 SET STATISTICS PROFILE ON 始终使用分析基础结构的旧的查询执行统计信息。
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
   
## <a name="examples"></a>示例  
 步骤 1： 登录到你打算使用 sys.dm_exec_query_profiles 运行将分析所查询的会话。 若要配置分析的查询时，可使用 SET STATISTICS PROFILE 上。 在同一会话中运行你的查询。  
  
```  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 步骤 2： 登录到不同于在其中运行你的查询的会话的第二个会话。  
  
 以下语句总结当前在会话 54 中运行的查询的进度。 为此，它基于每个节点的所有线程计算输出行的总数，然后将其与该节点的输出行的估算数目进行比较。  
  
```  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

