---
title: sys.databases _pdw_nodes_exec_query_profiles （Transact-sql） |Microsoft Docs
description: 动态管理视图，可用于在执行查询时监视实时数据仓库查询进度。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7237e7f7b49916e09f4a8c5cab0d7d49486cb971
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145652"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>sys.databases _pdw_nodes_exec_query_profiles （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

在执行查询时监视实时数据仓库查询进度。   
  
## <a name="table-returned"></a>返回的表  
返回的计数器基于每个运算符和每个线程。 结果是动态的，并且不匹配现有选项（如 `SET STATISTICS XML ON`）的结果，这些选项仅在查询完成后才会创建输出。  
  
|列名|“名称”|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**smallint**|与节点关联的唯一数字 ID。|
|session_id|**int**|标识运行此查询的会话。 引用 dm_exec_sessions.session_id。|  
|request_id|**smallint**|确定目标请求。 引用 dm_exec_sessions.request_id。|  
|sql_handle|**varbinary(64)**|是唯一标识查询所属的批处理或存储过程的标记。 引用 dm_exec_query_stats.sql_handle。|  
|plan_handle|**varbinary(64)**|是一个标记，用于唯一标识已执行并且其计划驻留在计划缓存中或当前正在执行的批处理的查询执行计划。 引用 dm_exec_query_stats. plan_handle。|  
|physical_operator_name|**nvarchar(256)**|物理运算符名称。|  
|node_id|**smallint**|标识查询树中的运算符节点。|  
|thread_id|**smallint**|区分属于同一个查询运算符节点的线程（针对并行查询）。|  
|task_address|**varbinary （8）**|确定此线程正在使用的 SQLOS 任务。 引用 dm_os_tasks.task_address。|  
|row_count|**bigint**|运算符迄今返回的行数。|  
|rewind_count|**bigint**|迄今为止的重绕数。|  
|rebind_count|**bigint**|迄今为止的重新绑定数。|  
|end_of_scan_count|**bigint**|迄今为止的扫描结束次数。|  
|estimate_row_count|**bigint**|估计的行数。 可用于将 estimated_row_count 与实际 row_count 进行比较。|  
|first_active_time|**bigint**|首次调用运算符的时间（毫秒）。|  
|last_active_time|**bigint**|上次调用运算符的时间（毫秒）。|  
|open_time|**bigint**|打开时的时间戳（毫秒）。|  
|first_row_time|**bigint**|打开第一行时的时间戳（毫秒）。|  
|last_row_time|**bigint**|打开最后一行时的时间戳（毫秒）。|  
|close_time|**bigint**|关闭时的时间戳（毫秒）。|  
|elapsed_time_ms|**bigint**|到目前为止，目标节点的操作所用的总运行时间（毫秒）。|  
|cpu_time_ms|**bigint**|到目前为止，目标节点的操作使用的总 CPU 时间（毫秒）。|  
|database_id|**int**|包含要对其进行读写的对象的数据库的 ID。|  
|object_id|**smallint**|要对其进行读写的对象的标识符。 引用 sys.objects.object_id。|  
|index_id|**smallint**|打开其行级的索引（如果有）。|  
|scan_count|**bigint**|迄今为止的表/索引扫描数。|  
|logical_read_count|**bigint**|迄今为止的逻辑读取数。|  
|physical_read_count|**bigint**|迄今为止的物理读取数。|  
|read_ahead_count|**bigint**|迄今为止的预读数。|  
|write_page_count|**bigint**|迄今为止由于溢出而导致的页写入数。|  
|lob_logical_read_count|**bigint**|迄今为止的 LOB 逻辑读取数。|  
|lob_physical_read_count|**bigint**|迄今为止的 LOB 物理读取数。|  
|lob_read_ahead_count|**bigint**|迄今为止的 LOB 预读数。|  
|segment_read_count|**smallint**|迄今为止的段预读数。|  
|segment_skip_count|**smallint**|迄今为止跳过的段数。| 
|actual_read_row_count|**bigint**|应用驻留谓词之前由运算符读取的行数。| 
|estimated_read_row_count|**bigint**|**适用于：** 从 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 开始。 <br/>在应用残留谓词之前估计要由运算符读取的行数。|  
  
## <a name="remarks"></a>注释  
[_Exec_query_profiles](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql?view=sql-server-ver15)中的相同备注适用。  

## <a name="permissions"></a>Permissions  
 要求具有对服务器的 `VIEW SERVER STATE` 权限。  

## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>后续步骤
 有关更多开发技巧，请参阅[SQL 数据仓库开发概述](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。
