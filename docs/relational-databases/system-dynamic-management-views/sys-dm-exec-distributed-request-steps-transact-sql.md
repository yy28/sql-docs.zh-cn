---
title: sys.dm_exec_distributed_request_steps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27df857e8863272f2b502c4950b4cc36ad936978
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401952"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关组合给定的 PolyBase 请求或查询的所有步骤的信息。 它列出了每个查询步骤对应一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 和 step_index 构成此视图的键。 与请求关联的唯一数字 id。|请参阅中的 ID [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|**int**|此步骤的一系列步骤组成该请求中的位置。|0 到 (n-1)，为包含 n 个步骤的请求。|  
|operation_type|**nvarchar(128)**|表示通过此步骤的操作的类型。|MoveOperation、 OnOperation、 RandomIDOperation、 针对以下、 ReturnOperation、 ShuffleMoveOperation、 TempTablePropertiesOperation、 DropDiagnosticsNotifyOperation、 HadoopShuffleOperation、 HadoopBroadCastOperationHadoopRoundRobinOperation|  
|distribution_type|**nvarchar(32)**|执行步骤的位置。|AllComputeNodes、 AllDistributions、 ComputeNode、 分发、 AllNodes、 SubsetNodes、 SubsetDistributions'，' 未指定。|  
|location_type|**nvarchar(32)**|执行步骤的位置。|计算、 Head 或者 DMS。 所有的数据移动步骤显示 DMS。|  
|status|**nvarchar(32)**|此步骤的状态|挂起、 正在运行，Complete、 Failed、 UndoFailed、 PendingCancel，取消，撤消，中止|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id|请参阅 id [sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，则未发生错误的情况下为 NULL。|  
|start_time|**datetime**|在步骤开始执行时间|小于或等于当前时间和更大或等于 end_compile_time 属于此步骤中的查询。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time，当前中执行的步骤设置为 NULL 或排入队列。|  
|total_elapsed_time|**int**|具有已执行的查询步骤，以毫秒为单位的时间的总金额|介于 0 和 end_time 和 start_time 之间的差异。 有关已排队的步骤为 0。|  
|row_count|**bigint**|更改或此请求返回的总行数|有关步骤的未更改或返回的数据，否则影响的行数为 0。 将设置为-1 表示 DMS 步骤。|  
|command|nvarchar(4000)|保留此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 如果长度超过 4000 个字符被截断。|  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 使用动态管理视图进行故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
