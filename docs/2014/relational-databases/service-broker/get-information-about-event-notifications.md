---
title: 获取有关事件通知的信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9786faaf44724b1a2452bd5304b63deb2c9ea54e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015309"
---
# <a name="get-information-about-event-notifications"></a>获取有关事件通知的信息
  下列目录视图可用于查询有关事件通知的元数据。  
  
 **获取有关非服务器级别事件通知的信息**  
  
-   [sys.event_notifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql)  
  
> [!NOTE]  
>  若要查看有关中的任何事件通知的元数据**sys.event_notifications**数据库级别创建，最小值必须具备以下条件：控制、 ALTER、 TAKE OWNERSHIP 或 VIEW DEFINITION 权限对数据库中，是事件通知的所有者或具有 ALTER ANY DATABASE EVENT NOTIFICATION 权限。 对于对特定队列创建的事件通知，最小值您必须具有：控制、 ALTER、 TAKE OWNERSHIP 或 VIEW DEFINITION 权限的对象上，是事件通知的所有者或具有 ALTER ANY DATABASE EVENT NOTIFICATION 权限。  
  
 **获取有关服务器级别事件通知的信息**  
  
-   [sys.server_event_notifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql)  
  
> [!NOTE]  
>  最小值，必须具备以下各项：控制或 VIEW ANY DEFINITION 权限在服务器上，为登录或事件通知的所有者或者具有 ALTER ANY EVENT NOTIFICATION 权限以查看有关中的任何事件通知的元数据**sys.server_event_notifications**.  
  
 **获取有关可以激发事件通知的所有事件的信息**  
  
-   [sys.event_notification_event_types (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql)  
  
> [!NOTE]  
>  此目录视图不返回事件组。  
  
## <a name="see-also"></a>请参阅  
 [事件通知](event-notifications.md)  
  
  
