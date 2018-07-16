---
title: SQL Server - Broker Activation 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4de21798991eb269cdca7232eb38ecdacc93e956
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320347"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server Broker Activation 对象
  **SQLServer:BrokerActivation** 性能对象包含一些性能计数器，这些计数器报告有关存储过程激活的信息。 下表列出了此对象包含的计数器。  
  
|SQL Server Broker Activation 计数器|Description|  
|-------------------------------------------|-----------------|  
|**Stored Procedures Invoked/sec**|此计数器报告每秒内实例中所有队列监视器调用的激活存储过程的总数。|  
|**Task Limit Reached**|此计数器报告队列监视器本应启动新任务但由于已在运行的队列任务数达到最大值而并未启动的总次数。|  
|**Task Limit Reached/sec**|此计数器报告每秒内队列监视器本应启动新任务但由于已在运行的队列任务数达到最大值而并未启动的次数。|  
|**Tasks Aborted/sec**|此计数器报告以错误结束或由队列监视器因无法接收消息而中止的激活存储过程任务数。|  
|**Tasks Running**|此计数器报告当前运行的激活存储过程数。|  
|**Tasks Started/sec**|此计数器报告每秒内实例中所有队列监视器启动的激活存储过程数。|  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_broker_activated_tasks (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql)   
 [sys.dm_broker_queue_monitors (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql)   
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
