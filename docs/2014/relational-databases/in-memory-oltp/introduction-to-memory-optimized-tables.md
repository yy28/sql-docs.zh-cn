---
title: 内存优化表简介 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff434efd0a9f4fcb3316143e598e636bff85f487
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157830"
---
# <a name="introduction-to-memory-optimized-tables"></a>内存优化表简介
  内存优化表是使用 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql) 创建的表。  
  
 内存优化表驻留在内存中。 从内存读取表中的行和将这些行写入内存。 整个表都驻留在内存中。 表数据的另一个副本维护在磁盘上，但仅用于持续性目的。  
  
 内存中 OLTP 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成，以便在所有方面（如开发、部署、可管理性和可支持性）提供无缝体验。 数据库可包含内存中对象以及基于磁盘的对象。  
  
 内存优化表中的行是版本化的。 这意味着表中的每行都可能有多个版本。 所有行版本均维护在同一个表数据结构中。 行版本控制用于实现对同一行的并发读取和写入。 有关对同一行的并发读取和写入的更多信息，请参阅 [Transactions in Memory-Optimized Tables](memory-optimized-tables.md)。  
  
 下图展示多版本控制。 该图显示了一个包含三行的表，其中，每行都有不同的版本。  
  
 ![多版本控制。](../../database-engine/media/hekaton-tables-1.gif "多版本控制。")  
  
 该表有三行：r1、r2 和 r3。 r1 有三个版本，r2 有两个版本，r3 有四个版本。 注意，同一行的不同版本不必占用连续的内存位置。 不同的行版本可分散到整个表数据结构中。  
  
 可将内存优化的表数据结构视为一个行版本集合。 基于磁盘的表中的行以页和区形式组织，各个行借助页码和页偏移量进行寻址，而内存优化表中的行版本则借助 8 字节的内存指针进行寻址。  
  
## <a name="durability"></a>持久性  
 默认情况下，内存优化的表是完全持久的，并且如同（传统的）基于磁盘的表上的事务一样，内存优化表上的完全持久的事务是完全原子、一致、隔离和持久 (ACID) 的。 内存优化的表和本机编译的存储过程支持 [!INCLUDE[tsql](../../../includes/tsql-md.md)]的一个子集。  
  
 内存中 OLTP 支持事务持续性延迟的持久表。 延迟的持久事务在提交事务后不久即保存到磁盘。 作为提高性能的代价，在服务器崩溃或故障转移过程中将丢失已提交但未保存到磁盘的事务。  
  
 除了默认持久的内存优化表之外， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还支持非持久的内存优化表，不记录这些表的日志且不在磁盘上保存它们的数据。 这意味着这些表上的事务不需要任何磁盘 IO，但如果服务器崩溃或进行故障转移，则无法恢复数据。  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>访问内存优化表中的数据  
 可通过以下两种方式访问内存优化表中的数据：  
  
-   通过解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] （本机编译存储过程之外）。 这些 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句可位于解释型存储过程内，也可以是临时 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。  
  
-   通过本机编译的存储过程。  
  
 内存优化表可以最高效地从本机编译的存储过程（[本机编译的存储过程](natively-compiled-stored-procedures.md)）访问。 还可以使用（传统的）解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)]访问内存优化表。 解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 是指在不使用本机编译的存储过程的情况下访问内存优化表。 解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 访问的一些示例包括从 DML 触发器、即席 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 批处理、视图和表值函数访问内存优化表。  
  
 下表总结了对各种对象的本机和解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 访问。  
  
|功能|使用本机编译的存储过程访问|解释型 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 访问|CLR 访问|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|内存优化表|是|是|否 <sup>1</sup>|  
|[内存优化表变量](../../database-engine/memory-optimized-table-variables.md)|是|是|否|  
|[本机编译的存储过程](https://msdn.microsoft.com/library/dn133184.aspx)|无法使用 EXECUTE 语句从本机编译的存储过程执行任意存储过程。|是|否 <sup>1</sup>|  
  
 <sup>1</sup>无法从上下文连接访问内存优化表或本机编译存储的过程 (从连接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]执行 CLR 模块时)。 但是，可以创建和打开能够访问内存优化的表和本机编译的存储过程的其他连接。 有关详细信息，请参阅[常规 vs。上下文连接](../clr-integration/data-access/context-connections-vs-regular-connections.md)。  
  
