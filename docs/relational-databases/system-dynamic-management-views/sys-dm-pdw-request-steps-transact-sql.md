---
title: sys.dm_pdw_request_steps (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 421d8db6ec62035b8605fde1293f727f7a6dc917
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关撰写给定的请求或查询中的所有步骤的信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它列出每个查询步骤的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id step_index 组成的密钥，此视图中。<br /><br /> 与请求关联的唯一数字 id。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|request_id step_index 组成的密钥，此视图中。<br /><br /> 此步骤中的步骤的构成请求序列的位置。|n 个步骤步骤的请求 (n-1) 为 0。|  
|operation_type|**nvarchar(35)**|表示此步骤的操作的类型。|**DMS 查询计划操作：** ReturnOperation、 PartitionMoveOperation、 MoveOperation、 BroadcastMoveOperation、 ShuffleMoveOperation、 TrimMoveOperation、 CopyOperation、 DistributeReplicatedTableMoveOperation<br /><br /> **SQL 查询计划操作：** OnOperation、 RemoteOperation<br /><br /> **其他查询计划操作：** MetaDataCreateOperation、 RandomIDOperation<br /><br /> **读取的外部操作：** HadoopShuffleOperation、 HadoopRoundRobinOperation、 HadoopBroadcastOperation<br /><br /> **有关 MapReduce 的外部操作：** HadoopJobOperation、 HdfsDeleteOperation<br /><br /> **对于写入外部操作：** ExternalExportDistributedOperation、 ExternalExportReplicatedOperation、 ExternalExportControlOperation<br /><br /> 有关详细信息，请参阅"了解查询计划" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。|  
|distribution_type|**nvarchar(32)**|此步骤将进行的分发的类型。|AllNodes、 AllDistributions、 AllComputeNodes、 ComputeNode、 分发、 SubsetNodes、 SubsetDistributions，未指定|  
|location_type|**nvarchar(32)**|其中运行步骤。|计算、 控制，DMS|  
|status|**nvarchar(32)**|此步骤的状态。|挂起、 正在运行、 完成、 失败、 UndoFailed、 PendingCancel，取消、 撤消，中止|  
|error_id|**nvarchar(36)**|如果有与此步骤中，关联的错误的唯一 id。|请参阅的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未发生错误，则为 NULL。|  
|start_time|**datetime**|步骤开始执行的时间。|小于或等于当前时间和更大或等于 end_compile_time 的此步骤所属于的查询。 有关查询的详细信息，请参阅[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|end_time|**datetime**|此步骤完成执行、 已取消，或失败的时间。|小于或等于当前时间和更大或等于 start_time。 为当前正在执行的步骤设置为 NULL 或排队。|  
|total_elapsed_time|**int**|总查询步骤已运行，以毫秒为单位的时间量。|之间 0 和 end_time 和 start_time 之间的差异。 对排队的步骤为 0。<br /><br /> 如果 total_elapsed_time 超过一个整数的最大值，total_elapsed_time 将继续是最大值。 这种情况将生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|row_count|**bigint**|总行数更改，或此请求返回的。|0 表示未更改或未返回数据的步骤。 否则为受影响的行数。|  
|command|**nvarchar(4000)**|包含此步骤的命令的完整文本。|步骤的任何有效的请求字符串。 为 NULL 的类型 MetaDataCreateOperation 操作时。 如果超过 4000 个字符被截断。|  
  
 有关通过此视图保留最大行数的信息，请参阅"最小值和最大值"中的最大的系统视图值部分中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
