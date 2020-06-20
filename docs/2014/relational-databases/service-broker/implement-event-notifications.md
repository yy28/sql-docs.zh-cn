---
title: 实现事件通知 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a89c66ca5c3b420fff14c087bd604b16c641369
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996551"
---
# <a name="implement-event-notifications"></a>实现事件通知
  若要实现事件通知，必须先创建目标服务以接收事件通知，然后再创建事件通知。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话安全模式。 必须根据完全安全模式手动配置对话安全设置。  
  
## <a name="creating-the-target-service"></a>创建目标服务  
 无需创建 [!INCLUDE[ssSB](../../includes/sssb-md.md)]启动服务，因为 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 包含以下特定的事件通知消息类型和约定：  
  
```  
https://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 接收事件通知的目标服务必须使用此预先存在的约定。  
  
 **创建目标服务**：  
  
1.  创建队列以接收消息。  
  
    > [!NOTE]  
    >  队列接收下列消息类型： `https://schemas.microsoft.com/SQL/Notifications/QueryNotification`。  
  
2.  在引用事件通知约定的队列上创建服务。  
  
3.  创建服务路由，以定义 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将服务消息发送到的地址。 对于指向同一数据库中的服务的事件通知，请指定 `ADDRESS = 'LOCAL'`。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由确定接收通知消息的服务。 如果事件通知指向远程服务器中的服务，则源服务器和目标服务器必须都定义了路由，确保实现双向通信。  
  
 下面的示例将创建队列、队列服务以及服务路由，以便依据事件通知约定处理消息。  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[https://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## <a name="creating-the-event-notification"></a>创建事件通知  
 事件通知使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION 语句创建，使用 DROP EVENT NOTIFICATION STATEMENT 删除。 若要修改事件通知，必须先删除事件通知，然后再重新创建。  
  
 下面的示例将创建事件通知 `CreateDatabaseNotification`。 该通知将服务器中发生的 `CREATE_DATABASE` 事件的相关消息发送到先前创建的 `NotifyService` 服务。  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  事件通知将 CREATE_SCHEMA 事件和 CREATE SCHEMA 语句的 <schema_element> 定义识别为不同的事件。 例如，针对 CREATE_SCHEMA 和 CREATE_TABLE 事件创建事件通知，然后便可运行以下批处理。  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  在此情况下，事件通知会引发两次：一次是在 CREATE_SCHEMA 事件发生时，另一次是在 CREATE_TABLE 事件发生时。 建议您避免针对 CREATE_SCHEMA 事件和任何相应 CREATE SCHEMA 定义的 <schema_element> 文本创建事件通知，也不要将逻辑置入应用程序中以免捕获不需要的事件数据。  
  
 **创建事件通知**  
  
-   [CREATE EVENT NOTIFICATION (Transact-SQL)](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
 **删除事件通知**  
  
-   [DROP EVENT NOTIFICATION (Transact-SQL)](/sql/t-sql/statements/drop-event-notification-transact-sql)  
  
## <a name="see-also"></a>另请参阅  
 [获取有关事件通知的信息](event-notifications.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
