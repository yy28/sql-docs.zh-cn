---
title: sys.dm_exec_distributed_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ae66757f7d7977ab91420267d6c45be205d72c4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  在查询中包含所有 SQL 查询分发信息作为 SQL 步骤的一部分。  此视图显示的最后 1000 条请求; 的数据活动请求始终具有在此视图中提供的数据。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id step_index 组成的密钥，此视图中。 与请求关联的唯一数字 id。|在中看到 ID [sys.dm_exec_requests &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|此分布是的一部分的查询步骤索引。|请参阅中的 step_index [sys.dm_exec_distributed_request_steps &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**int**|所表示的此步骤操作的类型。|请参阅中的 compute_node_id [sys.dm_exec_compute_nodes &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|其中执行的步骤。|设置为-1 可运行于的节点范围不分发范围的请求。|  
|status|**nvarchar(32)**|此步骤的状态|活动、 取消、 已完成、 失败、 排队|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id|请参阅 id [sys.dm_exec_compute_node_errors &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)、 未发生错误的情况下为 NULL。|  
|start_time|**datetime**|步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 的此步骤所属于的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，为当前正在执行的步骤设置为 NULL 或排队。|  
|total_elapsed_time|**int**|总已经执行查询的步骤，以毫秒为单位的时间量|之间 0 和 end_time 和 start_time 之间的差异。 对排队的步骤为 0。|  
|row_count|**bigint**|更改或此请求返回的行的总数|有关步骤，未更改或未返回数据，否则影响的行数为 0。 设置为-1 可 DMS 步骤。|  
|spid|**int**|在执行查询分发的 SQL Server 实例上的会话 id||  
|command|nvarchar(4000)|包含此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 如果超过 4000 个字符被截断。|  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
