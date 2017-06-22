---
title: "为内存优化表配置存储 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0250c8370960dc17adf13c020c51bfc603b111c8
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configuring-storage-for-memory-optimized-tables"></a>为内存优化表配置内存
  您需要配置存储容量和每秒输入/输出操作数 (IOPS)。  
  
## <a name="storage-capacity"></a>存储容量  
 使用 [估算内存优化表的内存需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 中的信息估计数据库的持久内存优化表的内存中大小。 由于未为内存优化表保留索引，因此不包括索引大小。 确定此大小后，您需要提供大小为持久内存中表大小的四倍的磁盘空间。  
  
## <a name="storage-iops"></a>存储 IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 会大大增加您的工作负荷吞吐量。 因此，确保 IO 不成为瓶颈非常重要。  
  
-   在将基于磁盘的表迁移到内存优化表时，请确保事务日志位于可支持增加事务日志活动的存储介质上。 例如，如果存储介质以 100 MB/秒的速度支持事务日志操作，并且内存优化表产生 5 倍以上的性能，则事务日志的存储介质必须还能支持 5 倍的性能改进，从而防止事务日志活动成为性能瓶颈。  
  
-   内存优化表保留在跨一个或多个容器分布的文件中。 通常，每个容器均应映射到其自己的主轴，并用于增加的存储容量和改进的 IOPS。 您需要确保存储介质的顺序 IOPS 可支持事务日志吞吐量的 3 倍增长。  
  
     例如，如果内存优化表在事务日志中生成 500MB/秒的活动，则内存优化表的存储必须支持 1.5GB/秒 IOPS。 之所以需要支持事务日志吞吐量的 3 倍增长，是因为观察到，数据和差异文件对将先与初始数据一起写入，然后需要作为合并操作的一部分读取/重新写入。  
  
     估计存储的 IOPS 时要考虑的另一个因素是内存优化表的恢复时间。 在使数据库对应用程序可用前，必须将持久表中的数据读取到内存中。 通常，可按 IOPS 速度将数据加载到内存优化表中。 如果持久内存优化表的总存储为 60 GB，并且您希望能够在 1 分钟内加载此数据，则存储的 IOPS 必须设置为 1 GB/秒。  
  
-   如果你有偶数个主轴，则与 SQL Server 2014 中不同，检查点文件将跨所有主轴均匀分布。  
  
## <a name="encryption"></a>加密  
 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中，作为在数据库上启用 TDE 的操作的一部分，将对内存优化表的存储进行加密。 有关详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption-tde.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化的对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
