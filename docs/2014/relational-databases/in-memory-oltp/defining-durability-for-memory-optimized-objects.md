---
title: 为内存优化对象定义持续性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: caae904bc1e25288e81d3baba21719be28c05d31
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050231"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>为内存优化对象定义持续性
  内存中 OLTP 可保证完整原子性、一致性、隔离和完整持久性 (ACID) 属性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和内存优化表上下文中的持续性提供了以下保证：  
  
 事务持续性  
 提交对内存优化表作出（DDL 或 DML）更改的完全持久事务时，对持久内存优化表作出的更改为永久更改。  
  
 向内存优化表提交延迟的持久事务时，仅在将内存中事务日志保存到磁盘后，该事务才成为持久事务。  
  
 重新启动持续性  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在崩溃或计划关闭后重新启动时，将对内存优化的持久表重新实例化，使其恢复为关闭或崩溃之前的状态。  
  
 介质故障持续性  
 如果发生故障或损坏的磁盘包含持久内存优化的对象的一个或多个持久化副本，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份和还原功能将内存优化表还原到新介质上。  
  
 有两个用于内存优化表的持续性选项：  
  
 SCHEMA_ONLY（非持久表）  
 此选项可确保表架构（包括索引）的持续性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新启动时，将会重新创建非持久表，但是该表启动时不包含数据。 （这与 tempdb 中的表不同；对于 tempdb 中的表，表及其数据都会在重新启动时丢失。）创建非持久表的典型情况是用于存储瞬时数据（如用于 ETL 进程的临时表）。 SCHEMA_ONLY 持续性可避免事务日志记录和检查点，这样可大幅减少 I/O 操作数。  
  
 SCHEMA_AND_DATA（持久表）  
 此选项提供架构和数据的持续性。 数据持续性的级别取决于提交事务时其作为完全持久还是延迟持续性。 完全持久事务对数据和架构提供相同的持续性保证，与基于磁盘的表类似。 延迟持续性将提高性能，但如果服务器崩溃或进行故障转移，则可能会丢失数据。 （有关延迟持续性的详细信息，请参阅 [控制事务持续性](../logs/control-transaction-durability.md)。）  
  
 与基于磁盘的表类似，内存优化表的架构在数据库的主文件组中持久化。  
  
 持久内存优化表中的数据保存在数据和差异文件对中。  
  
 内存优化表中定义的索引仅在元数据中持久化，而在存储中不持久化。 索引结构是在加载内存优化表期间生成的。  
  
 行由 DELETE 语句显式删除，或由 UPDATE 语句间接删除。 UPDATE 操作是先执行删除，然后执行插入。 删除行时，不会对数据文件进行任何更改，但是将用于标识已删除行的新行追加到对应的差异文件。  
  
 在恢复或还原操作过程中，内存中 OLTP 引擎读取数据和差异文件以将其载入物理内存。 加载时间由以下因素决定：  
  
-   要加载的数据量。  
  
-   顺序 I/O 带宽。  
  
-   并行度，由文件容器数和处理器核心数决定。  
  
-   日志的活动部分中需重做的日志记录量。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化对象的存储](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
