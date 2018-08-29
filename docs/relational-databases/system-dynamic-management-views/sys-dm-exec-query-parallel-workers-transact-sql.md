---
title: sys.dm_exec_query_parallel_workers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 1
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b59c1d1efb2343c8f7ff591278457bbde6ea31e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074459"
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  返回每个节点的辅助角色可用性信息。  
  
|“属性”|数据类型|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 节点 id。|  
|**scheduler_count**|**int**|此节点上的计划程序数。|  
|**max_worker_count**|**int**|用于并行查询的工作线程的最大数目。|  
|**reserved_worker_count**|**int**|保留的并行查询的工作线程数加上的所有请求都使用的主工作线程数。| 
|**free_worker_count**|**int**|适用于任务的工作线程数。<br /><br />**注意：** 每个传入请求会占用最少 1 辅助角色，即从可用的辅助角色数中减去。  就可以免费的辅助进程计数可以是负数负载很重的服务器上。| 
|**used_worker_count**|**int**|并行查询使用的工作线程数。|  
  
## <a name="permissions"></a>Permissions  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
 
## <a name="examples"></a>示例  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. 查看当前并行辅助角色可用性  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
