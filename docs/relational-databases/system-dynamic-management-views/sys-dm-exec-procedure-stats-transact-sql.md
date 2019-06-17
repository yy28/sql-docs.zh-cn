---
title: sys.dm_exec_procedure_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c7f4622eec6b7c5d3a3cc206b43cd31253fe7ee2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462662"
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回缓存存储过程的聚合性能统计信息。 该视图为每个缓存的存储过程计划都返回一行，行的生存期与存储过程保持缓存状态的时间一样长。 在从缓存中删除存储过程时，也将从该视图中删除对应行。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 若要避免公开此类信息，包含不属于已连接租户的数据的每一行都筛选掉。  
  
> [!NOTE]
> 初始查询**sys.dm_exec_procedure_stats**可能会产生不准确的结果，如果没有在服务器上当前正在执行的工作负荷。 可以通过重新运行查询来确定更准确的结果。  
  
> [!NOTE]
> 若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_procedure_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|存储过程所在的数据库 ID。|  
|**object_id**|**int**|存储过程的对象标识号。|  
|**type**|**char(2)**|对象的类型：<br /><br /> P = SQL 存储过程<br /><br /> PC = 程序集 (CLR) 存储过程<br /><br /> X = 扩展存储过程|  
|**type_desc**|**nvarchar(60)**|对对象类型的说明：<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|这可用于将与中的查询相关联**sys.dm_exec_query_stats**从此存储过程中执行的。|  
|**plan_handle**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可能与使用**sys.dm_exec_cached_plans**动态管理视图。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0x000。|  
|**cached_time**|**datetime**|存储过程添加到缓存的时间。|  
|**last_execution_time**|**datetime**|上次执行存储过程的时间。|  
|**execution_count**|**bigint**|上次编译以来执行存储的过程的次数。|  
|**total_worker_time**|**bigint**|CPU 时间，以微秒为单位，自编译后，此存储过程的执行所用的总金额。<br /><br /> 对于本机编译的存储过程，如果许多执行所用的时间都不到 1 毫秒，则 **total_worker_time** 可能不精确。|  
|**last_worker_time**|**bigint**|上次执行存储过程所用的 CPU 时间（微秒）。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|最小 CPU 时间，以微秒为单位，此存储过程具有执行期间曾占用单个。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|最大 CPU 时间，以微秒为单位，此存储过程具有执行期间曾占用单个。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|自编译后，此存储过程的执行期间所执行的物理读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_physical_reads**|**bigint**|上次执行存储的过程时所执行物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_physical_reads**|**bigint**|最小的物理读取次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_physical_reads**|**bigint**|最大的物理读取次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_writes**|**bigint**|自编译后，此存储过程的执行期间所执行的逻辑写入总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_writes**|**bigint**|缓冲池页数变脏的上次执行计划。 如果页已变脏（已修改），则不计入写次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_writes**|**bigint**|最小的逻辑写入次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_writes**|**bigint**|最大的逻辑写入次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_reads**|**bigint**|自编译后，此存储过程的执行期间所执行的逻辑读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_reads**|**bigint**|上次执行存储的过程时执行的逻辑读取操作数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_reads**|**bigint**|最小的逻辑读取次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_reads**|**bigint**|最大的逻辑读取次数，此存储过程在单次执行期间所执行。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_elapsed_time**|**bigint**|总运行时间，以微秒为单位，完成此存储过程的执行。|  
|**last_elapsed_time**|**bigint**|经过的时间，以微秒为单位，最近完成的执行存储过程。|  
|**min_elapsed_time**|**bigint**|最小运行时间，以微秒为单位，任何已完成执行此存储过程。|  
|**max_elapsed_time**|**bigint**|最大运行时间，以微秒为单位，任何已完成执行此存储过程。|  
|**total_spills**|**bigint**|执行此存储过程自编译后溢出总页数。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|页面数超出了上次执行存储的过程时，溢出。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|在单次执行期间曾扩散此存储过程的页面的最小数目。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|在单次执行期间曾扩散此存储过程的页面的最大数目。<br /><br /> **适用对象**：从开始[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**pdw_node_id**|**int**|对于此分布的节点标识符。<br /><br />**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
|**total_page_server_reads**|**bigint**|自编译后，此存储过程的执行期间所执行的页服务器读取的总数。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**last_page_server_reads**|**bigint**|上次执行存储的过程时执行的页服务器读取操作数。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**min_page_server_reads**|**bigint**|页服务器的最小数目读取此存储的过程在单次执行期间已过执行。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
|**max_page_server_reads**|**bigint**|页服务器的最大数目读取此存储的过程在单次执行期间已过执行。<br /><br /> **适用对象**：Azure SQL 数据库的超大规模|  
  
 <sup>1</sup>对于本机编译存储过程启用统计信息收集后，辅助角色收集时间以毫秒为单位。 如果查询执行不到 1 毫秒，则该值将为 0。  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
   
## <a name="remarks"></a>备注  
 存储过程执行完成后，将更新该视图中的统计信息。  
  
## <a name="examples"></a>示例  
 以下示例返回有关按平均占用时间衡量的前十个存储过程的信息。  
  
```sql  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>请参阅  
[与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)    
[sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)    
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  
  


