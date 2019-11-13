---
title: sys. dm_exec_session_wait_stats （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 6fc51bec78cf01522e6731648bdb7870ea7d9fb0
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982609"
---
# <a name="sysdm_exec_session_wait_stats-transact-sql"></a>sys. dm_exec_session_wait_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回有关对每个会话执行的线程所遇到的所有等待的信息。 您可以使用此视图诊断 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话的性能问题以及特定查询和批处理。  此视图返回的会话与为[sys. dm_os_wait_stats &#40;&#41; transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)聚合的信息相同，但也提供**session_id**号。  
  
**适用**于： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和更高版本）。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**int**|会话的 id。|  
|wait_type|**nvarchar(60)**|等待类型的名称。 有关详细信息，请参阅 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
|waiting_tasks_count|**bigint**|该等待类型的等待数。 该计数器在每开始一个等待时便会增加。|  
|wait_time_ms|**bigint**|该等待类型的总等待时间（毫秒）。 该时间包括 signal_wait_time_ms。|  
|max_wait_time_ms|**bigint**|该等待类型的最长等待时间。|  
|signal_wait_time_ms|**bigint**|正在等待的线程从收到信号通知到其开始运行之间的时差。|  
  
## <a name="remarks"></a>Remarks  
 此 DMV 会在会话打开时重置会话的信息，或者当会话重置时（如果连接池），  
  
 有关等待类型的信息，请参阅[sys. dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 如果用户对服务器具有**VIEW SERVER STATE**权限，则用户将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例上看到所有正在执行的会话;否则，用户将只看到当前会话。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与操作系统相关的&#40;&#41;动态管理视图 SQL Server transact-sql](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
