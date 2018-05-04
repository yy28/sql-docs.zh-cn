---
title: sys.dm_exec_query_resource_semaphores (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dca59c6557e951922fa19ebd95526aab5149b9fd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecqueryresourcesemaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中有关当前查询资源信号量状态的信息。 **sys.dm_exec_query_resource_semaphores**提供常规查询执行内存状态，并允许你以确定系统是否可以访问足够的内存。 此视图进行了补充中获得的内存信息[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)提供全面的服务器内存状态。 **sys.dm_exec_query_resource_semaphores**返回一个行的正则资源信号和小型查询资源信号量的另一行。 有小查询信号量的两个要求：  
  
-   请求的内存授予应小于 5 MB  
  
-   查询成本应小于 3 的成本单位  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_exec_query_resource_semaphores**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**int**|资源信号量的非唯一 ID。 0 表示常规资源信号量，1 表示小型查询资源信号量。|  
|**target_memory_kb**|**bigint**|授予使用的目标 (KB)。|  
|**max_target_memory_kb**|**bigint**|最大潜在目标 (KB)。 对于小型查询资源信号量，该值为 NULL。|  
|**total_memory_kb**|**bigint**|资源信号量所持有的内存 (KB)。 如果系统处于内存压力下，或如果强制最小经常授予内存，则此值可以是大于**target_memory_kb**或**max_target_memory_kb**值。 总内存是可用内存和被授予内存的和。|  
|**available_memory_kb**|**bigint**|可用于新授予的内存 (KB)。|  
|**granted_memory_kb**|**bigint**|授予的总内存 (KB)。|  
|**used_memory_kb**|**bigint**|授予内存中实际使用的部分 (KB)。|  
|**grantee_count**|**int**|内存授予得到满足的活动查询数。|  
|**waiter_count**|**int**|等待内存授予得到满足的查询数。|  
|**timeout_error_count**|**bigint**|自服务器启动以来的超时错误总数。 对于小型查询资源信号量，该值为 NULL。|  
|**forced_grant_count**|**bigint**|自服务器启动以来的强制最小内存授予总数。 对于小型查询资源信号量，该值为 NULL。|  
|**pool_id**|**int**|此资源信号量所属资源池的 ID。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="remarks"></a>注释  
 如果查询使用的动态管理视图中包括 ORDER BY 或聚合，则可能增加内存占用，进而产生需进行故障排除的问题。  
  
 使用**sys.dm_exec_query_resource_semaphores**进行故障排除但不是包含它的应用程序将使用的未来版本中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 数据库管理员可以使用资源调控器功能在多个资源池之间分发服务器资源，最多可为 64 个池。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更高版本中，每个池都类似于一个小型的独立服务器实例并且要求 2 个信号量。  
  
## <a name="see-also"></a>另请参阅  
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


