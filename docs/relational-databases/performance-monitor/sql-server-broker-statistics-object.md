---
title: SQL Server - Broker Statistics 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 254da13dac84d9014062219665626bb51331d1d0
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158485"
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server Broker Statistics 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQLServer:Broker Statistics 性能对象包含为 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 实例报告常规 [!INCLUDE[ssDE](../../includes/ssde-md.md)]信息的性能计数器。 下表列出了此对象包含的计数器：  
  
|SQL Server Broker Statistics 计数器|描述|  
|-------------------------------------------|-----------------|  
|**Activation Errors Total**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 激活存储过程因出现错误而退出的次数。|  
|**Broker Transaction Rollbacks**|包含与 [!INCLUDE[ssSB](../../includes/sssb-md.md)]相关的 DML 语句（如 SEND 和 RECEIVE）的已回滚事务数。|  
|**Corrupted Messages Total**|实例收到的已损坏消息数。|  
|**Dequeued Transmission Msgs/sec**|每秒从 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 传输队列中删除的消息数。|  
|**Dialog timer event count**|对话协议层中处于活动状态的计时器数。 此数与活动的对话数相对应。|  
|**Dropped Messages Total**|实例已收到、但无法传递到队列的消息数。|  
|**Enqueued Local Messages Total**|已放入实例中的队列的消息数，仅计数未通过网络到达的消息。|  
|**Enqueued Local Messages/sec**|每秒放入实例中的队列的消息数，仅计数未通过网络到达的消息。|  
|**Enqueued Messages Total**|已放入实例中的队列的消息总数。|  
|**Enqueued Messages/sec**|每秒放入实例中的队列的消息数。 这包括所有优先级别的消息。|  
|**Enqueued P1 Msgs/sec**|每秒放入实例中的队列内、优先级为 1 的消息数。|  
|**Enqueued P2 Msgs/sec**|每秒放入实例中的队列内、优先级为 2 的消息数。|  
|**Enqueued P3 Msgs/sec**|每秒放入实例中的队列内、优先级为 3 的消息数。|  
|**Enqueued P4 Msgs/sec**|每秒放入实例中的队列内、优先级为 4 的消息数。|  
|**Enqueued P5 Msgs/sec**|每秒放入实例中的队列内、优先级为 5 的消息数。|  
|**Enqueued P6 Msgs/sec**|每秒放入实例中的队列内、优先级为 6 的消息数。|  
|**Enqueued P7 Msgs/sec**|每秒放入实例中的队列内、优先级为 7 的消息数。|  
|**Enqueued P8 Msgs/sec**|每秒放入实例中的队列内、优先级为 8 的消息数。|  
|**Enqueued P9 Msgs/sec**|每秒放入实例中的队列内、优先级为 9 的消息数。|  
|**Enqueued P10 Msgs/sec**|每秒放入实例中的队列内、优先级为 10 的消息数。|  
|**Enqueued Transmission Msgs/sec**|每秒放入 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 传输队列中的消息数。|  
|**Enqueued Transport Msg Frag Tot**|放入实例中的队列的消息片断数，仅计数通过网络到达的消息。|  
|**Enqueued Transport Msg Frags/sec**|每秒放入实例中的队列的消息片断数。|  
|**Enqueued Transport Msgs Total**|放入实例中的队列的消息数，仅计数通过网络到达的消息。|  
|**Enqueued Transport Msgs/sec**|每秒放入实例中的队列的消息数，仅计数通过网络到达的消息。|  
|**Forwarded Messages Total**|此计算机转发的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 消息总数。|  
|**Forwarded Messages/sec**|此计算机每秒转发的消息数。|  
|**Forwarded Msg Byte Total**|此计算机转发的消息的总大小（字节）。|  
|**Forwarded Msg Bytes/sec**|此计算机每秒转发的消息的大小（字节）。|  
|**Forwarded Msg Discarded Total**|此计算机收到的要转发、但转发失败的消息数。|  
|**Forwarded Msg Discarded/sec**|此计算机每秒收到的要转发、但转发失败的消息数。|  
|**Forwarded Pending Msg Bytes**|当前保留的要转发的消息的总大小。|  
|**Forwarded Pending Msg Count**|当前保留的要转发的消息总数。|  
|**SQL RECEIVE Total**|已处理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 语句的总数。|  
|**SQL RECEIVEs/sec**|每秒处理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 语句数。|  
|**SQL SEND Total**|已执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 语句的总数。|  
|**SQL SENDs/sec**|每秒执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 语句数。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
