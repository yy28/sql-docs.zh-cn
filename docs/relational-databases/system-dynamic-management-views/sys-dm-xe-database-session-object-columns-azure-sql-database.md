---
title: sys.dm_xe_database_session_object_columns （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b37ced9ef4de7217b4c7ba3564898c6de2800fb5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824016"
---
# <a name="sysdmxedatabasesessionobjectcolumns-azure-sql-database"></a>sys.dm_xe_database_session_object_columns（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  显示绑定到会话的对象的配置值。  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 具有与 sys.dm_xe_database_sessions.address 的多对一关系。 不可为 null。|  
|column_name|**nvarchar(60)**|配置值的名称。 不可为 null。|  
|column_id|**int**|列的 ID。 在对象中是唯一的。 不可为 null。|  
|column_value|**nvarchar(2048)**|列的配置值。 可以为 Null。|  
|object_type|**nvarchar(60)**|对象的类型。  不是 nullable.object_type 是之一：<br /><br /> 事件<br /><br /> target|  
|object_name|**nvarchar(60)**|此列所属对象的名称。 不可为 null。|  
|object_package_guid|**uniqueidentifier**|包含该对象的包的 GUID。 不可为 null。|  
  
## <a name="permissions"></a>Permissions  
 要求拥有 VIEW DATABASE STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns.object_name<br /><br /> dm_xe_database_session_object_columns.object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多对一|  
|dm_xe_database_session_object_columns.column_name<br /><br /> dm_xe_database_session_object_columns.column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|多对一|  
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
