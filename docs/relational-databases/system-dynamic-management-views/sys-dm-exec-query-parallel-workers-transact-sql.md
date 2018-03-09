---
title: "sys.dm_exec_query_parallel_workers (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: 
author: pelopes
ms.author: pelopes
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 99165e38dc4f1ad0b25a754f2c0f38b4ae413e84
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2018
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  返回每个节点的辅助可用性信息。  
  
|名称|数据类型|Description|  
|----------|---------------|-----------------|  
|**通过 node_id**|**int**|NUMA 节点 id。|  
|**scheduler_count**|**int**|在此节点上的计划程序数。|  
|**max_worker_count**|**int**|最大并行查询的辅助进程数。|  
|**reserved_worker_count**|**int**|并行查询保留的辅助进程数加上的所有请求都使用的主辅助进程数。| 
|**free_worker_count**|**int**|可用于任务的辅助进程数。<br /><br />**注意：**每个传入请求消耗减去可用辅助进程计数的至少一个辅助进程。  很可能可用的工作线程数，可以是负数负载较重的服务器上。| 
|**used_worker_count**|**int**|使用并行查询的辅助进程数。|  
  
## <a name="permissions"></a>权限  
 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要服务器上的 VIEW SERVER STATE 权限。  
  
 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要 VIEW DATABASE STATE 权限的数据库中。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。  
  
## <a name="examples"></a>示例  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. 查看当前并行工作进程的可用性  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
