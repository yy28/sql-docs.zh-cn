---
title: sys.dm_pdw_dms_workers (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad9e41d1092f17d2fb5c37b7f16d2f6be056506b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关所有辅助进程完成 DMS 步骤的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 DMS 辅助进程是的一部分的查询。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|查询此 DMS 辅助进程是的一部分的步骤。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。|请参阅中的 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|在此辅助进程正在运行 DMS 计划中的步骤。<br /><br /> request_id、 step_index 和 dms_step_index 窗体的密钥，此视图。||  
|pdw_node_id|**int**|工作进程正在其运行的节点。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**Int**|如果有工作线程运行的分发。|请参阅中的 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。|  
|type|**nvarchar(32)**|此条目表示的 DMS 工作线程的类型。|DIRECT_CONVERTER、 DIRECT_READER、 FILE_READER、 HASH_CONVERTER、 HASH_READER、 ROUNDROBIN_CONVERTER、 EXPORT_READER、 EXTERNAL_READER、 EXTERNAL_WRITER、 PARALLEL_COPY_READER、 REJECT_WRITER、 写入器|  
|status|**nvarchar(32)**|DMS 辅助进程的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|在最后一秒中读取或写入吞吐量。|大于或等于 0。 如果查询已取消或失败之前无法执行工作线程，则为 NULL。|  
|bytes_processed|**bigint**|此工作线程处理的总字节数。|大于或等于 0。 如果查询已取消或失败之前无法执行工作线程，则为 NULL。|  
|rows_processed|**bigint**|读取或写入为此工作人员的行数。|大于或等于 0。 如果查询已取消或失败之前无法执行工作线程，则为 NULL。|  
|start_time|**datetime**|此辅助进程的执行开始时间。|大于或等于此辅助进程所属的查询步骤的开始时间。 请参阅[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|从该处执行将结束、 失败或已取消的时间。|正在进行或已排队的工作人员的为 NULL。 否则为大于 start_time。|  
|total_elapsed_time|**int**|在执行，以毫秒为单位中花费的总时间。|大于或等于 0。<br /><br /> 系统启动或重新启动后经过的总时间。 如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|cpu_time|**bigint**|使用此辅助进程，以毫秒为单位的 CPU 时间。|大于或等于 0。|  
|query_time|**int**|SQL 之前的时间段开始到线程，以毫秒为单位返回行。|大于或等于 0。|  
|buffers_available|**int**|未使用的缓冲区数。| 如果查询已取消或失败之前无法执行工作线程，则为 NULL。|  
|sql_spid|**int**|对于此 DMS 工作进程中执行此工作的 SQL Server 实例上的会话 id。||  
|dms_cpid|**int**|运行的实际线程的进程 ID。||  
|error_id|**nvarchar(36)**|如果有的话，此辅助进程的执行期间出现的错误的唯一标识符。|请参阅中的 error_id [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|source_info|**nvarchar(4000)**|对于读取器，源表和列的规范。||  
|destination_info|**nvarchar(4000)**|为的编写器，目标表规范。||  
  
 有关通过此视图保留最大行数的信息，请参阅[最大的系统视图值](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