## <a name="performance-and-scalability"></a>性能和可伸缩性  
 以下因素会影响可以通过内存中 OLTP 实现的性能提升：  
  
 通信  
 与包含较少调用且每个存储过程中实现的功能较多的应用程序相比，具有许多短存储过程调用的应用程序的性能提升可能较小。  
  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 执行  
 在使用本机编译的存储过程而不是解释的存储过程或查询执行时，内存中 OLTP 实现最佳性能。 存储过程如执行其他存储过程，则无法本机编译前者，但从此类存储过程中访问内存优化的表可存在优点。  
  
 范围扫描与点查找  
 内存优化的非聚集索引支持范围扫描和有序扫描。 对于点查找，内存优化的哈希索引具有比内存优化的非聚集索引更好的性能。 内存优化的非聚集索引具有比基于磁盘的索引更好的性能。  
  
 索引操作不记入日志并且只存在于内存中。  
  
 并发  
 在性能受引擎级别并发（如闩锁争用或阻塞）影响的应用程序迁移到内存中 OLTP 时，其性能会显著提高。  
  
 下表列出了关系数据库中常见的性能和可伸缩性问题以及内存中 OLTP 提高性能的方式。  
  
|问题|内存中 OLTP 影响|  
|-----------|----------------------------|  
|性能<br /><br /> 资源（CPU、I/O、网络或内存）使用率较高。|CPU<br /> 本机编译的存储过程可大幅降低 CPU 使用率，因为此类存储过程执行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句所需的指令比解释型存储过程少得多。<br /><br /> 内存中 OLTP 可以帮助减少扩展工作负荷时的硬件投资，因为一台服务器可提供五到十台服务器的吞吐量。<br /><br /> I/O<br /> 如果在处理数据或索引页方面遇到 I/O 瓶颈，则内存中 OLTP 可缓解瓶颈现象。 此外，内存中 OLTP 对象的检查点编号是连续的，不会导致 I/O 操作突然增多。 但是，如果对性能至关重要的表的工作集不能容纳于内存中，则内存中 OLTP 不会提高性能，因为它需要数据驻留在内存中。 如果在日志记录方面遇到 I/O 瓶颈，则内存中 OLTP 可缓解瓶颈现象，因为它进行的日志记录操作较少。 如果将一个或多个内存优化的表配置为非持久的表，您可以消除数据的日志记录。<br /><br /> 内存<br /> 内存中 OLTP 不会提供任何性能优势。 内存中 OLTP 可能会对内存产生额外的压力，因为这些对象需要驻留在内存中。<br /><br /> 网络<br /> 内存中 OLTP 不会提供任何性能优势。 数据需要从数据层传输到应用层。|  
|可伸缩性<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 应用程序中的大多数伸缩问题是由并发问题（如锁、闩锁和旋转锁中的争用）引起的。|闩锁争用<br /> 典型情况是按键顺序并发插入行时索引的最后一页上的争用。 由于内存中 OLTP 在访问数据时不采用闩锁，因此可完全消除与闩锁争用相关的可伸缩性问题。<br /><br /> 旋转锁争用<br /> 由于内存中 OLTP 在访问数据时不采用闩锁，因此可完全消除与旋转锁争用相关的可伸缩性问题。<br /><br /> 与锁定相关的争用<br /> 如果数据库应用程序遇到读操作与写操作之间的阻塞问题，则内存中 OLTP 可消除这些阻塞问题，因为它使用新的乐观并发控制形式来实现所有事务隔离级别。 内存中 OLTP 不使用 TempDB 来存储行版本。<br /><br /> 如果伸缩问题是由两个写操作之间的冲突（例如，两个并发事务尝试更新相同的行）引起的，则内存中 OLTP 会让其中一个事务成功，而让另一个事务失败。 必须显式或隐式重新提交失败的事务，从而重试该事物。 在任一情况下，您都需要对应用程序进行更改。<br /><br /> 如果应用程序遇到两个写操作之间的频繁冲突，则会减小乐观锁定的值。 该应用程序不适用于内存中 OLTP。 除非冲突是由锁升级引起的，否则大多数 OLTP 应用程序没有写冲突。|  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](in-memory-oltp-in-memory-optimization.md)  
  
  
