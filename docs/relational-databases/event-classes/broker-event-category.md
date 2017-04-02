---
title: "Broker 事件类别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server 事件类, Broker 事件类别"
  - "Broker 事件类别 [SQL Server]"
  - "事件类 [SQL Server], Broker 事件类别"
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# Broker 事件类别
  **Broker** 事件类别包含一般的 Service Broker 事件。  
  
## 本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[Broker:Activation 事件类](../../relational-databases/event-classes/broker-activation-event-class.md)|队列监视器启动激活存储过程时生成的事件。|  
|[Broker:Connection 事件类](../../relational-databases/event-classes/broker-connection-event-class.md)|为报告 Service Broker 所管理的传输连接的状态而生成的事件。|  
|[Broker:Conversation 事件类](../../relational-databases/event-classes/broker-conversation-event-class.md)|为报告会话进度而生成的事件。|  
|[Broker:Conversation Group 事件类](../../relational-databases/event-classes/broker-conversation-group-event-class.md)|数据库创建或删除会话组时生成的事件。|  
|[Broker:Corrupted Message 事件类](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)|为报告数据库接收到损坏的消息而生成的事件。|  
|[Broker:Forwarded Message Dropped 事件类](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)|SQL Server 删除本应已转发的 Service Broker 消息时生成的事件。|  
|[Broker:Forwarded Message Sent 事件类](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)|SQL Server 转发 Service Broker 消息时生成的事件。|  
|[Broker:Message Classify 事件类](../../relational-databases/event-classes/broker-message-classify-event-class.md)|Service Broker 确定消息的路由时生成的事件。|  
|[Broker:Message Drop 事件类](../../relational-databases/event-classes/broker-message-drop-event-class.md)|当 Service Broker 无法保留已收到的应传递给此实例中某个服务的消息时生成的事件。|  
|[Broker:Remote Message Ack 事件类](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|Service Broker 发送或接收消息确认时生成的事件。|  
  
 还为 Service Broker 提供了两个安全审核事件。 有关这些事件的详细信息，请参阅 [Audit Broker Login 事件类](../../relational-databases/event-classes/audit-broker-login-event-class.md)和 [Audit Broker Conversation 事件类](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)。  
  
## 另请参阅  
 [“安全审核”事件类别](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  