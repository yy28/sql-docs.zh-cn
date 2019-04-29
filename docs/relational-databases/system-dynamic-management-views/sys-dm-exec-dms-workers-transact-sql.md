---
title: sys.dm_exec_dms_workers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a31b03208eba573fc6bd50f2348733ef0a07c2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013326"
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关所有工作线程完成 DMS 步骤的信息。  
  
 此视图显示的最后 1000 个请求和活动请求; 的数据活动请求始终具有此视图中的数据。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|查询此 DMS 辅助进程是部分 of.request_id，step_index，和 dms_step_index 构成此视图的键。||  
|step_index|**int**|查询此 DMS 辅助角色是的一部分的步骤。|请参阅中的步索引[sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|运行此工作线程在 DMS 计划中的步骤。|See [sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|辅助角色运行的节点。|请参阅[sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|**int**|||  
|type|**nvarcha(32)**|||  
|status|**nvarchar(32)**|此步骤的状态|挂起、 正在运行，Complete、 Failed、 UndoFailed、 PendingCancel，取消，撤消，中止|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|在步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 属于此步骤中的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，当前中执行的步骤设置为 NULL 或排入队列。|  
|total_elapsed_time|**int**|具有已执行的查询步骤，以毫秒为单位的时间的总金额|介于 0 和 end_time 和 start_time 之间的差异。 有关已排队的步骤为 0。|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 使用动态管理视图进行故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
