---
title: sys.dm_exec_distributed_request_steps (TRANSACT-SQL) |Microsoft 文档
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
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f226ff8c5f18a0e812c6a457fe3382cb8f7b8d84
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464833"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  包含构成给定的 PolyBase 请求或查询的所有步骤的信息。 它列出每个查询步骤的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id step_index 组成的密钥，此视图中。 与请求关联的唯一数字 id。|在中看到 ID [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|**int**|此步骤中的步骤的构成请求序列的位置。|n 个步骤步骤的请求 (n-1) 为 0。|  
|operation_type|**nvarchar(128)**|所表示的此步骤操作的类型。|'MoveOperation','OnOperation','RandomIDOperation','RemoteOperation','ReturnOperation','ShuffleMoveOperation','TempTablePropertiesOperation','DropDiagnosticsNotifyOperation', ‘HadoopShuffleOperation', ‘HadoopBroadCastOperation', ‘HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|其中执行的步骤。|AllComputeNodes '，' AllDistributions、 ComputeNode、 分发、 AllNodes、 SubsetNodes、 SubsetDistributions'，' 未指定。|  
|location_type|**nvarchar(32)**|其中执行的步骤。|计算、 Head 或者 DMS。 所有数据移动步骤都演示了 DMS。|  
|status|**nvarchar(32)**|此步骤的状态|挂起，运行，完整、 Failed、 UndoFailed、 PendingCancel，取消，撤消、 中止|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id|请参阅 id [sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)、 未发生错误的情况下为 NULL。|  
|start_time|**datetime**|步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 的此步骤所属于的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，为当前正在执行的步骤设置为 NULL 或排队。|  
|total_elapsed_time|**int**|总已经执行查询的步骤，以毫秒为单位的时间量|之间 0 和 end_time 和 start_time 之间的差异。 对排队的步骤为 0。|  
|row_count|**bigint**|更改或此请求返回的行的总数|有关步骤，未更改或未返回数据，否则影响的行数为 0。 设置为-1 可 DMS 步骤。|  
|command|nvarchar(4000)|包含此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 如果超过 4000 个字符被截断。|  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
