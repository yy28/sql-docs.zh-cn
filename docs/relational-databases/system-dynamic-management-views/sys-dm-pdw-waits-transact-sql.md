---
title: sys.dm_pdw_waits (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 476b2f251bd41480962eb9925af6e3619507e791
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088748"
---
# <a name="sysdmpdwwaits-transact-sql"></a>sys.dm_pdw_waits (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存所有信息都等待请求的执行过程中遇到的状态或查询，其中包括锁等待传输队列中，依次类推。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|与等待状态相关联的唯一数字 id。<br /><br /> 此视图的键。|跨系统中的所有等待是唯一的。|  
|session_id|**nvarchar(32)**|在其发生的等待状态的会话 ID。|请参阅中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|type|**nvarchar(255)**|等待此条目表示的类型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|等待受影响的对象的类型。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**nvarchar(386)**|名称或 GUID 指定等待受影响的对象。||  
|request_id|**nvarchar(32)**|在其发生的等待状态的请求 ID。|请参阅中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|request_time|**datetime**|在该请求的等待状态的时间。||  
|acquire_time|**datetime**|获取的锁或资源的时间。||  
|state|**nvarchar(50)**|等待状态的状态。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|等待项的优先级。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
