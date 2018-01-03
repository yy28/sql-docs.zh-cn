---
title: "DROP EVENT NOTIFICATION (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2ecaff48f54ce76fe0d193eda5406df1bc574e7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从当前数据库中删除事件通知触发器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *notification_name*  
 要删除的事件通知名称。 可以指定多个事件通知。 若要查看当前创建的事件通知的列表，请使用[sys.event_notifications &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 指示应用于当前服务器的事件通知的作用域。 如果在创建事件通知时指定了 SERVER，则必须指定 SERVER。  
  
 DATABASE  
 指示事件通知的作用域是适用于当前数据库。 如果在创建事件通知时指定了 DATABASE，则必须指定 DATABASE。  
  
 队列*queue_name*  
 指示事件通知的作用域是适用于指定的队列*queue_name*。 如果在创建事件通知时指定了 QUEUE，则必须指定 QUEUE。 *queue_name*是队列的名称，还必须指定。  
  
## <a name="remarks"></a>Remarks  
 如果事件通知在事务中激发并在同一事务中删除，则发送事件通知实例，然后删除事件通知。  
  
## <a name="permissions"></a>权限  
 若要删除作用域为数据库级别的事件通知，用户至少必须是事件通知的所有者，或必须在当前数据库中拥有 ALTER ANY DATABASE EVENT NOTIFICATION 权限。  
  
 若要删除作用域为服务器级别的事件通知，用户至少必须是事件通知的所有者，或必须在服务器中拥有 ALTER ANY EVENT NOTIFICATION 权限。  
  
 若要删除针对特定队列的事件通知，用户至少必须是事件通知的所有者或必须对父队列拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
 以下示例创建具有数据库范围内的事件通知，然后删除该通知：  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建事件通知 &#40;Transact SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  
