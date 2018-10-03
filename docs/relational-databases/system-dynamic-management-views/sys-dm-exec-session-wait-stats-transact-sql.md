---
title: sys.dm_exec_session_wait_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d99f844a83ee112dbd66f6e4c2110035d70658a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681125"
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>sys.dm_exec_session_wait_stats (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回有关线程所执行的每个会话遇到的所有等待的信息。 可以使用此视图来诊断性能问题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会话和特定查询和批处理。  此视图返回会话相同的聚合的信息[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)提供，但**session_id**数量和。  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|会话的 id。|  
|wait_type|**nvarchar(60)**|等待类型的名称。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
|waiting_tasks_count|**bigint**|该等待类型的等待数。 该计数器在每开始一个等待时便会增加。|  
|wait_time_ms|**bigint**|该等待类型的总等待时间（毫秒）。 该时间包括 signal_wait_time_ms。|  
|max_wait_time_ms|**bigint**|该等待类型的最长等待时间。|  
|signal_wait_time_ms|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。|  
  
## <a name="remarks"></a>备注  
 当打开会话时，或重置会话时，此 DMV 重置会话的信息 (如果连接池)，  
  
 有关等待类型的信息，请参阅[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 如果用户具有**VIEW SERVER STATE**服务器上的权限，用户会执行的所有会话的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 否则为用户会看到仅为当前会话。  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
