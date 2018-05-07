---
title: sys.dm_exec_compute_node_errors (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ca01e2b67d4443c1ac1efa03fa86542b46d3de34
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexeccomputenodeerrors-transact-sql"></a>sys.dm_exec_compute_node_errors (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  出现的 PolyBase 的返回错误的计算节点。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|与错误关联的唯一数字 id。|在系统中的所有查询错误唯一|  
|源 (source)|**nvarchar(255)**|源线程或进程说明||  
|type|**nvarchar(255)**|错误类型。||  
|create_time|**datetime**|错误出现的时间||  
|compute_node_id|**int**|特定的计算节点标识符|请参阅的 compute_node_id [sys.dm_exec_compute_nodes &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|**nvarchar(36)**|PolyBase 查询，如果任何标识符。||  
|spid|**int**|SQL Server 会话标识符||  
|thread_id|**int**|发生错误的线程的数字标识符。||  
|详细信息|nvarchar(4000)|错误的详细信息的完整说明。||  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
