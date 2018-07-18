---
title: sys.dm_pdw_request_steps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5a6fbf843d3a9aca9172a5ab6ea828a0c0b0a40a
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926838"
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关编写给定的请求或查询中的所有步骤的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它列出了每个查询步骤对应一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id 和 step_index 构成此视图的键。<br /><br /> 与请求关联的唯一数字 id。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|request_id 和 step_index 构成此视图的键。<br /><br /> 此步骤的一系列步骤组成该请求中的位置。|0 到 (n-1)，为包含 n 个步骤的请求。|  
|operation_type|**nvarchar(35)**|表示此步骤的操作的类型。|**DMS 查询计划操作：** ReturnOperation、 执行、 MoveOperation、 为 BroadcastMoveOperation、 ShuffleMoveOperation、 针对以下、 CopyOperation、 DistributeReplicatedTableMoveOperation<br /><br /> **SQL 查询计划操作：** OnOperation、 针对以下<br /><br /> **其他查询计划操作：** MetaDataCreateOperation、 RandomIDOperation<br /><br /> **对于读取外部操作：** HadoopShuffleOperation、 HadoopRoundRobinOperation、 HadoopBroadcastOperation<br /><br /> **有关 MapReduce 的外部操作：** HadoopJobOperation、 HdfsDeleteOperation<br /><br /> **对于写入外部操作：** ExternalExportDistributedOperation、 ExternalExportReplicatedOperation、 ExternalExportControlOperation<br /><br /> 详细信息，请参阅"了解查询计划"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。|  
|distribution_type|**nvarchar(32)**|此步骤中将进行的分布的类型。|AllNodes、 AllDistributions、 AllComputeNodes、 ComputeNode、 分发、 SubsetNodes、 SubsetDistributions、 未指定|  
|location_type|**nvarchar(32)**|其中步骤正在运行。|计算、 控制，DMS|  
|status|**nvarchar(32)**|此步骤的状态。|挂起、 正在运行、 完成、 失败、 UndoFailed、 PendingCancel，已取消、 撤消、 已中止|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id。|请参阅的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未发生错误，则为 NULL。|  
|start_time|**datetime**|在步骤开始执行的时间。|小于或等于当前时间和更大或等于 end_compile_time 属于此步骤中的查询。 有关查询的详细信息，请参阅[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time。 有关当前正在执行的步骤设置为 NULL 或排入队列。|  
|total_elapsed_time|**int**|已运行的查询步骤，以毫秒为单位的时间总量。|介于 0 和 end_time 和 start_time 之间的差异。 有关已排队的步骤为 0。<br /><br /> 如果 total_elapsed_time 超出整数的最大值，将持续 total_elapsed_time 可最大值。 这种情况会生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|row_count|**bigint**|总行数发生更改，或此请求返回。|0 表示未更改或返回数据的步骤。 否则为受影响的行数。|  
|command|**nvarchar(4000)**|保留此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 如果该操作的类型 MetaDataCreateOperation，值为 NULL。 如果长度超过 4000 个字符被截断。|  
  
 此视图按保留的最大行有关的信息，请参阅"最小值和最大值"中的系统视图的最大值部分中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
