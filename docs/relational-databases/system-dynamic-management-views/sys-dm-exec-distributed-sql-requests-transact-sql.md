---
title: sys.dm_exec_distributed_sql_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ee6ce9ae453eb58bfa8dde2406c630b966287007
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540577"
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  在查询中包含有关所有 SQL 查询分布作为 SQL 步骤的一部分的信息。  此视图显示的最后 1000 条请求; 的数据活动请求始终具有此视图中的数据。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id 和 step_index 构成此视图的键。 与请求关联的唯一数字 id。|请参阅中的 ID [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|此分布是一部分的查询步骤的索引。|请参阅中的 step_index [sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|compute_node_id|**int**|表示通过此步骤的操作的类型。|请参阅中的 compute_node_id [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|**int**|执行步骤的位置。|将设置为-1 表示运行在节点范围内不分发范围的请求。|  
|status|**nvarchar(32)**|此步骤的状态|活动、 已取消、 已完成、 失败、 已排队|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id|请参阅 id [sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，则未发生错误的情况下为 NULL。|  
|start_time|**datetime**|在步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 属于此步骤中的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，当前中执行的步骤设置为 NULL 或排入队列。|  
|total_elapsed_time|**int**|具有已执行的查询步骤，以毫秒为单位的时间的总金额|介于 0 和 end_time 和 start_time 之间的差异。 有关已排队的步骤为 0。|  
|row_count|**bigint**|更改或此请求返回的总行数|有关步骤的未更改或返回的数据，否则影响的行数为 0。 将设置为-1 表示 DMS 步骤。|  
|spid|**int**|在执行查询分发的 SQL Server 实例上的会话 id||  
|command|nvarchar(4000)|保留此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 如果长度超过 4000 个字符被截断。|  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
