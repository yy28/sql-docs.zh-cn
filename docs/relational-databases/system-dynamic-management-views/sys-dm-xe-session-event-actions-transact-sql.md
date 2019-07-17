---
title: sys.dm_xe_session_event_actions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_event_actions_TSQL
- sys.dm_xe_session_event_actions_TSQL
- dm_xe_session_event_actions
- sys.dm_xe_session_event_actions
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_xe_session_event_actions dynamic management view
ms.assetid: 0c22a546-683e-4c84-ab97-1e9e95304b03
author: stevestein
ms.author: sstein
ms.openlocfilehash: c10ef9265ef659985d667632e864e55f58ef4911
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090254"
---
# <a name="sysdmxesessioneventactions-transact-sql"></a>sys.dm_xe_session_event_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关事件会话操作的信息。 激发事件时将执行操作。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|action_name|**nvarchar(256)**|操作的名称。 不可为 null。|  
|action_package_guid|**uniqueidentifier**|包含操作的包的 GUID。 不可为 null。|  
|event_name|**nvarchar(256)**|操作绑定到该事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含该事件的包 GUID。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|若要|关系|  
|----------|--------|------------------|  
|sys.dm_xe_session_event_actions.event_session_address|sys.dm_xe_sessions.address|多对一|  
|sys.dm_xe_session_event_actions.action_name,<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_session_events.event_package_guid|多对一|  
|sys.dm_xe_session_event_actions.event_name,<br /><br /> sys.dm_xe_session_event_actions.event_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

