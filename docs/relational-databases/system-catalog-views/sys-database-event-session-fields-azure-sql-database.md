---
description: sys.database_event_session_fields（Azure SQL 数据库）
title: database_event_session_fields (Azure SQL 数据库) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04479cb0def838e87c472bf17cffc282af298ee7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537405"
---
# <a name="sysdatabase_event_session_fields-azure-sql-database"></a>sys.database_event_session_fields（Azure SQL 数据库）
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  对在事件和目标上显式设置的每个可自定义列都返回一行。  
  
||  
|-|  
|**适用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|object_id|**int**|此字段所关联的对象的 ID。 不可为 null。|  
|name|**sysname**|字段的名称。 不可为 null。|  
|值|**sql_variant**|字段的值。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
| From | 到 | 关系 |
| ---- | -- | ------------ |
|sys. database_event_session_actions event_session_id|sys. database_event_sessions event_session_id|多对一|  
|sys. database_event_session_actions event_id<br /><br /> sys. database_event_session_actions object_id<br /><br /> sys. database_event_session_actions event_session_id|sys. database_event_session_events event_session_id<br /><br /> sys. database_event_session_events event_id|多对一|  
|sys. database_event_session_actions event_session_id<br /><br /> sys. database_event_session_actions object_id|sys. database_event_session_targets event_session_id<br /><br /> sys. database_event_session_targets target_id|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
