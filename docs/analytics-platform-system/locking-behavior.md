---
title: 锁定行为的并行数据仓库 |Microsoft Docs
description: 了解如何并行数据仓库使用锁定确保事务完整性和在多个用户同时访问数据时维护数据库的一致性。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f9862fed432036dcb4a3905fb3af1d3132349a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280893"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>并行数据仓库中的锁定行为
了解如何并行数据仓库使用锁定确保事务完整性和在多个用户同时访问数据时维护数据库的一致性。  
  
## <a name="Basics"></a>锁定的基础知识  
**模式**  
  
SQL Server PDW 支持四种锁定模式：  
  
排他  
排他锁禁止写入或读取直到持有排他锁完成的事务从锁定的对象。 排他锁在生效时允许不使用的任何模式下的任何其他锁。 例如，DROP TABLE 和 CREATE DATABASE 使用的排他锁。  
  
共享  
共享锁禁止启动受影响的对象的排他锁，但允许所有其他锁模式。 例如，SELECT 语句启动的共享锁，并因此允许多个查询同时访问所选的数据但会阻止更新到 SELECT 语句完成之前被读取的记录。  
  
ExclusiveUpdate  
使用 ExclusiveUpdate 锁禁止写入锁定的对象，但允许通过共享锁。 使用 ExclusiveUpdate 锁生效时允许不使用任何其他锁。 例如，备份数据库和还原的数据库使用的排他更新锁。  
  
SharedUpdate  
SharedUpdate 锁禁止独占和使用 ExclusiveUpdate 锁模式，并在对象上允许共享和 SharedUpdate 锁模式。 SharedUpdate 修改一个对象，但不限制读取访问到它在修改过程。 例如，插入和更新使用的 SharedUpdate 锁。  
  
**资源类**  
  
锁定对象的以下类：数据库、 架构、 对象 （表、 视图或过程），（在内部使用） 的应用程序、 EXTERNALDATASOURCE，EXTERNALFILEFORMAT 和 SCHEMARESOLUTION （数据库级别锁时创建、 更改或删除架构对象或数据库用户）。 这些对象类的对象类型列中可以出现[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)。  
  
## <a name="Remarks"></a>一般备注  
锁可以应用于数据库、 表或视图。  
  
SQL Server PDW 不实现任何可配置的隔离级别。 它支持定义的 ANSI 标准能在 READ_UNCOMMITTED 隔离级别。 但是，由于能在 READ_UNCOMMITTED 下运行操作的读取、 很少的阻塞操作实际上发生或者会导致争用系统中。  
  
SQL Server PDW 依赖于基础 SQL Server 引擎实现锁定和并发控制。 如果操作会导致同一节点内基础 SQL Server 死锁，SQL Server PDW 利用 SQL Server 死锁检测功能，并终止阻塞的语句之一。  
  
> [!NOTE]  
> SQL Server 不允许在等待锁会阻塞较新的锁请求的语句。 SQL Server PDW 尚未完全实施此过程。 SQL Server PDW 中新的共享锁的连续请求有时会阻止上一个 （但正在等待） 的排他锁请求。 例如，**更新**（需要排他锁） 的语句可能会被授予的系列的共享锁阻止**选择**语句。 若要解决阻塞的进程 (通过查看标识[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM)，停止提交新请求，直到已满足排他锁。  
  
## <a name="lock-definition-table"></a>锁定义表  
SQL Server 支持以下类型的锁。 并非所有的锁类型控制节点上可用，但可能会发生的计算节点上。  
  
-   Sch-s （架构稳定性）。 确保在任何会话持有对架构元素（例如表或索引）的架构稳定性锁时，不删除该架构元素。  
  
-   Sch-m （架构修改）。 必须由要更改指定资源架构的任何会话持有。 确保没有其他会话正在引用所指示的对象。  
  
-   S （共享）。 授予持有锁的会话对资源的共享访问权限。  
  
-   U （更新）。 指示对最终可能更新的资源获取的更新锁。 用于防止常见形式的死锁，这类死锁在多个会话锁定资源并且稍后可能更新资源时发生。  
  
-   X （排他）。 授予持有锁的会话对资源的独占访问权限。  
  
-   IS （意向共享）。 指示有意将 S 锁放置在锁层次结构中的某个从属资源上。  
  
-   IU （意向更新）。 指示有意将 U 锁放置在锁层次结构中的某个从属资源上。  
  
-   IX （意向排他）。 指示有意将 X 锁放置在锁层次结构中的某个从属资源上。  
  
-   SIU （共享意向更新）。 指示对有意在锁层次结构中的从属资源上获取更新锁的资源进行共享访问。  
  
-   六个 （共享意向排他）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源进行共享访问。  
  
-   UIX （更新意向排他）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源持有的更新锁。  
  
-   BU。 用于大容量操作。  
  
-   RangeS_S （共享键范围和共享资源锁）。 指示可串行范围扫描。  
  
-   RangeS_U （共享键范围和更新资源锁）。 指示可串行更新扫描。  
  
-   RangeI_N （插入键范围和 Null 资源锁）。 用于在将新键插入索引前测试范围。  
  
-   RangeI_S。 通过 RangeI_N 和 S 锁的重叠创建的键范围转换锁。  
  
-   RangeI_U。 通过 RangeI_N 和 U 锁的重叠创建的键范围转换锁。  
  
-   RangeI_X。 通过 RangeI_N 和 X 锁的重叠创建的键范围转换锁。  
  
-   RangeX_S。 通过 RangeI_N 和 RangeS_S 锁的重叠创建的键范围转换锁 锁。  
  
-   RangeX_U. 通过 RangeI_N 和 RangeS_U 锁的重叠创建的键范围转换锁。  
  
-   RangeX_X （排他键范围和排他资源锁）。 这是在更新范围中的键时使用的转换锁。  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
