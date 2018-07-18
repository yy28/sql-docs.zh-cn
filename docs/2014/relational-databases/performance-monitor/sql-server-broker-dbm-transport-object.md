---
title: SQL Server、 代理和 DBM Transport 对象 |Microsoft Docs
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
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 278e3776c19c9220b77347a0360e337184c4fd1f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253919"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>SQL Server、 代理和 DBM Transport 对象
  **Broker / DBM Transport** 性能对象包含报告 Service Broker 和数据库镜像的网络信息的性能计数器。 下表列出了此对象包含的计数器。  
  
|SQL Server Broker/DBM Transport 计数器|Description|  
|------------------------------------------------|-----------------|  
|**Current Bytes for Recv I/O**|此计数器报告当前运行的传输接收操作读取的字节数。|  
|**Current Bytes for Send I/O**|此计数器报告当前通过网络正被发送的消息片段中的字节数。|  
|**Current Msg Frags for Send I/O**|此计数器报告通过网络正被发送的消息片段的总数。|  
|**Message Fragment P1 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 1 的消息片段数。|  
|**Message Fragment P2 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 2 的消息片段数。|  
|**Message Fragment P3 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 3 的消息片段数。|  
|**Message Fragment P4 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 4 的消息片段数。|  
|**Message Fragment P5 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 5 的消息片段数。|  
|**Message Fragment P6 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 6 的消息片段数。|  
|**Message Fragment P7 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 7 的消息片段数。|  
|**Message Fragment P8 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 8 的消息片段数。|  
|**Message Fragment P9 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 9 的消息片段数。|  
|**Message Fragment P10 Sends/sec**|此计数器报告每秒通过网络发送的优先级为 10 的消息片段数。|  
|**消息片段发送大小 Avg**|此计数器报告通过网络发送的消息片段的平均大小。|  
|**Message Fragment Sends/sec**|此计数器报告每秒通过网络发送的所有优先级的消息片段数。|  
|**接收的消息片段数/秒**|此计数器报告每秒通过网络接收的消息片段数。|  
|**Msg Fragment Recv Size Avg**|此计数器报告通过网络接收的消息片段的平均大小。|  
|**Open Connection Count**|此计数器报告 Service Broker 当前已经打开的网络连接数。|  
|**Pending Bytes for Recv I/O**|此计数器报告已经从网络接收但尚未放置到队列中或尚未放弃的消息片段中包含的字节数。|  
|**Pending Bytes for Send I/O**|此计数器报告准备好通过网络发送的消息片段中的字节总数。|  
|**Pending Msg Frags for Recv I/O**|此计数器报告已经从网络接收但尚未放置到队列中或尚未放弃的消息片段数。|  
|**Pending Msg Frags for Send I/O**|此计数器报告准备好通过网络发送的消息片段的总数。|  
|**Receive I/O Bytes Total**|此计数器报告通过网络由 Service Broker 端点和数据库镜像端点接收的字节总数。|  
|**Receive I/O bytes/sec**|此计数器报告每秒通过网络由 Service Broker 端点和数据库镜像端点接收的字节数。|  
|**Receive I/O Len Avg**|此计数器报告传输接收操作的字节平均数。|  
|**接收 i/o 操作/秒**|此计数器报告每秒 Service Broker / DBM transport 层已完成的传输接收 I/O 操作数。 注意，传输接收操作可能包含多个消息片段。|  
|**Send I/O Bytes Total**|此计数器报告 Service Broker 端点和数据库镜像端点通过网络传送的总字节数。|  
|**Send I/O bytes/sec**|此计数器报告 Service Broker 端点和数据库镜像端点每秒通过网络传送的字节数。|  
|**Send I/O Len Avg**|此计数器报告每个传输发送操作的平均大小（以字节为单位）。 注意，传输发送操作可能包含多个消息片段。|  
|**Send I/Os/sec**|此计数器报告每秒已完成的传输发送 I/O 操作数。 注意，传输发送操作可能包含多个消息片段。|  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_broker_forwarded_messages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
