---
title: sys.dm_exec_query_memory_grants (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2332e4f80e0dded930b22d9f0faf76d80ec09141
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013235"
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关所有已请求并等待内存授予或已被授予的内存授予的查询的信息。 不需要的内存授予的查询不会出现在此视图。 例如，排序和哈希联接操作都具有以执行查询，而无需查询时的内存授予**ORDER BY**子句将没有内存授予。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 若要避免公开此类信息，包含不属于已连接租户的数据的每一行都筛选掉。此外，列中的值**scheduler_id**， **wait_order**， **pool_id**， **group_id**进行筛选; 设置列的值为 NULL。  
  
> [!NOTE]  
> 若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_query_memory_grants**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|正在运行查询的会话 ID (SPID)。|  
|**request_id**|**int**|请求的 ID。 在会话的上下文中是唯一的。|  
|**scheduler_id**|**int**|正在计划查询的计划程序的 ID。|  
|**dop**|**smallint**|查询的并行度。|  
|**request_time**|**datetime**|查询请求内存授予的日期和时间。|  
|**grant_time**|**datetime**|向查询授予内存的日期和时间。 如果尚未授予内存，则此值为 NULL。|  
|**requested_memory_kb**|**bigint**|请求的内存总量 (KB)。|  
|**granted_memory_kb**|**bigint**|实际授予的内存总量 (KB)。 如果尚未授予内存，该值可以为 NULL。 对于典型的情况下，此值应为相同**requested_memory_kb**。 创建索引时，除了初始授予的内存外，服务器还允许增加按需分配的内存。|  
|**required_memory_kb**|**bigint**|运行查询所需的最小内存 (KB)。 **requested_memory_kb**等于或大于该值。|  
|**used_memory_kb**|**bigint**|此刻使用的物理内存 (KB)。|  
|**max_used_memory_kb**|**bigint**|到此刻为止所用的最大物理内存 (KB)。|  
|**query_cost**|**float**|估计查询开销。|  
|**timeout_sec**|**int**|查询放弃内存授予请求前的超时时间（秒）。|  
|**resource_semaphore_id**|**smallint**|此查询正在等待的资源信号量的非唯一 ID。<br /><br /> **注意：** 此 ID 是唯一的版本中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。 此更改会对故障排除查询执行造成影响。 有关详细信息，请参阅本主题后面的"备注"部分。|  
|**queue_id**|**smallint**|查询等待内存授予时所在等待队列的 ID。 如果已授予内存，则为 NULL。|  
|**wait_order**|**int**|正在等待的查询中指定的连续顺序**queue_id**。 如果其他查询获得内存授予或超时时间，此值可以更改给定的查询。如果已授予内存，则为 NULL。|  
|**is_next_candidate**|**bit**|下一个内存授予的候选对象。<br /><br /> 1 = 是<br /><br /> 0 = 否<br /><br /> NULL = 已授予内存。|  
|**wait_time_ms**|**bigint**|等待时间（毫秒）。 如果已授予内存，则为 NULL。|  
|**plan_handle**|**varbinary(64)**|查询计划的标识符。 使用**sys.dm_exec_query_plan**提取实际的 XML 计划。|  
|**sql_handle**|**varbinary(64)**|查询的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文本标识符。 使用**sys.dm_exec_sql_text**可获取实际[!INCLUDE[tsql](../../includes/tsql-md.md)]文本。|  
|**group_id**|**int**|在其中运行此查询的工作负荷组的 ID。|  
|**pool_id**|**int**|该工作负荷组所属的资源池的 ID。|  
|**is_small**|**tinyint**|如果设置为 1，则指示此授予使用小型资源信号量。 如果设置为 0，则指示使用常规信号量。|  
|**ideal_memory_kb**|**bigint**|将所有内容存放在物理内存中所需的内存授予的大小（以 KB 为单位）。 这基于基数估计。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
   
## <a name="remarks"></a>备注  
 查询超时的典型调试情况可能如下所示：  
  
-   检查总体系统内存状态使用[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)， [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)，和各种性能计数器。  
  
-   检查在查询执行内存预留**sys.dm_os_memory_clerks**其中`type = 'MEMORYCLERK_SQLQERESERVATIONS'`。  
  
-   检查查询正在等待<sup>1</sup>授权使用的**sys.dm_exec_query_memory_grants**。  
  
    ```sql  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
    
    <sup>1</sup>在此方案中，等待类型通常是 RESOURCE_SEMAPHORE。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 
  
-   搜索查询的缓存使用的内存授予[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)并[sys.dm_exec_query_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```sql  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
    ```  
  
-   进一步检查占用大量内存的查询使用[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。  
  
    ```sql  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
      plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
    ```  
  
-   如果怀疑有失控查询，检查从 Showplan [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)和批处理中的文本[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)。  
  
 使用动态管理视图中包括的查询`ORDER BY`或聚合可能会增加内存消耗并进而产生需正在排查的问题的。  
  
 数据库管理员可以使用资源调控器功能在多个资源池之间分发服务器资源，最多可为 64 个池。 从[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，每个池都类似于一个小型的独立服务器实例并且要求 2 个信号量。 从返回的行数**sys.dm_exec_query_resource_semaphores**可能会最多 20 次中返回的行超过[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)     
 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [与执行相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
