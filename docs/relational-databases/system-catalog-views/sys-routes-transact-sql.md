---
title: "sys.routes (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e27f943e14ad6ef9340764bbd376d754f43dc26b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在目录视图中，每个路由对应一行。 Service Broker 使用路由定位服务的网络地址。   
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|路由名称，在数据库中唯一。 不可为 NULL。|  
|**route_id**|**int**|路由的标识符。 不可为 NULL。|  
|**principal_id**|**int**|拥有路由的数据库主体的标识符。 可以为 NULL。|  
|**remote_service_name**|**nvarchar(256)**|远程服务的名称。 可以为 NULL。|  
|**broker_instance**|**nvarchar （128)**|承载远程服务的 Broker 的标识符。 可以为 NULL。|  
|**生存期**|**datetime**|日期和路由的到期的时间。 注意，该值不使用本地时区， 而是显示 UTC 的过期时间。 可以为 NULL。|  
|**地址**|**nvarchar(256)**|Service Broker 将远程服务的消息发送到的网络地址。 可以为 NULL。|  
|**mirror_address**|**nvarchar(256)**|在地址中指定的服务器镜像伙伴的网络地址。 可以为 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
