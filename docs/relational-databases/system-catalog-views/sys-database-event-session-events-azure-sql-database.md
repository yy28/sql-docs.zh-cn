---
title: sys.database_event_session_events （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0e3d1035488696697d2f717e888806fb352b187
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707205"
---
# <a name="sysdatabaseeventsessionevents-azure-sql-database"></a>sys.database_event_session_events（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  对事件会话中的每个事件都返回一行。  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|event_id|**int**|事件的 ID。 此 ID 是在事件会话对象中是唯一的。 不可为 null。|  
|NAME|**sysname**|事件的名称。 不可为 null。|  
|包|**sysname**|包含事件的事件包的名称。 不可为 null。|  
|module|**sysname**|包含事件的模块的名称。 不可为 null。|  
|predicate|**nvarchar(3000)**|应用于事件的谓词表达式。 可以为 Null。|  
|predicate_xml|**nvarchar(3000)**|应用于事件的 XML 谓词表达式。 可以为 Null。|  
  
## <a name="permissions"></a>Permissions  
 要求对服务器具有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
||||  
|-|-|-|  
|From|若要|关系|  
|sys.database_event_session_events.event_session_id|sys.database_event_sessions.event_session_id|多对一|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
