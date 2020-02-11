---
title: 为内存优化表配置存储 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 93698be4738ef2a28c79581d0957f695b036c911
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62990638"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>为内存优化表配置内存
  您需要配置存储容量和每秒输入/输出操作数 (IOPS)。  
  
## <a name="storage-capacity"></a>存储容量  
 使用 [估算内存优化表的内存需求](memory-optimized-tables.md) 中的信息估计数据库的持久内存优化表的内存中大小。 由于未为内存优化表保留索引，因此不包括索引大小。 确定此大小后，您需要提供大小为持久内存中表大小的四倍的磁盘空间。  
  
## <a name="storage-performance"></a>存储性能  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]可以显著增加工作负荷吞吐量。 因此，确保 IO 不成为瓶颈非常重要。  
  
-   在将基于磁盘的表迁移到内存优化表时，请确保事务日志位于可支持增加事务日志活动的存储介质上。 例如，如果存储介质以 100 MB/秒的速度支持事务日志操作，并且内存优化表产生 5 倍以上的性能，则事务日志的存储介质必须还能支持 5 倍的性能改进，从而防止事务日志活动成为性能瓶颈。  
  
-   内存优化表保留在跨一个或多个容器分布的文件中。 通常，每个容器均应映射到其自己的主轴，并用于增加的存储容量和改进的性能。 你需要确保存储介质的顺序 IOPS 可支持事务日志吞吐量的3倍增长。  
  
     例如，如果内存优化表在事务日志中生成 500MB/sec 的活动，则内存优化表的存储必须支持 1.5 GB/秒。如果需要支持事务日志吞吐量的3倍增长，就会观察到，数据和差异文件对首先用初始数据写入，然后需要作为合并操作的一部分读取/重新写入。  
  
     估计存储的吞吐量时要考虑的另一个因素是内存优化表的恢复时间。 在使数据库对应用程序可用前，必须将持久表中的数据读取到内存中。 通常，可按 IOPS 速度将数据加载到内存优化表中。 如果持久内存优化表的总存储为 60 GB，并且您希望能够在 1 分钟内加载此数据，则存储的 IOPS 必须设置为 1 GB/秒。  
  
-   如果您具有偶数个主轴，则应创建两倍数目的容器，并且每对映射到相同的主轴。 这是扩展 IOPS 和存储所需的。 有关详细信息，请参阅[内存优化文件组](the-memory-optimized-filegroup.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化对象的存储](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
