---
title: sys. dm_xe_session_event_actions （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e50688acee036511d102247d4bff9b8d9a4df84b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898573"
---
# <a name="sysdm_xe_session_event_actions-transact-sql"></a>sys.dm_xe_session_event_actions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回有关事件会话操作的信息。 激发事件时将执行操作。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|action_name|**nvarchar(256)**|操作的名称。 不可为 null。|  
|action_package_guid|**uniqueidentifier**|包含操作的包的 GUID。 不可为 null。|  
|event_name|**nvarchar(256)**|操作绑定到的事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含事件的包的 GUID。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|功能|关系|  
|----------|--------|------------------|  
|sys.dm_xe_session_event_actions.event_session_address|sys.dm_xe_sessions.address|多对一|  
|sys. dm_xe_session_event_actions action_name，<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_session_events.event_package_guid|多对一|  
|sys. dm_xe_session_event_actions event_name，<br /><br /> sys.dm_xe_session_event_actions.event_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

