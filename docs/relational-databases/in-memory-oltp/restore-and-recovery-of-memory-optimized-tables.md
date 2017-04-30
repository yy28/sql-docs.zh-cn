---
title: "内存优化表的还原和恢复 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 56e6ac814b90fdd38f21be32f506846e542be977
ms.lasthandoff: 04/11/2017

---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>内存优化表的还原和恢复
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  检索或还原具有内存优化表的数据库的基本机制类似于仅具有基于磁盘的表的数据库。 但与基于磁盘的表不同，必须首先将内存优化表加载到内存中，然后数据库才可用于用户访问。 这会在数据库恢复中添加一个新步骤。  
  
 在恢复或还原操作过程中，内存中 OLTP 引擎读取数据和差异文件以将其载入物理内存。 加载时间由以下因素决定：  
  
-   要加载的数据量。  
  
-   顺序 I/O 带宽。  
  
-   并行度，由文件容器数和处理器核心数决定。  
  
-   日志的活动部分中需重做的日志记录量。  
  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新启动时，每个数据库都会经历一个恢复阶段，该阶段由以下三个阶段构成：  
  
1.  分析阶段。 在此阶段中，将对活动事务日志执行一遍，以便检测已提交和未提交事务。 内存中 OLTP 引擎标识检查点以便加载和预加载其系统表日志条目。 它还将处理某些文件分配日志记录。  
  
2.  重做阶段。 此阶段在基于磁盘的表和内存优化表上同时运行。  
  
     对于基于磁盘的表，数据库将移到当前时间点并且获取未提交事务持有的锁。  
  
     对于内存优化表，来自数据和差异文件对的数据将加载到内存中，然后基于上一持久检查点通过活动事务日志更新数据。  
  
     在基于磁盘的表和内存优化表上的上述操作完成后，数据库将可供访问。  
  
3.  撤消阶段。 在此阶段中，将回滚未提交的事务。  
  
 将内存优化表加载到内存中可能会影响恢复时间目标 (RTO) 的性能。 为缩短从数据和差异文件加载内存优化的数据的时间，内存中 OLTP 引擎按如下所示并行加载数据/差异文件：  
  
-   创建增量映射筛选器。 差异文件存储对已删除行的引用。 每个容器的一个线程读取差异文件并且创建增量映射筛选器。 （内存优化数据文件组可以具有一个或多个容器。）  
  
-   对数据文件进行流式处理。  在创建了增量映射筛选器后，可使用与逻辑 CPU 数量一样多的线程读取数据文件。 读取数据文件的每个线程都读取数据行、检查关联的增量映射并且只将尚未标记为删除的行插入表中。 在某些情况下，此部分的恢复可能是受到 CPU 的约束的，如下所述。  
  
 ![内存优化表。](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "内存优化表。")  
  
 内存优化表通常可按 I/O 速度加载到内存中，但有些情况下，将数据行加载到内存中将会较慢。 具体情况为：  
  
-   针对哈希索引的较低的存储桶计数可能会导致过多冲突，以致降低插入数据行的速度。 这通常导致非常高的 CPU 使用吞吐量，尤其是在恢复即将结束时。 如果您正确配置了哈希索引，则不应影响恢复时间。  
  
-   与在创建时调整其存储桶计数大小的哈希索引不同，具有一个或多个非聚集索引的大型内存优化表会动态增长，从而导致较高的 CPU 使用率。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表的备份、还原和恢复](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
