---
title: 将具有内存优化表的数据库绑定至资源池 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 635dabe67e8311d71097e445523de2be0974bc35
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537099"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>将具有内存优化表的数据库绑定至资源池
  资源池表示可以管理的物理资源的子集。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库绑定到默认资源池并使用其中的资源。 为保护 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，防止一个或多个内存优化表使用其资源，以及防止其他内存使用者使用内存优化表需要的内存，建议对具有内存优化表的数据库创建单独的资源池来管理内存使用情况。  
  
 一个数据库只能绑定至一个资源池。 不过您可以将多个数据库绑定至同一个资源池。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许将没有内存优化表的数据库绑定到资源池，但它不会有任何影响。 如果在将来您想要在数据库中创建内存优化表，则可能要将数据库绑定到某一命名的资源池。  
  
 在将数据库绑定到资源池之前，数据库和资源池必须已经存在。 下次该数据库联机时，此绑定生效。 有关详细信息，请参阅 [Database States](../databases/database-states.md) 。  
  
 有关资源池的信息，请参阅 [Resource Governor Resource Pool](../resource-governor/resource-governor-resource-pool.md)。  
  
## <a name="steps-to-bind-a-database-to-a-resource-pool"></a>将数据库绑定至资源池的步骤  
  
1.  [创建数据库和资源池](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_createpool)  
  
    1.  [创建数据库](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_createdatabase)  
  
    2.  [确定 MIN_MEMORY_PERCENT 的 MAX_MEMORY_PERCENT 的最小值](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_determinepercent)  
  
    3.  [创建一个资源池并配置内存](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_createresourcepool)  
  
2.  [将数据库绑定到池](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_definebinding)  
  
3.  [确认绑定](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_confirmbinding)  
  
4.  [使绑定生效](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_makebindingeffective)  
  
 本主题中的其他内容  
  
-   [更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_changeallocation)  
  
-   [可用于内存优化表和索引的内存百分比](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_percentavailable)  
  
##  <a name="bkmk_CreatePool"></a> 创建数据库和资源池  
 您可以按任意顺序创建数据库和资源池。 要注意的是，在将数据库绑定至资源池前，它们必须都已存在。  
  
###  <a name="bkmk_CreateDatabase"></a> 创建数据库  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 创建一个名为 IMOLTP_DB 的数据库，它将包含一个或多个内存优化表。 路径 \<driveAndPath> 必须在运行此命令前就存在。  
  
```tsql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
###  <a name="bkmk_DeterminePercent"></a> 确定 MIN_MEMORY_PERCENT 的 MAX_MEMORY_PERCENT 的最小值  
 在确定了内存优化表所需的内存后，确定所需的可用内存的百分比，并且将内存百分比设置为该值或更高值。  
  
 **例如：**   
对于此示例，我们将假定根据您的计算，确定了您的内存优化表和索引需要 16 GB 的内存。 假定您已提交了 32 GB 的内存供您使用。  
  
 乍看起来，可能需要将 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 设置为 50（16 是 32 的 50%）。  但是，这不会向您的内存优化表提供足够的内存。 通过查看下表（[可用于内存优化表和索引的内存百分比](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_percentavailable)），我们可以看到，如果有 32 GB 的已提交内存，则只有该内存量的 80% 可用于内存优化表和索引。  因此，我们基于可用内存量而不是已提交内存来计算最小和最大百分比。  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 插入实际数量：   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 因此，您需要至少 62.5% 的可用内存量来满足您的内存优化表和索引的 16 GB 要求。  因为 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值必须是整数，所以，我们将它们设置为至少 63%。  
  
###  <a name="bkmk_CreateResourcePool"></a> 创建一个资源池并配置内存  
 为内存优化表配置内存时，应基于 MIN_MEMORY_PERCENT 而非 MAX_MEMORY_PERCENT 完成容量规划。  有关 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的信息，请参阅 [ALTER RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/alter-resource-pool-transact-sql)。 对于内存优化表，这将提高内存可用性的可预测性，因为 MIN_MEMORY_PERCENT 会对其他资源池带来内存压力以确保其得到遵守。 为确保内存可用并帮助避免内存不足情况，MIN_MEMORY_PERCENT 与 MAX_MEMORY_PERCENT 的值应相同。 请参阅下面的 [可用于内存优化表和索引的内存百分比](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_percentavailable) ，以了解基于已提交内存量的可用于内存优化表的内存百分比。  
  
 有关在虚拟机环境下工作时的详细信息，请参阅[最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)时在虚拟机环境中工作的详细信息。  
  
 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码创建一个名为 Pool_IMOLTP 且可使用一半内存的资源池。  创建该池后，资源调控器重新配置为包括 Pool_IMOLTP。  
  
```tsql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bkmk_DefineBinding"></a> 将数据库绑定到池  
 使用系统函数 `sp_xtp_bind_db_resource_pool` 将数据库绑定到资源池。 该函数使用两个参数：数据库名称和资源池名称。  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定义数据库 IMOLTP_DB 与资源池 Pool_IMOLTP 的绑定。 该绑定要到数据库联机后才生效。  
  
