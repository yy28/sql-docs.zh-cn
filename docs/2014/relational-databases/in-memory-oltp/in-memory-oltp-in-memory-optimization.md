---
title: 内存中 OLTP（内存中优化）| Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0893a32d31c4f64d99503fce7e64ccdd325cea7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138507"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>内存中 OLTP（内存中优化）
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]中的新增功能 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 可大幅度提高 OLTP 数据库应用程序性能。 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 是集成到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 引擎中的内存优化的数据库引擎，针对 OLTP 进行了优化。  
  
|||  
|-|-|  
|![Azure 虚拟机](../../master-data-services/media/azure-virtual-machine.png "Azure 虚拟机")|是否想要试用 SQL Server 2016？ 注册 Microsoft Azure，然后转到 **[此处](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** 以加速已安装有 SQL Server 2016 的虚拟机。 你可以在完成操作后删除该虚拟机。|  
  
 若要使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]，请将经常访问的表定义为内存优化表。 内存优化表具有完全事务性和持久性，可通过与访问基于磁盘的表一样的方式使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 对其进行访问。 查询可引用内存优化表和基于磁盘的表。 事务可更新内存优化表和基于磁盘的表中的数据。 仅引用内存优化表的存储过程可本机编译为机器代码，以便进一步提高性能。 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎专用于实现从高度扩展的中间层推动的 OLTP 类型的事务的超高会话并发。 为实现此目标，它使用无闩锁数据结构和多版本乐观并发控制。 结果是可预测的，通过数据库事务的线性扩展实现了亚毫秒级低延迟和高吞吐量。 实际的性能提升取决于许多因素，但通常可实现 5 到 20 倍的性能改进。  
  
 下表总结了可通过使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]获得最多好处的工作负载模式：  
  
|实现场景|实现场景|优势 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]|  
|-----------------------------|-----------------------------|-------------------------------------|  
|来自多个并发连接的高数据插入率。|主要是仅限追加存储。<br /><br /> 无法与工作负荷保持同步。|消除争用。<br /><br /> 减少日志记录。|  
|读取性能并通过定期批量插入和更新进行扩展。|高性能读取操作，尤其是在每个服务器请求包含多个要执行的读取操作时。<br /><br /> 无法满足扩展要求。|在新数据到达时消除争用。<br /><br /> 延迟较低的数据检索。<br /><br /> 最大限度缩短代码执行时间。|  
|数据库服务器中的密集的业务逻辑处理。|插入、更新和删除工作负荷。<br /><br /> 存储过程中大量的计算。<br /><br /> 读写争用。|消除争用。<br /><br /> 最大限度缩短代码执行时间，以降低延迟和提高吞吐量。|  
|低延迟。|需要典型数据库解决方案无法实现的低延迟业务事务。|消除争用。<br /><br /> 最大限度缩短代码执行时间。<br /><br /> 低延迟代码执行。<br /><br /> 高效数据检索。|  
|会话状态管理。|频繁插入、更新和点查找。<br /><br /> 来自大量无状态 web 服务器的大规模的负荷。|消除争用。<br /><br /> 高效数据检索。<br /><br /> 使用非持久表时，可选的 IO 减少或删除|  
  
 有关 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 将导致最大的性能提升的情景的详细信息，请参阅 [内存中 OLTP – 常见的工作负荷模式和迁移注意事项](http://msdn.microsoft.com/library/dn673538.aspx)。  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 将提高具有短时间运行的事务的 OLTP 中的性能。  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 将改善的编程模式包括并发情景、点查找、存在许多插入和更新的工作负荷以及存储过程中的业务逻辑。  
  
 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 相集成意味着您可以在同一个数据库中具有内存优化表以及基于磁盘的表，并且可以跨这两种类型的表进行查询。  
  
 在 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 中，对于 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 支持的 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]外围应用存在一些限制。  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 通过使用，从而实现显著的性能和可伸缩性提升：  
  
-   专为访问内存常驻数据而优化的算法。  
  
-   用于消除逻辑锁的积极并发控制。  
  
-   消除所有物理锁和闩锁的免锁对象。 执行事务性工作的线程不使用锁或闩锁进行并发控制。  
  
-   本机编译存储过程，在访问内存优化表时，其性能明显高于解释型存储过程。  
  
> [!IMPORTANT]  
>  一些对表和存储过程的语法更改将需要使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]。 有关详细信息，请参阅 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)。 在尝试将基于磁盘的表迁移到内存优化的表前，请阅读[确定表或存储过程是否应移植到内存中 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 以了解哪些表和存储过程将从 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 中受益。  
  
## <a name="in-this-section"></a>本节内容  
 本节提供有关以下概念的信息：  
  
|主题|Description|  
|-----------|-----------------|  
|[使用内存优化表的要求](memory-optimized-tables.md)|讨论使用内存优化的表的硬件和软件要求及指导原则。|  
|[在 VM 环境下使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|讨论内容包括在虚拟化环境中使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 。|  
|[内存中 OLTP 代码示例](in-memory-oltp-code-samples.md)|包含说明如何创建和使用内存优化的表的代码示例。|  
|[Memory-Optimized Tables](memory-optimized-tables.md)|介绍内存优化的表。|  
|[内存优化表变量](../../database-engine/memory-optimized-table-variables.md)|一个代码示例，其中展示如何使用内存优化的表变量代替传统的表变量以减少 tempdb 的使用次数。|  
|[内存优化表上的索引](../../database-engine/indexes-on-memory-optimized-tables.md)|介绍内存优化索引。|  
|[本机编译的存储过程](natively-compiled-stored-procedures.md)|介绍本机编译的存储过程。|  
|[管理内存中 OLTP 的内存](../../database-engine/managing-memory-for-in-memory-oltp.md)|了解和管理系统中的内存用量。|  
|[创建和管理用于内存优化对象的存储](creating-and-managing-storage-for-memory-optimized-objects.md)|论述数据和差异文件，其中存储有关内存优化的表中事务的信息。|  
|[内存优化表的备份、还原和恢复](restore-and-recovery-of-memory-optimized-tables.md)|讨论内存优化表的备份、还原和恢复。|  
|[对内存中 OLTP 的 Transact-SQL 支持](transact-sql-support-for-in-memory-oltp.md)|讨论 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 对 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]的支持。|  
|[对内存中 OLTP 数据库的高可用性支持](high-availability-support-for-in-memory-oltp-databases.md)|讨论 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]中的可用性组和故障转移群集。|  
|[SQL Server 对内存中 OLTP 的支持](sql-server-support-for-in-memory-oltp.md)|列出支持内存优化表的新增和更新的语法和功能。|  
|[迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)|论述如何将基于磁盘的表迁移到内存优化的表。|  
  
 有关 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 的详细信息，请参阅：  
  
-   [Microsoft® SQL Server® 2014 产品指南](http://www.microsoft.com/download/confirmation.aspx?id=39269)  
  
-   [内存中 OLTP 博客](http://go.microsoft.com/fwlink/?LinkId=311696)  
  
-   [内存中 OLTP - 常见的工作负荷模式和迁移注意事项](http://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [SQL Server 内存中 OLTP 内部组件概述](http://msdn.microsoft.com/library/dn720242.aspx)  
  
## <a name="see-also"></a>请参阅  
 [数据库功能](../database-features.md)  
  
  
