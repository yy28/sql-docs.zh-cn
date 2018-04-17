---
title: sys.dm_exec_query_memory_grants (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f564f6b610996d00d366a4ade1af8204d688a44f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关已请求并等待内存授予或已被授予内存授予的所有查询信息。 不需要内存授予的查询将不会出现在此视图中。 例如，排序和哈希联接操作设置为查询的执行，而无需查询时的内存授予**ORDER BY**子句不会授予的内存。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。此外，列中的值**scheduler_id**， **wait_order**， **pool_id**， **group_id**进行筛选; 列的值设置为 NULL。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_query_memory_grants**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|正在运行查询的会话 ID (SPID)。|  
|**request_id**|**int**|请求的 ID。 在会话的上下文中是唯一的。|  
|**scheduler_id**|**int**|正在计划查询的计划程序的 ID。|  
|**dop**|**int**|查询的并行度。|  
|**request_time**|**datetime**|查询请求内存授予的日期和时间。|  
|**grant_time**|**datetime**|向查询授予内存的日期和时间。 如果尚未授予内存，则此值为 NULL。|  
|**requested_memory_kb**|**bigint**|请求的内存总量 (KB)。|  
|**granted_memory_kb**|**bigint**|实际授予的内存总量 (KB)。 如果尚未授予内存，该值可以为 NULL。 对于典型的情况下，此值应为相同**requested_memory_kb**。 创建索引时，除了初始授予的内存外，服务器还允许增加按需分配的内存。|  
|**required_memory_kb**|**bigint**|运行查询所需的最小内存 (KB)。 **requested_memory_kb**等于或大于此量。|  
|**used_memory_kb**|**bigint**|此刻使用的物理内存 (KB)。|  
|**max_used_memory_kb**|**bigint**|到此刻为止所用的最大物理内存 (KB)。|  
|**query_cost**|**float**|估计查询开销。|  
|**timeout_sec**|**int**|查询放弃内存授予请求前的超时时间（秒）。|  
|**resource_semaphore_id**|**int**|此查询正在等待的资源信号量的非唯一 ID。<br /><br /> **注意：**此 ID 是唯一的版本中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。 此更改会对故障排除查询执行造成影响。 有关详细信息，请参阅本主题中后面的"备注"部分。|  
|**queue_id**|**int**|查询等待内存授予时所在等待队列的 ID。 如果已授予内存，则为 NULL。|  
|**wait_order**|**int**|等待查询在指定的连续顺序**queue_id**。 如果其他查询获得内存授予或超时，则给定查询的该值可以更改。如果已授予内存，则为 NULL。|  
|**is_next_candidate**|**bit**|下一个内存授予的候选对象。<br /><br /> 1 = 是<br /><br /> 0 = 否<br /><br /> NULL = 已授予内存。|  
|**wait_time_ms**|**bigint**|等待时间（毫秒）。 如果已授予内存，则为 NULL。|  
|**plan_handle**|**varbinary(64)**|查询计划的标识符。 使用**sys.dm_exec_query_plan**提取实际的 XML 计划。|  
|**sql_handle**|**varbinary(64)**|查询的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文本标识符。 使用**sys.dm_exec_sql_text**以获取实际[!INCLUDE[tsql](../../includes/tsql-md.md)]文本。|  
|**group_id**|**int**|在其中运行此查询的工作负荷组的 ID。|  
|**pool_id**|**int**|该工作负荷组所属的资源池的 ID。|  
|**is_small**|**tinyint**|如果设置为 1，则指示此授予使用小型资源信号量。 如果设置为 0，则指示使用常规信号量。|  
|**ideal_memory_kb**|**bigint**|将所有内容存放在物理内存中所需的内存授予的大小（以 KB 为单位）。 这基于基数估计。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
   
## <a name="remarks"></a>注释  
 查询超时的典型调试情况可能如下所示：  
  
-   请检查总体系统内存状态使用[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)， [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，和各种性能计数器。  
  
-   中的查询执行内存预留检查**sys.dm_os_memory_clerks**其中`type = 'MEMORYCLERK_SQLQERESERVATIONS'`。  
  
-   检查查询等待授予使用**sys.dm_exec_query_memory_grants**。  
  
    ```  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
  
-   搜索与使用的内存授予的查询的缓存[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)和[sys.dm_exec_query_plan &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
  
    ```  
  
-   进一步检查占用大量内存的查询使用[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。  
  
    ```  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    Plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
  
    ```  
  
-   如果怀疑有失控查询，检查从 Showplan [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)和批处理中的文本[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)。  
  
 如果查询使用的动态管理视图中包括 ORDER BY 或聚合，则可能会增加内存占用，进而产生需进行故障排除的问题。  
  
 数据库管理员可以使用资源调控器功能在多个资源池之间分发服务器资源，最多可为 64 个池。 开头[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，每个池的行为类似的小型的独立服务器实例，且需要 2 信号量。 从返回的行数**sys.dm_exec_query_resource_semaphores**可以是最多 20 次中返回的行超过[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)   
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


