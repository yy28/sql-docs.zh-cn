---
title: "内存中 OLTP 垃圾回收 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 内存中 OLTP 垃圾回收
  如果数据行已被一个不再活动的事务删除，则该数据行被视为是陈旧的。 可对陈旧的行进行垃圾回收。 下面是[!INCLUDE[hek_2](../../includes/hek-2-md.md)] 中垃圾收集的特征：  
  
-   不产生阻塞。 垃圾收集随着时间推移进行分布，对工作负荷的影响极小。  
  
-   协作。 用户事务通过主垃圾收集线程参与垃圾收集。  
  
-   高效。 用户事务将所使用的访问路径（索引）中的陈旧行解除链接。 这样会减少最终删除行时所需的工作。  
  
-   快速响应。 内存压力会导致频繁垃圾收集。  
  
-   可缩放。 提交后，用户事务执行部分垃圾收集工作。 事务活动越多，解除链接的陈旧行就越多。  
  
 垃圾收集由主垃圾收集线程控制。 主垃圾收集线程每分钟运行一次，或在提交的事务数目超过内部阈值时运行。 垃圾收集器的任务是：  
  
-   标识已删除或更新一组行且在最旧的活动事务之前已提交的事务。  
  
-   标识这些旧事务创建的行版本。  
  
-   将旧行分组到每个单元有 16 行的一个或多个单元中。 执行此操作是为了将垃圾收集器的工作分配到若干较小的单元中。  
  
-   将这些工作单元移到垃圾收集队列中，每个计划程序一个。 有关详细信息，请参考以下垃圾回收器 DMV：[sys.dm_xtp_gc_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md)、[sys.dm_db_xtp_gc_cycle_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md) 和 [sys.dm_xtp_gc_queue_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)。  
  
 在用户事务提交后，它识别与它在其上运行的计划程序相关联的所有排队项，然后释放内存。 如果计划程序上的垃圾收集队列为空，则它会搜索当前 NUMA 节点中的任何非空队列。 如果存在较少事务活动或者有内存压力，则主垃圾收集线程可访问任何队列的垃圾收集行。 如果在删除大量行后（举例）没有事务活动并且没有内存压力，则在事务活动恢复或有内存压力之前，不会对删除的行进行垃圾收集。  
  
## 另请参阅  
 [管理内存中 OLTP 的内存](../Topic/Managing%20Memory%20for%20In-Memory%20OLTP.md)  
  
  