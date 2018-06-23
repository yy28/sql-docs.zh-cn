---
title: Broker 事件类别 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fbcb1207da570e960ba7eb2f96a2d698b7d69d3b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137983"
---
# <a name="broker-event-category"></a>Broker 事件类别
  **Broker** 事件类别包含一般的 Service Broker 事件。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[Broker:Activation 事件类](broker-activation-event-class.md)|队列监视器启动激活存储过程时生成的事件。|  
|[Broker:Connection 事件类](broker-connection-event-class.md)|为报告 Service Broker 所管理的传输连接的状态而生成的事件。|  
|[Broker:Conversation 事件类](broker-conversation-event-class.md)|为报告会话进度而生成的事件。|  
|[Broker:Conversation Group 事件类](broker-conversation-group-event-class.md)|数据库创建或删除会话组时生成的事件。|  
|[Broker:Corrupted Message 事件类](broker-corrupted-message-event-class.md)|为报告数据库接收到损坏的消息而生成的事件。|  
|[Broker:Forwarded Message Dropped 事件类](broker-forwarded-message-dropped-event-class.md)|SQL Server 删除本应已转发的 Service Broker 消息时生成的事件。|  
|[Broker:Forwarded Message Sent 事件类](broker-forwarded-message-sent-event-class.md)|SQL Server 转发 Service Broker 消息时生成的事件。|  
|[Broker:Message Classify 事件类](broker-message-classify-event-class.md)|Service Broker 确定消息的路由时生成的事件。|  
|[Broker:Message Drop 事件类](broker-message-drop-event-class.md)|当 Service Broker 无法保留已收到的应传递给此实例中某个服务的消息时生成的事件。|  
|[Broker:Remote Message Ack 事件类](broker-remote-message-ack-event-class.md)|Service Broker 发送或接收消息确认时生成的事件。|  
  
 还为 Service Broker 提供了两个安全审核事件。 有关这些事件的详细信息，请参阅 [Audit Broker Login 事件类](audit-broker-login-event-class.md) 和 [Audit Broker Conversation 事件类](audit-broker-conversation-event-class.md)。  
  
## <a name="see-also"></a>请参阅  
 [“安全审核”事件类别](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  