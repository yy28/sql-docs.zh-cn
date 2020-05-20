---
title: sys. dm_xe_session_object_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_object_columns_TSQL
- sys.dm_xe_session_object_columns_TSQL
- dm_xe_session_object_columns
- sys.dm_xe_session_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- xe
- sys.dm_xe_session_object_columns dynamic management view
ms.assetid: e97f3307-2da6-4c54-b818-a474faec752e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 980aa0c4c7d82fcf7b58d88fd6e9f068627d9dca
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829032"
---
# <a name="sysdm_xe_session_object_columns-transact-sql"></a>sys.dm_xe_session_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示绑定到会话的对象的配置值。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 与 sys.dm_xe_sessions.address 之间具有多对一关系。 不可为 null。|  
|column_name|**nvarchar(256)**|配置值的名称。 不可为 null。|  
|column_id|**int**|列的 ID。 在对象中是唯一的。 不可为 null。|  
|column_value|**nvarchar （3072）**|列的配置值。 可以为 Null。|  
|object_type|**nvarchar(60)**|对象的类型。 不可为 null。 object_type 是以下其中之一：<br /><br /> event<br /><br /> 目标|  
|object_name|**nvarchar(256)**|此列所属对象的名称。 不可为 null。|  
|object_package_guid|**uniqueidentifier**|包含该对象的包的 GUID。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|功能|关系|  
|----------|--------|------------------|  
|dm_xe_session_object_columns. object_name，<br /><br /> dm_xe_session_object_columns.object_package_guid|sys. dm_xe_objects package_guid，<br /><br /> sys.dm_xe_objects.name|多对一|  
|dm_xe_session_object_columns. column_name，<br /><br /> dm_xe_session_object_columns.column_id|sys.databases. dm_xe_object_columns，<br /><br /> sys.dm_xe_object_columns.column_id|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

