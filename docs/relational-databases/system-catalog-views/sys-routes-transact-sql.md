---
title: sys.routes (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 89fb63380c95e38f97f02b24eb68c178182b873a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220058"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  在目录视图中，每个路由对应一行。 Service Broker 使用路由定位服务的网络地址。   

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|路由名称，在数据库中唯一。 不可为 NULL。|  
|**route_id**|**int**|路由的标识符。 不可为 NULL。|  
|**principal_id**|**int**|拥有路由的数据库主体的标识符。 可以为 NULL。|  
|**remote_service_name**|**nvarchar(256)**|远程服务的名称。 可以为 NULL。|  
|**broker_instance**|**nvarchar(128)**|承载远程服务的 Broker 的标识符。 可以为 NULL。|  
|**lifetime**|**datetime**|日期和路由的到期的时间。 注意，该值不使用本地时区， 而是显示 UTC 的过期时间。 可以为 NULL。|  
|**address**|**nvarchar(256)**|Service Broker 将远程服务的消息发送到的网络地址。 可以为 NULL。 对于 SQL 数据库托管实例，地址必须是本地。|  
|**mirror_address**|**nvarchar(256)**|在地址中指定的服务器镜像伙伴的网络地址。 可以为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
