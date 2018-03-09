---
title: sys.dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d80848491c46046ba260956fb02ce41e7becdd6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对计划异步（后台）执行的每个查询处理器作业返回一行。  
  
> **注意！！** 若要从我们称之为 **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** 或 **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** ，使用名称**sys.dm_pdw_nodes_exec_background_job_queue**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|作业添加到队列中的时间。|  
|**job_id**|**int**|作业标识符。|  
|**database_id**|**int**|执行作业所在的数据库。|  
|**object_id1**|**int**|值取决于作业类型。 有关详细信息，请参见“备注”部分。|  
|**object_id2**|**int**|值取决于作业类型。 有关详细信息，请参见“备注”部分。|  
|**object_id3**|**int**|值取决于作业类型。 有关详细信息，请参见“备注”部分。|  
|**object_id4**|**int**|值取决于作业类型。 有关详细信息，请参见“备注”部分。|  
|**error_code**|**int**|如果因失败而重新插入作业，则为错误代码。 如果作业已挂起、未被选取或已完成，则为 NULL。|  
|**request_type**|**int**|作业请求的类型。|  
|**retry_count**|**int**|从队列中选取作业又因缺少资源或其他原因而将其重新插入队列的次数。|  
|**in_progress**|**int**|指示作业是否已开始执行。<br /><br /> 1 = 已开始<br /><br /> 0 = 仍在等待|  
|**session_id**|**int**|会话标识符。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限  
 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要服务器上的 VIEW SERVER STATE 权限。  
  
 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]高级层需要 VIEW DATABASE STATE 权限的数据库中。 上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]标准版和基本层需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]管理员帐户。  
  
## <a name="remarks"></a>注释  
 该视图只返回有关异步更新统计作业的信息。 有关异步更新统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。  
  
 值**object_id1**通过**object_id4**取决于作业请求的类型。 下表总结了这些列对于不同作业类型的含义。  
  
|请求类型|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|异步更新统计信息|表或视图的 ID|统计信息 ID|未使用|未使用|  
  
## <a name="examples"></a>示例  
 以下示例为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的每个数据库返回后台队列中活动异步作业的数量。  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [统计信息](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact SQL &#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



