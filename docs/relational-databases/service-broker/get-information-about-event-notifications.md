---
title: "获取有关事件通知的信息 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e41d81ae5f32fd8d78e1515f17a9229129348df
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="get-information-about-event-notifications"></a>获取有关事件通知的信息
  下列目录视图可用于查询有关事件通知的元数据。  
  
 **获取有关非服务器级别事件通知的信息**  
  
-   [sys.event_notifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  若要查看 **sys.event_notifications** 中在数据库级别创建的任意事件通知的元数据，至少必须满足下列条件：对数据库具有 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 权限，是事件通知的所有者，或者具有 ALTER ANY DATABASE EVENT NOTIFICATION 权限。 对于对特定队列创建的事件通知，至少必须满足下列条件：对对象具有 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 权限，是事件通知的所有者，或者具有 ALTER ANY DATABASE EVENT NOTIFICATION 权限。  
  
 **获取有关服务器级别事件通知的信息**  
  
-   [sys.server_event_notifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  至少必须满足下列条件：对服务器具有 CONTROL 或 VIEW ANY DEFINITION 权限，是事件通知的登录者或所有者，或者具有查看 **sys.server_event_notifications**中的任何事件通知的元数据的 ALTER ANY EVENT NOTIFICATION 权限。  
  
 **获取有关可以激发事件通知的所有事件的信息**  
  
-   [sys.event_notification_event_types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  此目录视图不返回事件组。  
  
## <a name="see-also"></a>另请参阅  
 [事件通知](../../relational-databases/service-broker/event-notifications.md)  
  
  

