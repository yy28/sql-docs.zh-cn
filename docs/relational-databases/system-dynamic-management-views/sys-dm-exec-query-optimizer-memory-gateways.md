---
title: sys.dm_exec_query_optimizer_memory_gateways (TRANSACT-SQL) |Microsoft Docs
description: 返回用来限制并发查询优化的资源信号量的当前状态
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005709"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

返回用来限制并发查询优化的资源信号量的当前状态。

|“列”|类型|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|资源池 ID 在资源调控器|  
|**名称**|**sysname**|编译入口名称 （小型网关，中型网关，大型网关）|
|**max_count**|**int**|并发编译的最大配置的计数|
|**active_count**|**int**|在此入口中编译的当前处于活动状态计数|
|**waiter_count**|**int**|此入口在等待者数|
|**threshold_factor**|**bigint**|用于定义由查询优化的最大内存部分阈值因子。  对于小型网关，threshold_factor 指示以字节为单位的一个查询的最大的优化器内存使用率，需要访问在小型网关之前。  对于中等和大型网关，threshold_factor 显示可用于此入口的总服务器内存的部分。 计算入口的内存使用情况阈值时，它用作除数。|
|**threshold**|**bigint**|以字节为单位的阈值内存下一步。  查询需要获得对此网关的访问权限，如果其内存使用量达到此阈值。  "-1"如果查询不需要获得对此网关的访问权限。|
|**is_active**|**bit**|查询是否需要或不传递当前入口。|


## <a name="permissions"></a>权限  
SQL Server 要求在服务器上的 VIEW SERVER STATE 权限。

Azure SQL 数据库需要数据库的 VIEW DATABASE STATE 权限。


## <a name="remarks"></a>Remarks  
SQL Server 使用分层的网关方法来限制允许的并发编译数。  使用三个网关时，包括小型、 中型和大型。 网关来帮助防止通过更大的编译内存要求使用者的总体内存资源耗尽。

等待延迟的编译中对网关的结果。 在编译中的延迟，除了限制的请求将具有等待类型累积关联的 RESOURCE_SEMAPHORE_QUERY_COMPILE。 RESOURCE_SEMAPHORE_QUERY_COMPILE 等待类型可能指示查询正在编译使用大量的内存和内存已用尽，或者没有足够的内存可用总体而言，在特定的但是可用单位网关都已用完。 输出**sys.dm_exec_query_optimizer_memory_gateways**可用于诊断情况的出现内存不足，无法编译查询执行计划。  

## <a name="examples"></a>示例  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. 资源信号量上查看统计信息  
为此 SQL Server 实例的当前优化器内存网关统计信息有哪些？

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](./system-dynamic-management-views.md)   
 [与执行相关的动态管理视图和函数 (Transact-SQL)](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[如何使用 DBCC MEMORYSTATUS 命令监视 SQL Server 2005 上的内存使用情况](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[大型查询编译在 SQL Server 2014 中 RESOURCE_SEMAPHORE_QUERY_COMPILE 上等待](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
