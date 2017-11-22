---
title: "sys.dm_exec_procedure_stats (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f935b0e9a4c150830a03ecb2ea1f67a4cd270d3f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回缓存存储过程的聚合性能统计信息。 该视图为每个缓存的存储过程计划都返回一行，行的生存期与存储过程保持缓存状态的时间一样长。 在从缓存中删除存储过程时，也将从该视图中删除对应行。 此时，Performance Statistics SQL 跟踪事件将引发类似于**sys.dm_exec_query_stats**。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  
  
> **注意：**的初始查询**sys.dm_exec_procedure_stats**可能会产生不准确的结果，如果没有在服务器上当前正在执行的工作负荷。 可以通过重新运行查询来确定更准确的结果。  
  
> **Azure SQL 数据仓库的注意 ！** 若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_procedure_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|存储过程所在的数据库 ID。|  
|**object_id**|**int**|存储过程的对象标识号。|  
|**type**|**char(2)**|对象的类型：<br /><br /> P = SQL 存储过程<br /><br /> PC = 程序集 (CLR) 存储过程<br /><br /> X = 扩展存储过程|  
|**type_desc**|**nvarchar(60)**|对对象类型的说明：<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql 句柄**|**varbinary(64)**|这可用来查询关联**sys.dm_exec_query_stats** ，此存储过程中执行的。|  
|**plan_handle 收集**|**varbinary(64)**|内存中计划的标识符。 该标识符是瞬态的，仅当计划保留在缓存中时，它才保持不变。 此值可用于**sys.dm_exec_cached_plans**动态管理视图。<br /><br /> 当本机编译的存储过程查询内存优化的表时，此项将始终为 0x000。|  
|**cached_time**|**datetime**|存储过程添加到缓存的时间。|  
|**last_execution_time**|**datetime**|上次执行存储过程的时间。|  
|**execution_count**|**bigint**|存储过程自上次编译以来所执行的次数。|  
|**total_worker_time**|**bigint**|此存储过程自编译以来执行所用的 CPU 时间总量（微秒）。<br /><br /> 对于本机编译的存储过程，如果许多执行所用的时间都不到 1 毫秒，则 **total_worker_time** 可能不精确。|  
|**last_worker_time**|**bigint**|上次执行存储过程所用的 CPU 时间（微秒）。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|此存储过程在单次执行期间曾占用的最小 CPU 时间（微秒）。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|此存储过程在单次执行期间曾占用的最大 CPU 时间（微秒）。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|此存储过程自编译后在执行期间所执行的物理读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_physical_reads**|**bigint**|上次执行存储过程时所执行的物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_physical_reads**|**bigint**|该存储过程在单次执行期间所执行的最少物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_physical_reads**|**bigint**|该存储过程在单次执行期间所执行的最大物理读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_writes**|**bigint**|此存储过程自编译后在执行期间所执行的逻辑写入总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_writes**|**bigint**|上次执行计划时变脏的缓冲池页数。 如果页已变脏（已修改），则不计入写次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_writes**|**bigint**|该存储过程在单次执行期间所执行的最少逻辑写入次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_writes**|**bigint**|该存储过程在单次执行期间所执行的最大逻辑写入次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_logical_reads**|**bigint**|此存储过程自编译后在执行期间所执行的逻辑读取总次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**last_logical_reads**|**bigint**|上次执行存储过程时所执行的逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**min_logical_reads**|**bigint**|该存储过程在单次执行期间所执行的最少逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**max_logical_reads**|**bigint**|该存储过程在单次执行期间所执行的最大逻辑读取次数。<br /><br /> 当查询内存优化的表时，此项将始终为 0。|  
|**total_elapsed_time**|**bigint**|完成此存储过程的执行所用的总时间（微秒）。|  
|**last_elapsed_time**|**bigint**|最近完成此存储过程的执行所用的时间（微秒）。|  
|**min_elapsed_time**|**bigint**|任意一次完成此存储过程的执行所用的最短时间（微秒）。|  
|**max_elapsed_time**|**bigint**|任意一次完成此存储过程的执行所用的最长时间（微秒）。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
 <sup>1</sup>对于本机编译存储过程启用统计信息收集后，工作线程时间收集以毫秒为单位。 如果查询执行不到 1 毫秒，则该值将为 0。  
  
## <a name="permissions"></a>Permissions  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。 
  
## <a name="remarks"></a>注释  
 存储过程执行完成后，将更新该视图中的统计信息。  
  
## <a name="examples"></a>示例  
 以下示例返回有关按平均占用时间衡量的前十个存储过程的信息。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行相关的动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
  


