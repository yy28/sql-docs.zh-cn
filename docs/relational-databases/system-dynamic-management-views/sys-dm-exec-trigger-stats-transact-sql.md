---
title: sys.dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/10/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63430240cfd518ce38567d10fbebbf258a37d872
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回缓存触发器的聚合性能统计信息。 每个触发器在该视图中对应一行，行的生存期与触发器保持缓存状态的时间一样长。 在从缓存中删除触发器时，也将从该视图中删除对应行。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|触发器所在的数据库 ID。|  
|**object_id**|**int**|触发器的对象标识号。|  
|**类型**|**char(2)**|对象的类型：<br /><br /> TA = 程序集 (CLR) 触发器<br /><br /> TR = SQL 触发器|  
|**Type_desc**|**nvarchar(60)**|对对象类型的说明：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|这可用来查询关联**sys.dm_exec_query_stats** ，中执行此触发器的。|  
|**plan_handle**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可用于**sys.dm_exec_cached_plans**动态管理视图。|  
|**cached_time**|**datetime**|触发器添加到缓存的时间。|  
|**last_execution_time**|**datetime**|上次执行触发器的时间。|  
|**execution_count**|**bigint**|上次编译以来所执行触发器的次数。|  
|**total_worker_time**|**bigint**|CPU 时间 （毫秒），自编译后，此触发器的执行所用的总量。|  
|**last_worker_time**|**bigint**|上次执行触发器所用的 CPU 时间（微秒）。|  
|**min_worker_time**|**bigint**|最大 CPU 时间，单位为微秒，在单个执行期间所用此触发器。|  
|**max_worker_time**|**bigint**|最大 CPU 时间，单位为微秒，在单个执行期间所用此触发器。|  
|**total_physical_reads**|**bigint**|执行期间所执行的此触发器自编译后的物理读取总次数。|  
|**last_physical_reads**|**bigint**|上次执行触发器时所执行的物理读取数。|  
|**min_physical_reads**|**bigint**|最小此触发器在单次执行期间所执行的物理读取数。|  
|**max_physical_reads**|**bigint**|最大此触发器在单次执行期间所执行的物理读取数。|  
|**total_logical_writes**|**bigint**|执行期间所执行的此触发器自编译后的逻辑写入总次数。|  
|**last_logical_writes**|**bigint**|上次执行触发器时所执行的逻辑写入次数。|  
|**min_logical_writes**|**bigint**|最小此触发器在单次执行期间所执行的逻辑写入数。|  
|**max_logical_writes**|**bigint**|最大此触发器在单次执行期间所执行的逻辑写入数。|  
|**total_logical_reads**|**bigint**|执行期间所执行的此触发器自编译后的逻辑读取总次数。|  
|**last_logical_reads**|**bigint**|上次执行触发器时所执行的逻辑读取数。|  
|**min_logical_reads**|**bigint**|最小此触发器在单次执行期间所执行的逻辑读取数。|  
|**max_logical_reads**|**bigint**|最大此触发器在单次执行期间所执行的逻辑读取数。|  
|**total_elapsed_time**|**bigint**|总运行时间，单位为微秒，完成此触发器的执行。|  
|**last_elapsed_time**|**bigint**|最近完成此触发器的执行所用的时间（微秒）。|  
|**min_elapsed_time**|**bigint**|最小的运行时间，单位为微秒，任何已完成此触发器的执行。|  
|**max_elapsed_time**|**bigint**|最大运行时间，单位为微秒，任何已完成此触发器的执行。| 
|**total_spills**|**bigint**|溢出通过执行此触发器自编译后的页的总数。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|总页数溢出的上次执行触发器时。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|此触发器在单次执行期间曾溢出的页中最小的数。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|最大页数此触发器在单次执行期间曾溢出。<br /><br /> **适用于**： 开头[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
  
## <a name="remarks"></a>注释  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  

查询完成后，将更新该视图中的统计信息。  
  
## <a name="permissions"></a>权限  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。
  
  
## <a name="examples"></a>示例  
 以下示例返回有关按平均占用时间衡量的前五个触发器的信息。  
  
```sql  
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
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
