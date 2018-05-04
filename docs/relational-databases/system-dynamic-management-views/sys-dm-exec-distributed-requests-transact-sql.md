---
title: sys.dm_exec_distributed_requests (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b2a8da4e2bb2da05e13b8c603653a5401aeb1c2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  有关所有请求的信息包含当前或最近 active PolyBase 查询中。 它列出每个请求/查询的一行。  
  
 基于会话和请求 ID，用户可以然后检索生成要执行 – 通过 sys.dm_exec_distributed_requests 实际分布式的请求。 例如，涉及常规 SQL 和外部的 SQL 表的查询将分解为跨各种的计算节点执行的各种语句/请求。 若要跟踪的分布式的步骤，在所有计算节点，我们引入 'global' 执行 ID 可以用于跟踪分别与一个特定的请求和运算符，相关联的计算节点上的所有操作。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|此视图的键。 与请求关联的唯一数字 id。|唯一跨系统中的所有请求。|  
|execution_id|**nvarchar(32**|与在其中运行此查询会话相关联的唯一数字 id。||  
|status|**nvarchar(32**|请求的当前状态。|挂起，授权，AcquireSystemResources，初始化、 计划，分析，AquireResources，正在运行、 取消，完整，已失败，取消。|  
|error_id|**nvarchar(36)**|如果有与此请求相关联的错误的唯一 id。|如果未发生错误，则设置为 NULL。|  
|start_time|**datetime**|请求执行开始时间。|0 表示排队请求;否则为有效日期时间小于或等于当前时间。|  
|end_time|**datetime**|引擎完成编译请求的时间。|对于排队或活动的请求; 为 null否则为有效日期时间小于或等于当前时间。|  
|total_elapsed_time|**int**|自启动请求，以毫秒为单位，在执行过程中已用时间。|之间 0 和 start_time 和 end_time 之间的差异。如果 total_elapsed_time 超过一个整数的最大值，total_elapsed_time 将继续是最大值。 这种情况将生成警告"的最大值已超出。" 以毫秒为单位的最大值相当于 24.8 天。|  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
