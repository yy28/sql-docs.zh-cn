---
title: sys.dm_exec_query_optimizer_memory_gateways (Transact SQL) |Microsoft 文档
description: 返回用于限制并发查询优化的资源信号量的当前状态
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b9d36c4a67fab2f9f7c867a3ba6b7e7d01fc5d29
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34468063"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

返回用于限制并发查询优化的资源信号量的当前状态。

|列|类型|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|资源池 ID 在资源调控器|  
|**名称**|**sysname**|编译入口名称 （小网关，中型网关，大型网关）|
|**max_count**|**int**|并发编译最大配置的计数|
|**active_count**|**int**|在此入口的编译的当前活动计数|
|**waiter_count**|**int**|此入口在等待程序数|
|**threshold_factor**|**bigint**|阈值因子，用于定义由查询优化的最大内存部分。  对于小网关，threshold_factor 指示以字节为单位为一个查询的最大优化器内存使用率之前需要访问在小的网关。  对于中型和大型网关，threshold_factor 显示可用于此入口的服务器总内存的部分。 计算入口内存使用情况阈值时，它用作除数。|
|**threshold**|**bigint**|以字节为单位的下一步阈值内存。  查询需要获得对此网关的访问权限，如果它的内存消耗达到此阈值。  "-1"如果查询不需要获得对此网关的访问权限。|
|**is_active**|**bit**|是否查询还需要或不通过当前入口。|


## <a name="permissions"></a>权限  
SQL Server 需要服务器上的 VIEW SERVER STATE 权限。

Azure SQL 数据库需要 VIEW DATABASE STATE 权限的数据库中。


## <a name="remarks"></a>注释  
SQL Server 使用一种分层的网关方法来限制允许的并发编译数。  使用三个网关时，包括小、 中和大型。 网关帮助防止由更大的编译内存要求使用者的总体内存资源耗尽。

等待网关导致延迟的编译。 除了在编译的延迟，中止的请求将具有等待类型累积关联的 RESOURCE_SEMAPHORE_QUERY_COMPILE。 RESOURCE_SEMAPHORE_QUERY_COMPILE 等待类型可能表示查询正在编译的使用大量的内存和已耗尽内存，或者没有足够的内存可用的总体上而言，在特定的但是可用单元网关都已用完。 输出**sys.dm_exec_query_optimizer_memory_gateways**可用于诊断的情况时内存不足，无法编译查询执行计划的位置。  

## <a name="examples"></a>示例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 在资源信号量上查看统计信息  
SQL Server 的此实例的当前优化器内存网关统计信息有哪些？

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](./system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[如何使用 DBCC MEMORYSTATUS 命令来监视 SQL Server 2005 上的内存使用情况](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[大型查询编译上 SQL Server 2014 中 RESOURCE_SEMAPHORE_QUERY_COMPILE 等待](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
