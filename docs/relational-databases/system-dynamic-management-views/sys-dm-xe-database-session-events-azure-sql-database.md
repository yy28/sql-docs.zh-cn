---
title: sys.dm_xe_database_session_events （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6ba6b7613dbda16831502ad8030f1b0a0a065370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045826"
---
# <a name="sysdmxedatabasesessionevents-azure-sql-database"></a>sys.dm_xe_database_session_events（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关会话事件的信息。 事件是离散执行点。 如果事件不包含所需的信息，则可对事件应用谓词以阻止其激发。  
  
||  
|-|  
|**适用对象**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 不可为 null。|  
|event_name|**nvarchar(60)**|操作绑定到的事件的名称。 不可为 null。|  
|event_package_guid|**uniqueidentifier**|包含事件的包的 GUID。 不可为 null。|  
|event_predicate|**nvarchar(2048)**|应用于事件的谓词树的 XML 表示形式。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|若要|关系|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|多对一|  
|sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name、sys.dm_xe_objects.package_guid|多对一|  
  
  
