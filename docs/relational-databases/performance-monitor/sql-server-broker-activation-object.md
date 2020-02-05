---
title: SQL Server - Broker Activation 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 364fd8e037e2c09afa16294e75096993f861ca20
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67987159"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server Broker Activation 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
  
