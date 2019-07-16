---
title: sys.dm_exec_trigger_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c8ebe5ec97613b820ab6470f36f3f5351c7da649
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936826"
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回缓存触发器的聚合性能统计信息。 每个触发器在该视图中对应一行，行的生存期与触发器保持缓存状态的时间一样长。 在从缓存中删除触发器时，也将从该视图中删除对应行。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|触发器所在的数据库 ID。|  
|**object_id**|**int**|触发器的对象标识号。|  
|**type**|**char(2)**|对象的类型：<br /><br /> TA = 程序集 (CLR) 触发器<br /><br /> TR = SQL 触发器|  
|**Type_desc**|**nvarchar(60)**|对对象类型的说明：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|这可用于将与中的查询相关联**sys.dm_exec_query_stats**从此触发器中执行的。|  
|**plan_handle**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可能与使用**sys.dm_exec_cached_plans**动态管理视图。|  
|**cached_time**|**datetime**|触发器添加到缓存的时间。|  
|**last_execution_time**|**datetime**|上次执行触发器的时间。|  
|**execution_count**|**bigint**|上次编译以来执行触发器的次数。|  
|**total_worker_time**|**bigint**|CPU 时间，以微秒为单位，自编译后，此触发器的执行所用的总金额。|  
|**last_worker_time**|**bigint**|上次执行触发器所用的 CPU 时间（微秒）。|  
|**min_worker_time**|**bigint**|最大 CPU 时间，以微秒为单位，此触发器在单次执行期间曾占用。|  
|**max_worker_time**|**bigint**|最大 CPU 时间，以微秒为单位，此触发器在单次执行期间曾占用。|  
|**total_physical_reads**|**bigint**|自编译后，此触发器的执行期间所执行的物理读取总次数。|  
|**last_physical_reads**|**bigint**|上次执行触发器时执行的物理读取操作数。|  
|**min_physical_reads**|**bigint**|此触发器在单次执行期间所执行的物理读取次数最小数目。|  
|**max_physical_reads**|**bigint**|此触发器在单次执行期间所执行的物理读取次数最大数目。|  
|**total_logical_writes**|**bigint**|自编译后，此触发器的执行期间所执行的逻辑写入总次数。|  
|**last_logical_writes**|**bigint**|上次执行触发器时所执行逻辑写入次数。|  
|**min_logical_writes**|**bigint**|此触发器在单次执行期间所执行的逻辑写入次数最小数目。|  
|**max_logical_writes**|**bigint**|此触发器在单次执行期间所执行的逻辑写入次数最大数目。|  
|**total_logical_reads**|**bigint**|自编译后，此触发器的执行期间所执行的逻辑读取总次数。|  
|**last_logical_reads**|**bigint**|上次执行触发器时执行的逻辑读取操作数。|  
|**min_logical_reads**|**bigint**|此触发器在单次执行期间所执行的逻辑读取次数最小数目。|  
|**max_logical_reads**|**bigint**|此触发器在单次执行期间所执行的逻辑读取次数最大数目。|  
|**total_elapsed_time**|**bigint**|总运行时间，以微秒为单位，完成此触发器的执行。|  
|**last_elapsed_time**|**bigint**|最近完成此触发器的执行所用的时间（微秒）。|  
|**min_elapsed_time**|**bigint**|最短已用时间，以微秒为单位，此触发器的任何已完成执行。|  
|**max_elapsed_time**|**bigint**|最大运行时间，以微秒为单位，此触发器的任何已完成执行。| 
|**total_spills**|**bigint**|执行此触发器自编译后溢出总页数。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|页数溢出的上次执行触发器。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|此触发器在单次执行期间曾扩散的页面中最小的数。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|此触发器在单次执行期间曾扩散最大页数。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**total_page_server_reads**|**bigint**|自编译后，此触发器的执行期间所执行的页服务器读取的总数。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**last_page_server_reads**|**bigint**|上次执行触发器时执行的页服务器读取操作数。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**min_page_server_reads**|**bigint**|页服务器的最小数目读取此触发器在单次执行期间已过执行。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**max_page_server_reads**|**bigint**|页服务器的最大数目读取此触发器在单次执行期间已过执行。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  

  
## <a name="remarks"></a>备注  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 若要避免公开此类信息，包含不属于已连接租户的数据的每一行都筛选掉。  

查询完成后，将更新该视图中的统计信息。  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 上，需要在数据库中拥有 `VIEW DATABASE STATE` 权限。   
  
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
  
## <a name="see-also"></a>请参阅  
[与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
