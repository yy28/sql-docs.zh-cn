---
title: sys.dm_pdw_dms_workers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 96fd36d1710a166285fecba092735c7d2495271e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690447"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关所有工作线程完成 DMS 步骤的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|查询的此 DMS 辅助进程的一部分。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|查询此 DMS 辅助角色是的一部分的步骤。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。|请参阅中的 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|运行此工作线程在 DMS 计划中的步骤。<br /><br /> request_id、 step_index 和 dms_step_index 构成此视图的键。||  
|pdw_node_id|**int**|辅助角色运行的节点。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**Int**|正在运行工作线程，如果有的分发。|请参阅中的 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。|  
|type|**nvarchar(32)**|此条目表示的 DMS 辅助线程的类型。|DIRECT_CONVERTER、 DIRECT_READER、 FILE_READER、 HASH_CONVERTER、 HASH_READER、 ROUNDROBIN_CONVERTER、 EXPORT_READER、 EXTERNAL_READER、 EXTERNAL_WRITER、 PARALLEL_COPY_READER、 REJECT_WRITER、 写入器|  
|status|**nvarchar(32)**|DMS 辅助角色的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|上一秒钟内读取或写入吞吐量。|大于或等于 0。 如果查询已取消或失败之前无法执行辅助角色为 NULL。|  
|bytes_processed|**bigint**|处理此工作线程的总字节数。|大于或等于 0。 如果查询已取消或失败之前无法执行辅助角色为 NULL。|  
|rows_processed|**bigint**|行读取或写入此工作线程数。|大于或等于 0。 如果查询已取消或失败之前无法执行辅助角色为 NULL。|  
|start_time|**datetime**|此工作线程的执行开始时间。|大于或等于此辅助角色所属的查询步骤的开始时间。 请参阅[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|时间的执行将结束、 失败或已取消。|对于正在进行或排入队列的辅助角色为 NULL。 否则为大于 start_time。|  
|total_elapsed_time|**int**|所用的执行，以毫秒为单位的总时间。|大于或等于 0。<br /><br /> 系统启动或重新启动后经过的总时间。 如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|cpu_time|**bigint**|使用此工作线程，以毫秒为单位的 CPU 时间。|大于或等于 0。|  
|query_time|**int**|长时间内 SQL 启动行返回到线程，以毫秒为单位。|大于或等于 0。|  
|buffers_available|**int**|未使用的缓冲区数。| 如果查询已取消或失败之前无法执行辅助角色为 NULL。|  
|sql_spid|**int**|此 DMS 辅助角色执行工作的 SQL Server 实例上的会话 id。||  
|dms_cpid|**int**|运行的实际线程的进程 ID。||  
|error_id|**nvarchar(36)**|如果有此工作线程的执行过程中发生的错误的唯一标识符。|请参阅中的 error_id [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|source_info|**nvarchar(4000)**|对于读取器，源表和源列的规范。||  
|destination_info|**nvarchar(4000)**|编写器，目标表的规范。||  
  
 此视图按保留的最大行有关的信息，请参阅中的元数据部分[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题...  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
