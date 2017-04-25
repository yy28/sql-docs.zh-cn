---
title: "SQL Server - Broker Activation 对象 | Microsoft Docs"
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
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 98c72781fdd1532c683bc918221b22a77c419f12
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-broker-activation-object"></a>SQL Server Broker Activation 对象
  **SQLServer:BrokerActivation** 性能对象包含一些性能计数器，这些计数器报告有关存储过程激活的信息。 下表列出了此对象包含的计数器。  
  
|SQL Server Broker Activation 计数器|说明|  
|-------------------------------------------|-----------------|  
|**Stored Procedures Invoked/sec**|此计数器报告每秒内实例中所有队列监视器调用的激活存储过程的总数。|  
|**Task Limit Reached**|此计数器报告队列监视器本应启动新任务但由于已在运行的队列任务数达到最大值而并未启动的总次数。|  
|**Task Limit Reached/sec**|此计数器报告每秒内队列监视器本应启动新任务但由于已在运行的队列任务数达到最大值而并未启动的次数。|  
|**Tasks Aborted/sec**|此计数器报告以错误结束或由队列监视器因无法接收消息而中止的激活存储过程任务数。|  
|**Tasks Running**|此计数器报告当前运行的激活存储过程数。|  
|**Tasks Started/sec**|此计数器报告每秒内实例中所有队列监视器启动的激活存储过程数。|  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_broker_activated_tasks (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql.md)   
 [sys.dm_broker_queue_monitors (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
