---
title: "sys.dm_exec_trigger_stats (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回缓存触发器的聚合性能统计信息。 每个触发器在该视图中对应一行，行的生存期与触发器保持缓存状态的时间一样长。 在从缓存中删除触发器时，也将从该视图中删除对应行。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|触发器所在的数据库 ID。|  
|**object_id**|**int**|触发器的对象标识号。|  
|**type**|**char(2)**|对象的类型：<br /><br /> TA = 程序集 (CLR) 触发器<br /><br /> TR = SQL 触发器|  
|**Type_desc**|**nvarchar(60)**|对对象类型的说明：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql 句柄**|**varbinary(64)**|这可用来查询关联**sys.dm_exec_query_stats** ，中执行此触发器的。|  
|**plan_handle 收集**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可用于**sys.dm_exec_cached_plans**动态管理视图。|  
|**cached_time**|**datetime**|触发器添加到缓存的时间。|  
|**last_execution_time**|**datetime**|上次执行触发器的时间。|  
|**execution_count**|**bigint**|触发器自上次编译以来所执行的次数。|  
|**total_worker_time**|**bigint**|此触发器自编译以来执行所用的 CPU 时间总量（微秒）。|  
|**last_worker_time**|**bigint**|上次执行触发器所用的 CPU 时间（微秒）。|  
|**min_worker_time**|**bigint**|此触发器在单次执行期间曾占用的最大 CPU 时间（微秒）。|  
|**max_worker_time**|**bigint**|此触发器在单次执行期间曾占用的最大 CPU 时间（微秒）。|  
|**total_physical_reads**|**bigint**|此触发器自编译后在执行期间所执行的物理读取总次数。|  
|**last_physical_reads**|**bigint**|上次执行触发器时所执行的物理读取次数。|  
|**min_physical_reads**|**bigint**|该触发器在单次执行期间所执行的最少物理读取次数。|  
|**max_physical_reads**|**bigint**|该触发器在单次执行期间所执行的最大物理读取次数。|  
|**total_logical_writes**|**bigint**|此触发器自编译后在执行期间所执行的逻辑写入总次数。|  
|**last_logical_writes**|**bigint**|**total_physical_reads**的上次执行触发器时所执行的逻辑写入次数。|  
|**min_logical_writes**|**bigint**|该触发器在单次执行期间所执行的最少逻辑写入次数。|  
|**max_logical_writes**|**bigint**|该触发器在单次执行期间所执行的最大逻辑写入次数。|  
|**total_logical_reads**|**bigint**|此触发器自编译后在执行期间所执行的逻辑读取总次数。|  
|**last_logical_reads**|**bigint**|上次执行触发器时所执行的逻辑读取次数。|  
|**min_logical_reads**|**bigint**|该触发器在单次执行期间所执行的最少逻辑读取次数。|  
|**max_logical_reads**|**bigint**|该触发器在单次执行期间所执行的最大逻辑读取次数。|  
|**total_elapsed_time**|**bigint**|完成此触发器的执行所用的总时间（微秒）。|  
|**last_elapsed_time**|**bigint**|最近完成此触发器的执行所用的时间（微秒）。|  
|**min_elapsed_time**|**bigint**|任意一次完成此触发器的执行所用的最短时间（微秒）。|  
|**max_elapsed_time**|**bigint**|任意一次完成此触发器的执行所用的最长时间（微秒）。|  
  
## <a name="remarks"></a>注释  
 在 Windows Azure SQL Database 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  

查询完成后，将更新该视图中的统计信息。  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。
  
  
## <a name="examples"></a>示例  
 以下示例返回有关按平均占用时间衡量的前五个触发器的信息。  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行相关的动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [sys.dm_exec_procedure_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
