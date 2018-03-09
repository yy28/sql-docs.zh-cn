---
title: "sys.dm_db_task_space_usage (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_task_space_usage_TSQL
- sys.dm_db_task_space_usage_TSQL
- dm_db_task_space_usage
- sys.dm_db_task_space_usage
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_task_space_usage dynamic management view
ms.assetid: fb0c87e5-43b9-466a-a8df-11b3851dc6d0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a10c12a2510baaace72219803e9f3cc26bebf20
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtaskspaceusage-transact-sql"></a>sys.dm_db_task_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回任务为数据库进行的页分配和释放活动。  
  
> [!NOTE]  
>  此视图是仅适用于[tempdb 数据库](../../relational-databases/databases/tempdb-database.md)。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_db_task_space_usage**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|会话 ID。|  
|**request_id**|**int**|会话内的请求 ID。<br /><br /> 请求也称为批，可以包含一个或多个查询。 一个会话可以同时具有多个活动请求。 如果使用并行执行计划，则请求中的每个查询可以启动多个线程（任务）。|  
|**exec_context_id**|**int**|任务的执行上下文 ID。 有关详细信息，请参阅[sys.dm_os_tasks &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|**database_id**|**int**|数据库 ID。|  
|**user_objects_alloc_page_count**|**bigint**|此任务为用户对象保留或分配的页数。|  
|**user_objects_dealloc_page_count**|**bigint**|此任务为用户对象释放并不再保留的页数。|  
|**internal_objects_alloc_page_count**|**bigint**|此任务为内部对象保留或分配的页数。|  
|**internal_objects_dealloc_page_count**|**bigint**|此任务为内部对象释放并不再保留的页数。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  
 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要服务器上的 VIEW SERVER STATE 权限。  
  
 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要 VIEW DATABASE STATE 权限的数据库中。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。  
  
## <a name="remarks"></a>注释  
 此视图所报告的任何页计数均不包括 IAM 页。  
  
 在请求开始时，页计数器被初始化为零 (0)。 在请求完成时，这些值将在会话级别聚合。 有关详细信息，请参阅[sys.dm_db_session_space_usage &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md).  
  
 工作表缓存、临时表缓存和延迟的删除操作会影响在指定任务中分配和释放的页数。  
  
## <a name="user-objects"></a>用户对象  
 用户对象页计数器中包括下列对象：  
  
-   用户定义的表和索引  
  
-   系统表和索引  
  
-   全局临时表和索引  
  
-   局部临时表和索引  
  
-   表变量  
  
-   表值函数中返回的表  
  
## <a name="internal-objects"></a>内部对象  
 内部对象才在**tempdb**。 内部对象页计数器中包括下列对象：  
  
-   用于游标或假脱机操作以及临时大型对象 (LOB) 存储的工作表  
  
-   用于哈希联接等操作的工作文件  
  
-   排序段  
  
## <a name="physical-joins"></a>物理联接  
 ![有关 sys.dm_db_session_task_usage 物理联接](../../relational-databases/system-dynamic-management-views/media/join-dm-db-task-space-usage-1.gif "物理联接为 sys.dm_db_session_task_usage")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|dm_db_task_space_usage.request_id|dm_exec_requests.request_id|一对一|  
|dm_db_task_space_usage.session_id|dm_exec_requests.session_id|一对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  


