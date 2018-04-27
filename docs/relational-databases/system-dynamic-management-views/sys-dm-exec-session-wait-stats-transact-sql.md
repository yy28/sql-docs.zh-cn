---
title: sys.dm_exec_session_wait_stats (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bd87b3a99f965d60c4d02f2149a1fe33cbf9e5b9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>sys.dm_exec_session_wait_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回有关遇到的每个会话中执行的线程的所有等待的信息。 您可以使用此视图来诊断性能问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会话和也与特定查询和批处理。  此视图返回会话为聚合的相同信息[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)但提供**session_id**以及数。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|会话的 id。|  
|wait_type|**nvarchar(60)**|等待类型的名称。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
|waiting_tasks_count|**bigint**|该等待类型的等待数。 该计数器在每开始一个等待时便会增加。|  
|wait_time_ms|**bigint**|该等待类型的总等待时间（毫秒）。 该时间包括 signal_wait_time_ms。|  
|max_wait_time_ms|**bigint**|该等待类型的最长等待时间。|  
|signal_wait_time_ms|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。|  
  
## <a name="remarks"></a>注释  
 当打开会话时，或重置会话时，此 DMV 重置会话的信息 (如果连接池)，  
  
 有关的等待类型的信息，请参阅[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 如果用户具有**VIEW SERVER STATE**服务器上的权限，用户将看到执行的所有会话的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 否则为用户将看到的只对当前会话。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
