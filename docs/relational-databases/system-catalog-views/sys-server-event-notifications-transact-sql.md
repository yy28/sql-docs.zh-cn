---
title: sys.server_event_notifications (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b985d915d3d7bb6b3130ccb63a400f314fa05a38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62860904"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个服务器级事件通知对象返回一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|服务器事件通知名称。 在所有服务器级事件通知中是唯一的。|  
|**object_id**|**int**|对象标识号。 在中是唯一**主**数据库。|  
|**parent_class**|**tinyint**|父级的类。 始终为 100 = Server。|  
|**parent_class_desc**|**nvarchar(60)**|父类的说明。 始终为 SERVER。|  
|**parent_id**|**int**|是始终为 0。|  
|**create_date**|**datetime**|创建日期。|  
|**modify_date**|**datetime**|上次使用 ALTER 语句修改对象的日期。|  
|service_name|**nvarchar(256)**|向其发送通知的目标服务的名称。|  
|**broker_instance**|**nvarchar(128)**|定义命名目标服务的 service broker。|  
|**creator_sid**|**varbinary(85)**|执行事件通知创建语句的登录名的 SID。 如果在事件通知定义中未指定 WITH FAN_IN，则为 NULL。|  
|**principal_id**|**int**|拥有此对象的服务器主体的 ID。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
