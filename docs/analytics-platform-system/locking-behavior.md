---
title: "锁定行为 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c55c636e-b767-4a0c-8184-be991a10801f
caps.latest.revision: "27"
ms.openlocfilehash: c1cb1b0ec346ff18d40a3ac03e7ba45b37666c98
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="locking-behavior"></a>锁定行为
SQL Server PDW 使用锁定来确保事务完整性并在多个用户同时访问数据时维护数据库的一致性。  
  
## <a name="Basics"></a>锁定的基础知识  
**模式**  
  
SQL Server PDW 支持四种锁定模式：  
  
排他  
排他锁禁止写入或读取事务持有排他锁完成之前从锁定的对象。 实际上排他锁时允许不使用的任何模式的任何其他锁。 例如，DROP TABLE 和 CREATE DATABASE 使用的排他锁。  
  
共享  
共享锁禁止启动的受影响的对象的排他锁，但允许所有其他锁定模式。 例如，SELECT 语句启动的共享锁，并因此允许多个查询来同时，访问所选的数据，但阻止对 SELECT 语句完成之前所读取的记录更新。  
  
ExclusiveUpdate  
ExclusiveUpdate 锁禁止写入到锁定的对象，但允许通过共享锁。 实际上 ExclusiveUpdate 锁定时允许不使用任何其他锁。 例如，备份数据库和还原的数据库使用的排他更新锁。  
  
SharedUpdate  
SharedUpdate 锁禁止独占和 ExclusiveUpdate 锁定模式，并允许该对象上的共享和 SharedUpdate 锁定模式。 SharedUpdate 修改的对象，但不限制读取访问权限到它在修改过程。 例如，插入和更新使用 SharedUpdate 锁。  
  
**资源类**  
  
锁定持续时间对象在以下类： 数据库、 架构、 对象 （表、 视图或过程）、 （在内部使用） 的应用程序、 EXTERNALDATASOURCE、 EXTERNALFILEFORMAT 和 SCHEMARESOLUTION (数据库级别锁定拍摄时创建，更改，或删除架构对象或数据库用户）。 中的对象类型列才会显示这些对象类[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)。  
  
## <a name="Remarks"></a>一般备注  
锁可以应用于数据库、 表或视图。  
  
SQL Server PDW 不实现任何可配置的隔离级别。 按照的 ANSI 标准的定义，它支持 READ_UNCOMMITTED 隔离级别。 但是，因为读取操作在 READ_UNCOMMITTED 下运行，非常少的阻止操作实际发生或导致系统中的争用。  
  
SQL Server PDW 依赖于基础的 SQL Server 引擎，若要实现锁定和并发控制。 如果操作导致同一节点内基础 SQL Server 死锁，SQL Server PDW 利用 SQL Server 死锁检测功能，并终止正在阻塞的语句之一。  
  
> [!NOTE]  
> SQL Server 不允许在等待锁可以被阻塞的较新的锁请求的语句。 SQL Server PDW 尚未完全实施此过程。 SQL Server PDW 中对新的共享锁的连续请求有时可能会阻止以前 （但正在等待） 的排他锁请求。 例如，**更新**（需要的排他锁） 的语句可能会被授予一系列的共享锁阻止**选择**语句。 若要解决阻塞的进程 (通过查看标识[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM)，停止提交新请求，直到已满足排他锁。  
  
## <a name="lock-definition-table"></a>锁定义表  
SQL Server 支持以下类型的锁。 并非所有的锁类型都位于管理节点中，但无法在计算节点上发生。  
  
-   Sch-S （架构稳定性）。 确保在任何会话持有对架构元素（例如表或索引）的架构稳定性锁时，不删除该架构元素。  
  
-   Sch-M （架构修改）。 必须由要更改指定资源架构的任何会话持有。 确保没有其他会话正在引用所指示的对象。  
  
-   S （共享）。 授予持有锁的会话对资源的共享访问权限。  
  
-   U （更新）。 指示对最终可能更新的资源获取的更新锁。 用于防止常见形式的死锁，这类死锁在多个会话锁定资源并且稍后可能更新资源时发生。  
  
-   X （独占）。 授予持有锁的会话对资源的独占访问权限。  
  
-   IS （意向共享）。 指示有意将 S 锁放置在锁层次结构中的某个从属资源上。  
  
-   IU （意向更新）。 指示有意将 U 锁放置在锁层次结构中的某个从属资源上。  
  
-   IX （意向排它）。 指示有意将 X 锁放置在锁层次结构中的某个从属资源上。  
  
-   SIU （共享意向更新）。 指示对有意在锁层次结构中的从属资源上获取更新锁的资源进行共享访问。  
  
-   六个 （共享意向排他）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源进行共享访问。  
  
-   UIX （更新意向排它）。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源持有的更新锁。  
  
-   BU。 用于大容量操作。  
  
-   RangeS_S （共享键范围和共享资源锁）。 指示可串行范围扫描。  
  
-   RangeS_U （共享键范围和更新资源锁）。 指示可串行更新扫描。  
  
-   RangeI_N （插入键范围和 Null 资源锁）。 用于在将新键插入索引前测试范围。  
  
-   RangeI_S。 通过 RangeI_N 和 S 锁的重叠创建的键范围转换锁。  
  
-   RangeI_U。 通过 RangeI_N 和 U 锁的重叠创建的键范围转换锁。  
  
-   RangeI_X。 通过 RangeI_N 和 X 锁的重叠创建的键范围转换锁。  
  
-   RangeX_S。 通过 RangeI_N 和 RangeS_S 锁的重叠创建的键范围转换锁 锁。  
  
-   RangeX_U。 通过 RangeI_N 和 RangeS_U 锁的重叠创建的键范围转换锁。  
  
-   RangeX_X （排他键范围和排他资源锁）。 这是在更新范围中的键时使用的转换锁。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
