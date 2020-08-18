---
description: sys.dm_exec_dms_workers (Transact-SQL)
title: sys. dm_exec_dms_workers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1dd32f2bd3a810e01dc7bf50347b0a23a884796
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88398613"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>sys.dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关完成 DMS 步骤的所有工作线程的信息。  
  
 此视图显示最后一个1000请求和活动请求的数据;活动请求始终具有此视图中的数据。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|查询此 DMS 工作线程所属的部分。 request_id、step_index 和 dms_step_index 构成此视图的键。||  
|step_index|`int`|查询步骤此 DMS 辅助角色所属的部分。|请参阅 sys.databases 中的步骤索引 [&#40;transact-sql&#41;dm_exec_distributed_request_steps ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|dms_step_index|`int`|此工作线程正在运行的 DMS 计划中的步骤。|请参阅 [dm_exec_dms_workers (transact-sql) ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|`int`|正在运行辅助角色的节点。|请参阅 [sys.databases &#40;transact-sql&#41;dm_exec_compute_nodes ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|`int`|||  
|type|`nvarcha(32)`|||  
|状态|`nvarchar(32)`|此步骤的状态|"挂起"、"正在运行"、"完成"、"失败"、"UndoFailed"、"PendingCancel"、"已取消"、"撤消"、"已中止"|  
|bytes_per_sec|`bigint`|||  
|bytes_processed|`bigint`|||  
|rows_processed|`bigint`|||  
|start_time|`datetime`|步骤开始执行的时间|小于或等于当前时间，大于或等于此步骤所属的查询 end_compile_time。|  
|end_time|`datetime`|此步骤完成执行、已取消或失败的时间。|小于或等于当前时间，大于或等于 start_time，则将设置为 NULL 以查看当前正在执行或已排队的步骤。|  
|total_elapsed_time|`int`|执行查询步骤的总时间（毫秒）|介于0与 end_time 与 start_time 之间的差异。 对于排队步骤，为0。|  
|cpu_time|`bigint`|||  
|query_time|`int`|||  
|buffers_available|`int`|||  
|dms_cpid|`int`|||  
|sql_spid|`int`|||  
|error_id|`nvarchar(36)`|||  
|source_info|`nvarchar(4000)`|||  
|destination_info|`nvarchar(4000)`|||  
|command|`nvarchar(4000)`|||
|compute_pool_id|`int`|池的唯一标识符。|

## <a name="see-also"></a>另请参阅  
 [通过动态管理视图进行 PolyBase 故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
