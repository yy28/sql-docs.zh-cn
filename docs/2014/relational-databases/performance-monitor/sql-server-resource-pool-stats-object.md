---
title: SQL Server - Resource Pool Stats 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reosurce Pool Stats object
- 'SQLServer: Resource Pool Stats object'
ms.assetid: bb46e029-fcf9-4aeb-a066-be41e7668fb9
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 26d74ff671e55843b279d0609e8ee99a6b7b58b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015874"
---
# <a name="sql-server-resource-pool-stats-object"></a>SQL Server，Resource Pool Stats 对象
  SQLServer:Resource Pool Stats 对象包含报告资源调控器资源池统计相关信息的性能计数器。  
  
 每个活动资源池都创建一个 SQLServer:Resource Pool Stats 性能对象实例，实例的名称与资源调控器资源池的名称相同。 下表介绍了此实例支持的计数器。  
  
|计数器名称|Description|  
|------------------|-----------------|  
|CPU usage %|属于此池的所有工作负荷组中所有请求的 CPU 带宽使用量。 此值是相对于计算机度量的，并针对系统中的所有 CPU 进行规范化。 此值将随着可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的 CPU 量的变化而变化。 它不会针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程接收的信息进行规范化。|  
|CPU usage target %|资源池基于资源池配置设置和系统负荷的目标 CPU 使用率 (%)。|  
|CPU control effect %|资源调控器对资源池的控制效果。 计算公式为：（CPU 使用率 %）/（无资源调控器情况下的 CPU 使用率 %）。|  
|Compile memory target (KB)|查询编译的当前内存代理目标值，以千字节 (KB) 为单位。|  
|Cache memory target (KB)|缓存的当前内存代理目标值，以千字节 (KB) 为单位。|  
|Query exec memory target (KB)|查询执行内存授予的当前内存代理目标值，以千字节 (KB) 为单位。 此信息还可在 [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql)中获得。|  
|Memory grants/sec|每秒此资源池中发生的内存授予数。|  
|Active memory grants count|当前内存授予总数。 此信息还可在 [sys.dm_exec_query_memory_grants](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql)中获得。|  
|Memory grant timeouts/sec|每秒内存授予超时数。|  
|Active memory grant amount (KB)|当前授予的内存总量，以千字节 (KB) 为单位。 此信息还可在 [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql) 中获得。|  
|Pending memory grant count|队列中挂起的内存授予请求数。 此信息还可在 [sys.dm_exec_query_resource_semaphores](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql)中获得。|  
|Max memory (KB)|资源池基于资源池设置和服务器状态可获得的最大内存量，以千字节 (KB) 为单位。|  
|Used memory (KB)|用于资源池的内存量，以千字节 (KB) 为单位。|  
|Target memory (KB)|资源池基于资源池设置和服务器状态尝试获得的目标内存量，以千字节 (KB) 为单位。|  
|Disk Read IO/sec|在上一秒中从磁盘读取的操作数。|  
|Disk Read IO Throttled/sec|在上一秒中中止的读取操作数。|  
|Disk Read Bytes/sec|在上一秒中从磁盘读取的字节数。|  
|Avg Disk Read IO (ms)|从磁盘进行读取操作的平均时间（毫秒）。|  
|Disk Write IO/sec|在上一秒中写入磁盘的操作数。|  
|Disk Write IO Throttled/sec|在上一秒中中止的写入操作数。|  
|Disk Write Bytes/sec|在上一秒中写入磁盘的字节数。|  
|Avg Disk Write IO (ms)|对磁盘进行写入操作的平均时间（毫秒）。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)   
 [SQLServer，Workload Group Stats 对象](sql-server-workload-group-stats-object.md)   
 [资源调控器](../resource-governor/resource-governor.md)  
  
  
