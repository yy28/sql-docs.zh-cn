---
title: sys. database_event_session_targets （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 741883623a50b14ffdba8045559a2683c7ca3c67
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785040"
---
# <a name="sysdatabase_event_session_targets-azure-sql-database"></a>sys.database_event_session_targets（Azure SQL 数据库）
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

  返回事件会话的每个事件目标所对应的行。  
  
||  
|-|  
|**适用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更高版本。|  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件会话的 ID。 不可为 null。|  
|target_id|**int**|目标的 ID。 ID 在事件会话对象中是唯一的。 不可为 null。|  
|name|**sysname**|事件目标的名称。 不可为 null。|  
|包|**sysname**|包含事件目标的事件包的名称。 不可为 null。|  
|name|**sysname**|包含事件目标的模块的名称。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>备注  
 此视图具有下列关系基数。  
  
||||  
|-|-|-|  
|From|功能|关系|  
|sys. database_event_session_targets event_session_id|sys. database_event_sessions event_session_id|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
