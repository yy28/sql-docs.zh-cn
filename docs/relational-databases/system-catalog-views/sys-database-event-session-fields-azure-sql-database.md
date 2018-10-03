---
title: sys.database_event_session_fields （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7874cb88d70aae5a843475f2adf4946730aed1b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717952"
---
# <a name="sysdatabaseeventsessionfields-azure-sql-database"></a>sys.database_event_session_fields（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  对在事件和目标上显式设置的每个可自定义列都返回一行。  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|object_id|**int**|此字段所关联的对象的 ID。 不可为 null。|  
|NAME|**sysname**|字段的名称。 不可为 null。|  
|值|**sql_variant**|字段的值。 不可为 null。|  
  
## <a name="permissions"></a>Permissions  
 要求对服务器具有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
||||  
|-|-|-|  
|From|若要|关系|  
|sys.database_event_session_actions.event_session_id|sys.database_event_sessions.event_session_id|多对一|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.object_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|多对一|  
|sys.database_event_session_actions.event_session_id<br /><br /> sys.database_event_session_actions.object_id|sys.database_event_session_targets.event_session_id<br /><br /> sys.database_event_session_targets.target_id|多对一|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