```tsql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 系统函数 sp_xtp_bind_db_resourece_pool 使用两个字符串参数：database_name 和 pool_name。  
  
##  <a name="bkmk_ConfirmBinding"></a> 确认绑定  
 确认绑定，记录 IMOLTP_DB 的资源池 ID。 它不应为 NULL。  
  
```tsql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
##  <a name="bkmk_MakeBindingEffective"></a> 使绑定生效  
 将数据库绑定至资源池后，必须使数据库脱机后再恢复联机以使绑定生效。 如果在先前数据库已绑定至另一资源池，此操作将移除之前的资源池中分配的内存，内存优化表和索引的内存分配现在来自与数据库新绑定的资源池。  
  
```tsql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 现在数据库已绑定至资源池。  
  
##  <a name="bkmk_ChangeAllocation"></a> 更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT  
 如果您将附加内存添加到服务器，或者添加内存优化表更改所需的内存量，则可能需要更改 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值。 以下步骤演示了如何更改资源池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值。 有关要用于 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值的指导信息，请参阅下面的部分。  有关详细信息，请参阅主题[最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)有关详细信息。  
  
1.  使用 `ALTER RESOURCE POOL` 可更改 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 的值。  
  
2.  使用 `ALTER RESURCE GOVERNOR` 可用新值重新配置资源调控器。  
  
 **示例代码**  
  
```tsql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
##  <a name="bkmk_PercentAvailable"></a> 可用于内存优化表和索引的内存百分比  
 如果将包含内存优化表的数据库和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作负荷映射到同一资源池，资源调控器会为 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 设置一个内部使用阈值，使资源池用户不产生资源使用冲突。 一般来说， [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 使用阈值约为资源池的 80%。 下表列出了不同内存大小的实际阈值。  
  
 在为 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 数据库创建专用资源池时，您需要在考虑行版本和数据增长后估计内存中表所需的物理内存量。 在估计所需的内存后，你将使用 DMV `sys.dm_os_sys_info` 中“committed_target_kb”列所反映的针对 SQL 实例的提交目标内存所占用的百分比，创建一个资源池（请参阅 [sys.dm_os_sys_info](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql)）。 例如，您可以将可供实例使用的总内存的 40% 用来创建资源池 P1。 在此 40% 之外， [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 引擎将获取一个较小的百分比来存储 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 数据。  这样做是为了确保 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 不会占用来自该池的所有内存。  这个较小的百分比值依赖于目标提交内存。 下表描述在引发 OOM 错误之前在资源池（命名资源池或默认资源池）中可用于 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 数据库的内存。  
  
|目标提交内存|可用于内存中表的百分比|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 例如，如果“目标提交内存”为 100 GB，并且估计内存优化表和索引需要 60GB 的内存，则可以使用 MAX_MEMORY_PERCENT = 67（需要的 60GB / 0.90 = 66.667GB – 化整为 67GB；67GB / 安装的 100GB = 67%）创建一个资源池，以便确保 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 对象具有其需要的 60GB。  
  
 在数据库已绑定到某一命名资源池后，使用以下查询可查看跨不同资源池分配的内存。  
  
```tsql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 此示例输出显示，内存优化对象使用的内存在资源池 PoolIMOLTP 中为 1356 MB，上限为 2307 MB。 此上限控制可由映射到此池的用户和系统内存优化对象使用的总内存。  
  
 **示例输出**   
此输出来自我们在上面创建的数据库和表。  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 有关详细信息，请参阅 [sys.dm_resource_governor_resource_pools (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)。  
  
 如果未将数据库绑定到某一命名资源池，则它将绑定到“默认”池。 由于对于大多数其他分配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用默认资源池，因此，对于感兴趣的数据库，您将不能使用 DMV sys.dm_resource_governor_resource_pools 精确监视内存优化表使用的内存。  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_xtp_bind_db_resource_pool (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)   
 [资源调控器](../resource-governor/resource-governor.md)   
 [Resource Governor Resource Pool](../resource-governor/resource-governor-resource-pool.md)   
 [创建资源池](../resource-governor/create-a-resource-pool.md)   
 [更改资源池设置](../resource-governor/change-resource-pool-settings.md)   
 [删除资源池](../resource-governor/delete-a-resource-pool.md)  
  
  
