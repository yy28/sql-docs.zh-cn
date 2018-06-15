---
title: sys.dm_pdw_sql_requests (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: aa8d0384eee7ab74c17797c9bd11ac65042d79c5
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467353"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  在查询中包含有关所有 SQL Server 查询分布作为 SQL 步骤的一部分的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 查询分发所属于的查询的唯一标识符。<br /><br /> request_id、 step_index 和 distribution_id 窗体的密钥，此视图。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此分布是的一部分的查询步骤索引。<br /><br /> request_id、 step_index 和 distribution_id 窗体的密钥，此视图。|请参阅中的 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|pdw_node_id|**int**|在其上运行此查询分发的节点的唯一标识符。|请参阅中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**int**|在其上运行此查询分布的分布的唯一标识符。<br /><br /> request_id、 step_index 和 distribution_id 窗体的密钥，此视图。|请参阅中的 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。 设置为-1 的请求的运行在节点范围内，不分发作用域。|  
|status|**nvarchar(32)**|查询分发的当前状态。|挂起状态，运行，失败、 取消、 完成，中止 CancelSubmitted|  
|error_id|**nvarchar(36)**|与此查询分发情况下，如果任何关联的错误的唯一标识符。|请参阅中的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未发生错误，则设置为 NULL。|  
|start_time|**datetime**|在哪个查询分发已开始执行的时间。|此查询分发属于较小或等于当前时间和大于或等于 start_time 查询步骤|  
|end_time|**datetime**|从该处此查询分发完成执行、 已取消，或失败的时间。|大于或等于开始时间，或如果正在进行或已排队的是查询分发设置为 NULL。|  
|total_elapsed_time|**int**|表示查询分发已运行，以毫秒为单位的时间。|大于或等于 0。 等于的增量 start_time 和 end_time 已完成的、 失败或取消查询分发。<br /><br /> 如果 total_elapsed_time 超过一个整数的最大值，total_elapsed_time 将继续是最大值。 这种情况将生成警告"的最大值已超出。"<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|row_count|**bigint**|更改或读取此查询分发的行数。|操作，不会更改或返回数据，例如 CREATE TABLE 和 DROP TABLE-1。|  
|spid|**int**|在运行查询分发的 SQL Server 实例上的会话 id。||  
|command|**nvarchar(4000)**|为此查询分发的命令的完整文本。|任何有效的查询或请求字符串。|  
  
 有关通过此视图保留最大行数的信息，请参阅中的最大的系统视图值部分[最小值和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主题。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
