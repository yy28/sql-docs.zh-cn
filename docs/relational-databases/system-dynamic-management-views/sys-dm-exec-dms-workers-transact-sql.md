---
title: sys.dm_exec_dms_workers (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 695d31f4a232b071ba847373d291b9e9630e4163
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关所有辅助进程完成 DMS 步骤的信息。  
  
 此视图显示的数据的最后 1000 条请求和活动请求;活动请求始终具有在此视图中提供的数据。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|查询此 DMS 辅助进程是部分 of.request_id，step_index，和 dms_step_index 窗体的密钥，此视图。||  
|step_index|**int**|查询此 DMS 辅助进程是的一部分的步骤。|请参阅中的步骤索引[sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|在此辅助进程正在运行 DMS 计划中的步骤。|请参阅[sys.dm_exec_dms_workers (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|工作进程正在其运行的节点。|请参阅[sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|**int**|||  
|type|**nvarcha(32)**|||  
|status|**nvarchar(32)**|此步骤的状态|挂起，运行，完整、 Failed、 UndoFailed、 PendingCancel，取消，撤消、 中止|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 的此步骤所属于的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，为当前正在执行的步骤设置为 NULL 或排队。|  
|total_elapsed_time|**int**|总已经执行查询的步骤，以毫秒为单位的时间量|之间 0 和 end_time 和 start_time 之间的差异。 对排队的步骤为 0。|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
