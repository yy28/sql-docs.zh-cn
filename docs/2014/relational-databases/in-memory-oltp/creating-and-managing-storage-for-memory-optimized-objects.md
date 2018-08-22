---
title: 创建和管理用于内存优化对象的存储 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
caps.latest.revision: 61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4459972905c5f40eddc55e126a4fb37e89cf29d9
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392699"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>创建和管理用于内存优化的对象的存储
  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎集成到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之中，这可让你在同一数据库中同时拥有内存优化表和（传统的）基于磁盘的表。 但是，内存优化表的存储结构不同于基于磁盘的表。  
  
 基于磁盘的表的存储具有以下键属性：  
  
-   映射到文件组且该文件组包含一个或多个文件。  
  
-   每个文件分为 8 页的盘区，且每页的大小为 8K 字节。  
  
-   可以在多个表之间共享盘区，但在已分配的页和表或索引之间存在 1 对 1 的映射。 换而言之，一页不能有来自两个或多个表或索引的行。  
  
-   数据将根据需要移动到内存（缓冲池）中，已修改或新创建的页将异步写入到主要生成随机 IO 的磁盘。  
  
 内存优化表的存储具有以下键属性：  
  
-   所有内存优化表都映射到内存优化文件组。 使用 filestream 文件组来生成此文件组。  
  
-   没有任何页，且数据作为行保留。  
  
-   通过追加到活动文件来存储对内存优化表的所有更改。 读取和写入文件都是按顺序进行的。  
  
-   通过进行删除，然后进行插入来实现更新。 已删除的行不会立刻从存储中删除。 已删除的行将基于 [内存优化表的持续性](memory-optimized-tables.md)中所述的策略通过名为 MERGE 的后台进程删除。  
  
-   与基于磁盘的表不同，内存优化表的存储不会被压缩。 在将压缩的（ROW 或 PAGE）基于磁盘的表迁移到内存优化表时，需要考虑大小的改变。  
  
-   内存优化表可以是持久的或非持久的。 只需为持久内存优化表配置存储。  
  
 本节描述检查点文件对以及内存优化表中数据的存储方式的其他方面。  
  
 本节主题：  
  
-   [为内存优化表配置内存](configuring-storage-for-memory-optimized-tables.md)  
  
-   [内存优化的文件组](the-memory-optimized-filegroup.md)  
  
-   [内存优化表的持续性](memory-optimized-tables.md)  
  
-   [内存优化表的检查点操作](checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [为内存优化对象定义持续性](defining-durability-for-memory-optimized-objects.md)  
  
-   [比较基于磁盘的表存储与内存优化的表存储](comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
-   [监视数据与差异文件对的合并以及排除其故障](../../database-engine/monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs.md)  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](in-memory-oltp-in-memory-optimization.md)  
  
  
