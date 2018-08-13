---
title: sys.dm_exec_function_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 51f94535dcc29e1da3156d661ff9e1f6bdc2cf2a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537077"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.dm_exec_function_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  返回聚合缓存的函数的性能统计信息。 视图将返回为每个缓存的函数计划，一个行和行的生存期只要函数保持缓存。 从缓存删除函数后，相应的行也将从此视图。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。 返回有关标量函数，包括内存中的函数以及 CLR 标量函数的信息。 不返回有关表值函数的信息。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  
  
> [!NOTE]
> 初始查询**sys.dm_exec_function_stats**可能会产生不准确的结果，如果没有在服务器上当前正在执行的工作负荷。 可以通过重新运行查询来确定更准确的结果。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|该函数所在的数据库 ID。|  
|**object_id**|**int**|函数的对象标识号。|  
|**类型**|**char(2)**|对象的类型： FN = 标量值的函数|  
|**type_desc**|**nvarchar(60)**|对象类型的说明： SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|这可用于将与中的查询相关联**sys.dm_exec_query_stats**中此函数执行的。|  
|**plan_handle**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可能与使用**sys.dm_exec_cached_plans**动态管理视图。<br /><br /> 将始终为 0x000 时本机编译的函数查询内存优化表。|  
|**cached_time**|**datetime**|向缓存添加函数的时间。|  
|**last_execution_time**|**datetime**|该函数执行的最后一个时间。|  
|**execution_count**|**bigint**|上次编译以来执行该函数的次数。|  
|**total_worker_time**|**bigint**|中的微秒为单位，自编译后，此函数的执行所用总 CPU 时间量。<br /><br /> 对于本机编译的函数， **total_worker_time**可能不准确，如果许多执行所需不到 1 毫秒。|  
|**last_worker_time**|**bigint**|CPU 时间，以微秒为单位，已使用上次执行该函数的时间量。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|最小 CPU 时间，以微秒为单位，在单次执行期间曾占用此函数。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|最大 CPU 时间，以微秒为单位，在单次执行期间曾占用此函数。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|自编译后，此函数的执行期间所执行的物理读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_physical_reads**|**bigint**|上次执行该函数时执行物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_physical_reads**|**bigint**|此函数在单次执行期间所执行的物理读取次数最小节点数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_physical_reads**|**bigint**|此函数在单次执行期间所执行的物理读取的最大数目。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_writes**|**bigint**|自编译后，此函数的执行期间所执行的逻辑写入总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_writes**|**bigint**|上次执行计划时变脏的缓冲池页数。 如果页已变脏（已修改），则不计入写次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_writes**|**bigint**|此函数在单次执行期间所执行的逻辑写入次数最小。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_writes**|**bigint**|此函数在单次执行期间所执行的逻辑写入的最大数目。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_reads**|**bigint**|自编译后，此函数的执行期间所执行的逻辑读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_reads**|**bigint**|上次执行该函数时执行的逻辑读取数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_reads**|**bigint**|此函数在单次执行期间所执行的逻辑读取次数最小节点数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_reads**|**bigint**|此函数在单次执行期间所执行的逻辑读取的最大数目。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_elapsed_time**|**bigint**|总运行时间，以微秒为单位，完成此函数的执行。|  
|**last_elapsed_time**|**bigint**|所用的时间以微秒为单位，最近完成此函数的执行。|  
|**min_elapsed_time**|**bigint**|最小运行时间，以微秒为单位，任何已完成此函数的执行。|  
|**max_elapsed_time**|**bigint**|最大运行时间，以微秒为单位，任何已完成此函数的执行。|  
  
## <a name="permissions"></a>Permissions  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="examples"></a>示例  
 以下示例返回有关按平均占用时间衡量的前十个函数的信息。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>请参阅  
 [与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
