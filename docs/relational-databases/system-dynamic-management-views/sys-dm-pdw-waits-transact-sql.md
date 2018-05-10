---
title: sys.dm_pdw_waits (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b78d2aa75718669c19ea2b01ceb7123580596921
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwwaits-transact-sql"></a>sys.dm_pdw_waits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含所有相关信息等待状态的请求的执行过程中遇到或查询，包括锁将一直等待传输队列中，依次类推。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|与等待状态相关联的唯一数字 id。<br /><br /> 此视图的键。|跨系统中的所有等待唯一。|  
|session_id|**nvarchar(32)**|在其发生等待状态的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|type|**nvarchar(255)**|等待此条目表示的类型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|通过在等待受影响的对象类型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**nvarchar(386)**|名称或 GUID 指定等待受影响的对象。||  
|request_id|**nvarchar(32)**|在其发生等待状态的请求的 ID。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|request_time|**datetime**|从该处请求等待状态的时间。||  
|acquire_time|**datetime**|获取锁或资源的时间。||  
|state|**nvarchar(50)**|等待状态的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待项的优先级。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_wait_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
