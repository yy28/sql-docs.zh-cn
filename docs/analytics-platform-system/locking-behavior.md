---
title: 锁定行为
description: 了解当多个用户同时访问数据时，并行数据仓库如何使用锁定来确保事务的完整性和保持数据库的一致性。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401000"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>并行数据仓库中的锁定行为
了解当多个用户同时访问数据时，并行数据仓库如何使用锁定来确保事务的完整性和保持数据库的一致性。  
  
## <a name="Basics"></a>锁定基础知识  
**交货**  
  
SQL Server PDW 支持四种锁定模式：  
  
排他  
独占锁定禁止对锁定的对象进行写入或读取，直到持有排他锁的事务完成。 在排他锁生效时，不允许任何模式的其他锁。 例如，DROP TABLE 和 CREATE DATABASE 使用排他锁。  
  
共享  
共享锁禁止对受影响的对象启动排他锁，但允许所有其他锁模式。 例如，SELECT 语句会启动共享锁，因而允许多个查询同时访问所选数据，但在 SELECT 语句完成之前，将阻止对读取记录进行更新。  
  
ExclusiveUpdate  
ExclusiveUpdate 锁定禁止写入锁定对象，但允许通过共享锁进行读取。 ExclusiveUpdate 锁生效时，不允许使用其他锁。 例如，备份数据库和还原数据库使用独占更新锁。  
  
SharedUpdate  
SharedUpdate 锁禁止 "独占" 和 "ExclusiveUpdate" 锁模式，并允许对象上的 "共享" 和 "SharedUpdate" 锁模式。 SharedUpdate 会修改对象，但不会在修改期间限制对该对象的读取访问。 例如，INSERT 和 UPDATE 使用 SharedUpdate 锁。  
  
**资源类**  
  
锁包含在以下对象类中：数据库、架构、对象（表、视图或过程）、应用程序（内部使用）、EXTERNALDATASOURCE、EXTERNALFILEFORMAT 和 SCHEMARESOLUTION （创建、更改或删除架构对象或数据库用户）。 这些对象类可以出现在[sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)的 object_type 列中。  
  
## <a name="Remarks"></a>一般备注  
锁定可以应用于数据库、表或视图。  
  
SQL Server PDW 不实现任何可配置的隔离级别。 它支持 ANSI 标准定义的 READ_UNCOMMITTED 隔离级别。 不过，由于读取操作是在 READ_UNCOMMITTED 下运行，因此非常少的阻塞操作实际上会发生，或者系统中会导致争用。  
  
SQL Server PDW 依赖于基础 SQL Server 引擎来实现锁定和并发控制。 如果操作导致同一节点内出现基础 SQL Server 死锁，则 SQL Server PDW 利用 SQL Server 死锁检测功能，并终止其中一个阻塞语句。  
  
> [!NOTE]  
> SQL Server 不允许正在等待锁的语句被较新的锁请求阻止。 SQL Server PDW 尚未完全实现此过程。 在 SQL Server PDW 中，对新共享锁的连续请求有时会阻止上一个（等待）请求进行排他锁。 例如，可以通过为一系列**SELECT**语句授予的共享锁来阻止**UPDATE**语句（需要排他锁）。 若要解决阻止的进程（通过[dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)查看 DVM 来识别），请停止提交新请求，直到满足排他锁。  
  
## <a name="lock-definition-table"></a>锁定定义表  
SQL Server 支持以下类型的锁。 并非所有锁类型在控制节点上都可用，但在计算节点上可能会出现这种情况。  
  
-   Sch-m-S （架构稳定性）。 确保在任何会话持有对架构元素（例如表或索引）的架构稳定性锁时，不删除该架构元素。  
  
-   Sch-m （架构修改）。 必须由要更改指定资源架构的任何会话持有。 确保没有其他会话正在引用所指示的对象。  
  
-   S （共享）。 授予持有锁的会话对资源的共享访问权限。  
  
-   U （更新）。 指示对最终可能更新的资源获取的更新锁。 用于防止常见形式的死锁，这类死锁在多个会话锁定资源并且稍后可能更新资源时发生。  
  
-   X （独占）。 授予持有锁的会话对资源的独占访问权限。  
  
-   IS （意向共享）。 指示有意将 S 锁放置在锁层次结构中的某个从属资源上。  
  
-   IU （意向更新）。 指示有意将 U 锁放置在锁层次结构中的某个从属资源上。  
  
-   IX （意向排他）。 指示有意将 X 锁放置在锁层次结构中的某个从属资源上。  
  
-   SIU （共享意向更新）。 指示对有意在锁层次结构中的从属资源上获取更新锁的资源进行共享访问。  
  
-   六个（共享意向排他）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源进行共享访问。  
  
-   UIX （更新意向排他）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源持有的更新锁。  
  
-   BU. 用于大容量操作。  
  
-   RangeS_S （共享键范围和共享资源锁）。 指示可串行范围扫描。  
  
-   RangeS_U （共享键范围和更新资源锁）。 指示可串行更新扫描。  
  
-   RangeI_N （插入键范围和 Null 资源锁）。 用于在将新键插入索引前测试范围。  
  
-   RangeI_S。 通过 RangeI_N 和 S 锁的重叠创建的键范围转换锁。  
  
-   RangeI_U。 通过 RangeI_N 和 U 锁的重叠创建的键范围转换锁。  
  
-   RangeI_X。 通过 RangeI_N 和 X 锁的重叠创建的键范围转换锁。  
  
-   RangeX_S。 通过 RangeI_N 和 RangeS_S 锁的重叠创建的键范围转换锁 住.  
  
-   RangeX_U。 通过 RangeI_N 和 RangeS_U 锁的重叠创建的键范围转换锁。  
  
-   RangeX_X （排他键范围和排他资源锁）。 这是在更新范围中的键时使用的转换锁。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
