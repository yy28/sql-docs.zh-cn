---
title: sys.dm_pdw_sql_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bca9930ef51de28c8059223c93ea0bb2651f971d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089148"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  在查询中包含有关所有 SQL Server 查询分布作为 SQL 步骤的一部分的信息。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 查询分发所属的查询的唯一标识符。<br /><br /> request_id、 step_index 和 distribution_id 构成此视图的键。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此分布是一部分的查询步骤的索引。<br /><br /> request_id、 step_index 和 distribution_id 构成此视图的键。|请参阅中的 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|pdw_node_id|**int**|在其运行此查询分布的节点的唯一标识符。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**int**|在其运行此查询分布的分布的唯一标识符。<br /><br /> request_id、 step_index 和 distribution_id 构成此视图的键。|请参阅中的 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。 将设置为-1 表示运行在节点范围内，不分发范围的请求。|  
|status|**nvarchar(32)**|查询分发的当前状态。|挂起、 失败、 已取消、 完成运行，中止 CancelSubmitted|  
|error_id|**nvarchar(36)**|与此查询分布，情况下，如果任何关联的错误的唯一标识符。|请参阅中的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未发生错误，则设置为 NULL。|  
|start_time|**datetime**|查询分发已开始执行的时间。|此查询分配较小或等于当前时间和大于或等于的查询步骤的 start_time 属于|  
|end_time|**datetime**|此查询分发一次完成执行，不取消，或者失败的时间。|大于或等于开始时间，或如果查询分布是正在进行或排入队列设置为 NULL。|  
|total_elapsed_time|**int**|表示查询分发已运行，以毫秒为单位的时间。|大于或等于 0。 等于增量 start_time 和 end_time 完成，失败或已取消查询分发版。<br /><br /> 如果 total_elapsed_time 超出整数的最大值，将持续 total_elapsed_time 可最大值。 这种情况会生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|row_count|**bigint**|更改或此查询分布读取的行数。|对于不更改或不返回数据，如 CREATE TABLE 和 DROP TABLE 操作为-1。|  
|spid|**int**|运行查询分发版的 SQL Server 实例上的会话 id。||  
|command|**nvarchar(4000)**|此查询分发的命令的完整文本。|任何有效的查询或请求字符串。|  
  
 此视图按保留的最大行有关的信息，请参阅中的元数据部分[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
