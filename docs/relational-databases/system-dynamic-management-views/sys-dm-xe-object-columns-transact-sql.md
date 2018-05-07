---
title: sys.dm_xe_object_columns (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_object_columns
- sys.dm_xe_object_columns_TSQL
- dm_xe_object_columns_TSQL
- dm_xe_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_object_columns dynamic management view
- extended events [SQL Server], views
ms.assetid: d96a14f3-4284-45ff-b1fe-4858e540a013
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b751ef75af9fd9ec246410d51cb483297144886
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmxeobjectcolumns-transact-sql"></a>sys.dm_xe_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回所有对象的架构信息。  
  
> [!NOTE]  
>  事件对象可为只读数据和读写数据公开固定架构。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|列的名称。 名称是在对象中是唯一的。 不可为 null。|  
|column_id|**int**|列的标识符。 column_id 内是唯一的对象与 column_type 一起使用时。 不可为 null。|  
|object_name|**nvarchar(60)**|此列所属对象的名称。 与 sys.dm_xe_objects.id 存在多对一的关系。不可为 null。|  
|object_package_guid|**uniqueidentifier**|包含该对象的包的 GUID。 不可为 null。|  
|type_name|**nvarchar(60)**|此列的类型名称。 不可为 null。|  
|type_package_guid|**uniqueidentifier**|包含列数据类型的包的 GUID。 不可为 null。|  
|column_type|**nvarchar(60)**|指示如何使用此列。 不可为 null。 column_type 可以是以下项之一：<br /><br /> readonly。 该列包含不能被更改的静态值。<br /><br /> data。 该列可包含由对象公开的运行时数据。<br /><br /> customizable。 该列包含可以被更改的值。<br /><br /> 注意： 如果更改此值，则可以修改对象的行为。|  
|column_value|**nvarchar(256)**|显示与对象列关联的静态值。 可以为 Null。|  
|capabilities|**int**|一个描述列的功能的位图。 可以为 Null。|  
|capabilities_desc|**nvarchar(256)**|此对象列的功能的说明。 此值可以为下列值之一：<br /><br /> Mandatory。 将父对象绑定到一个事件会话时必须设置该值。<br /><br /> NULL|  
|description|**nvarchar(256)**|此对象列的说明。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|sys.dm_xe_object_columns.object_name、sys.dm_xe_object_columns.object_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_objects.package_guid|多对一|  
|sys.dm_xe_object_columns.type_name<br /><br /> sys.dm_xe_object_columns.type_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

