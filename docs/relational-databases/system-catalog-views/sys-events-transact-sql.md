---
title: sys.events (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 95cc7112d42a0e2975d886dc8cfa58dc6d7193d3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  导致触发器或事件通知激发的每个事件对应一行。 这些事件表示将触发器或事件通知通过使用创建时指定的事件类型[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)或[CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|触发器或事件通知的 ID。 此值，与一起**类型**唯一地标识一行。|  
|**类型**|**int**|导致触发器激发的事件。|  
|**type_desc**|**nvarchar(60)**|导致触发器激发的事件的说明。|  
|**is_trigger_event**|**bit**|1 = 触发器事件。<br /><br /> 0 = 通知事件。|  
|**event_group_type**|**int**|要对其创建触发器或事件通知的事件组，如果未对事件组中创建触发器或事件通知，则为 Null。|  
|**event_group_type_desc**|**nvarchar(60)**|创建触发器或事件通知的事件组的说明，如果未在事件组中创建触发器或事件通知，则为 Null。|  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
