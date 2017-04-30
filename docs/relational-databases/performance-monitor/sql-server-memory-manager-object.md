---
title: "SQL Server - Memory Manager 对象 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Memory Manager
- Memory Manager object
ms.assetid: dbf49000-eeb0-4e9c-a361-5092363920dc
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 884e6d05db70f9978b84a3423bdfad748f50b29c
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-memory-manager-object"></a>SQL Server Memory Manager 对象
  Microsoft **中的** Memory Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象提供了监视总体的服务器内存使用情况的计数器。 监视总体的服务器内存使用情况，以估计用户活动和资源使用，有助于查明性能瓶颈。 监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例使用的内存有助于确定：  
  
-   瓶颈的存在是否是因为物理内存不足以存储缓存中被频繁访问的数据。 如果内存不足， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须从磁盘检索数据。  
  
-   是否可以通过添加更多内存或使更多内存可用于数据缓存或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部结构来改善查询性能。  
  
## <a name="memory-manager-counters"></a>Memory Manager 计数器  
 下表说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Manager** 计数器。  
  
|SQL Server Memory Manager 计数器|说明|  
|----------------------------------------|-----------------|  
|**Connection Memory (KB)**|指定服务器正用来维护连接的动态内存的总量。|  
|**Database Cache Memory (KB)**|指定服务器当前正用来缓存数据库页面的内存量。|  
|**External benefit of memory**|内存的外部值(毫秒/页/毫秒，乘以 100 亿并截断为整数)。| 
|**Free Memory (KB)**|指定服务器当前未使用的已提交内存量。|  
|**Granted Workspace Memory (KB)**|指定当前授予执行哈希、排序、大容量复制和索引创建操作等进程的内存总量。|  
|**Lock Blocks**|指定服务器上使用的锁块的当前数目（定期进行刷新）。 一个锁块代表一个单独的锁定资源，如表、页或行。|  
|**Lock Blocks Allocated**|指定所分配的锁块的当前数量。 服务器启动时，分配的锁块数加上分配的锁拥有者块数依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 配置选项。 若需要更多的锁块，此值会增加。|  
|**Lock Memory (KB)**|指定服务器用于锁的动态内存总量。|  
|**Lock Owner Blocks**|指定当前正在服务器上使用的锁拥有者块的数目（定期进行刷新）。 一个锁拥有者块代表一个独立线程对某一对象上的一个锁的拥有权。 因此，若三个线程在一个页上各有一个共享 (S) 锁，就会有三个锁拥有者块。|  
|**Lock Owner Blocks Allocated**|指定所分配的锁拥有者块的当前数量。 服务器启动时，分配的锁拥有者块数和分配的锁块数依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 配置选项。 若需要更多的锁拥有者块，此数值会动态增加。|  
|**Log Pool Memory (KB)**|服务器正用于日志池的动态内存的总量。| 
|**Maximum Workspace Memory (KB)**|指示用于执行哈希、排序、大容量复制和索引创建操作等进程的最大可用内存数。|  
|**Memory Grants Outstanding**|指定成功获得工作空间内存授权的进程总数。|  
|**Memory Grants Pending**|指定等待工作空间内存授权的进程总数。|  
|**Optimizer Memory (KB)**|指定服务器正用于查询优化的动态内存总数。|  
|**Reserved Server Memory (KB)**|指示服务器保留供将来使用的内存量。 此计数器显示最初授予（显示在 **Granted Workspace Memory (KB)**中）但当前未使用的内存量。|  
|**SQL Cache Memory (KB)**|指定服务器正用于动态 SQL 缓存的动态内存总数。|  
|**Stolen Server Memory (KB)**|指定服务器当前正用于除数据库页面之外的其他用途的内存量。|  
|**Target Server Memory (KB)**|指示服务器能够使用的理想内存量。|  
|**Total Server Memory (KB)**|指定服务器已使用内存管理器提交的内存量。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Buffer Manager 对象](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
[sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
