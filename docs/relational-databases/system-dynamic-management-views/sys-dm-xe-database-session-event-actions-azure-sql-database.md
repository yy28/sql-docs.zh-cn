---
title: sys.dm_xe_database_session_event_actions （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 48519fd9-c7c2-434b-848d-ccbf41133fdd
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 40587866b77e67947a1658c742ceed9f9e71b581
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090437"
---
# <a name="sysdmxedatabasesessioneventactions-azure-sql-database"></a>sys.dm_xe_database_session_event_actions（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关事件会话操作的信息。 激发事件时将执行操作。 此管理视图聚合了有关操作已经执行的次数及操作的总执行时间的统计信息。  
  
||  
|-|  
|**适用对象**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和所有将来的版本。|  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|action_name|**nvarchar(60)**|操作的名称。 不可为 null。|  
|action_package_guid|**uniqueidentifier**|包含操作的包的 GUID。 不可为 null。|  
|event_name|**nvarchar(60)**|操作绑定到该事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含该事件的包 GUID。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|若要|关系|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_event_actions.event_session_address|sys.dm_xe_database_sessions.address|多对一|  
|sys.dm_xe_database_session_event_actions.action_name<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_database_session_events.event_package_guid|多对一|  
|sys.dm_xe_database_session_event_actions.event_name<br /><br /> sys.dm_xe_database_session_event_actions.event_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
