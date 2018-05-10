---
title: sys.dm_xe_packages (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1be7763fbbf1e2f530d3e9d8530278d461bdfc13
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmxepackages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出向扩展的事件引擎注册的所有包。  
  
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|包的名称。 包自身便可显示说明。 不可为 null。|  
|guid|**uniqueidentifier**|标识包的 GUID。 不可为 null。|  
|description|**nvarchar(256)**|包说明。 descriptionis 由程序包作者设置，并且不可以为 null。|  
|capabilities|**int**|说明此包的功能的位图。 可以为 Null。|  
|capabilities_desc|**nvarchar(256)**|此包可能具有的所有功能的列表。 可以为 Null。|  
|module_guid|**uniqueidentifier**|公开此包的模块的 GUID。 不可为 null。|  
|module_address|**varbinary(8)**|用于加载包含此包的模块的基址。 单个模块可以公开多个包。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>注释  
 向扩展事件引擎注册的包可以公开事件、激发事件时可采取的操作以及事件数据的同步和异步处理目标。  
  
 这些包可以动态加载到进程地址空间中。 包在加载时将向扩展事件引擎注册其公开的所有对象。  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
||||  
|-|-|-|  
|从|若要|关系|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|多对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

