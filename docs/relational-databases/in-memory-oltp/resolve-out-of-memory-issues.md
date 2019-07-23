---
title: 解决内存不足问题 | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a2dd428c7f035cf73e679bbd6c47e78f1f745457
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111822"
---
# <a name="resolve-out-of-memory-issues"></a>解决内存不足问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 相比， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 随着需求的不断增加，为 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 安装和分配的内存量可能会不足。 这时内存就会不足。 本主题介绍如何从 OOM 情况恢复。 有关可帮助你避免很多 OOM 情况的指南，请参阅 [内存使用情况的监视和故障排除](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) 。  
  
## <a name="covered-in-this-topic"></a>本主题的内容  
  
|主题|概述|  
|-----------|--------------|  
|[解决 OOM 导致的数据库还原故障](#bkmk_resolveRecoveryFailures)|收到错误消息“由于资源池 '\<resourcePoolName>' 内存不足，数据库 '  \<databaseName>  ' 的还原操作失败”时应采取的操作。|  
|[消除工作负荷的低内存或 OOM 情况的影响](#bkmk_recoverFromOOM)|发现内存不足问题对性能产生负面影响时应采取的操作。|  
|[在提供足够内存时，解决由于内存不足导致的页分配失败问题](#bkmk_PageAllocFailure)|收到错误消息“由于资源池 '\<resourcePoolName>  ' 内存不足，不允许对数据库 '\<databaseName>  ' 进行页分配”时应采取的操作。 ……”当可用内存足以进行操作时。|
|[在 VM 环境下使用内存中 OLTP 的最佳做法](#bkmk_VMs)|在虚拟化环境中使用内存中 OLTP 需要注意的内容。|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> 解决 OOM 导致的数据库还原故障  
 尝试还原数据库时，可能会收到错误消息：“由于资源池‘\<databaseName>’内存不足，数据库‘\<resourcePoolName>’的还原操作失败。”   这表明服务器没有足够的可用内存来还原数据库。 
   
将数据库还原到的服务器必须有足够的可用内存用于数据库备份中的内存优化表，否则数据库不会联机，并且会被标记为可疑。  
  
如果服务器具有足够的物理内存，但仍然显示此错误，则可能是其他进程正在使用过多内存或配置问题导致没有足够的内存可用于还原。 对于此类问题，请采取以下措施，为还原操作留出更多可用内存： 
  
-   临时关闭正在运行的应用程序。   
    通过关闭一个或多个正在运行的应用程序，或停止目前不需要的服务，可以将它们使用的内存用于还原操作。 您可以在成功还原后重新启动这些应用程序。  
  
-   增加 MAX_MEMORY_PERCENT 值。   
    如果数据库 [绑定到资源池](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)（这是最佳做法），可用于还原的内存将由 MAX_MEMORY_PERCENT 控制。 如果值太低，还原将失败。 此代码段将资源池 PoolHk 的 MAX_MEMORY_PERCENT 更改为所安装内存的 70%。  
  
    > [!IMPORTANT]  
    > 如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 设置为与 MAX_MEMORY_PERCENT 相同的值。   
    > 有关详细信息，请参阅主题 [在 VM 环境下使用内存中 OLTP 的最佳做法](#bkmk_VMs)。  
  
    ```sql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     有关 MAX_MEMORY_PERCENT 最大值的信息，请参阅主题部分 [可用于内存优化表和索引的内存百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
-   增加 **最大服务器内存**。  
    有关配置 max server memory 的信息，请参阅主题[“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  。  
  
##  <a name="bkmk_recoverFromOOM"></a> 消除工作负荷的低内存或 OOM 情况的影响  
 当然，最好不要出现低内存或 OOM（内存不足）情况。 好的计划和监视有助于避免 OOM 情况。 但再好的计划也并不总能预见实际情况，最后仍有可能遇到低内存或 OOM 情况。 从 OOM 恢复有两个步骤：  
  
1.  [打开 DAC（专用管理员连接）](#bkmk_openDAC)  
  
2.  [采取纠正措施](#bkmk_takeCorrectiveAction)  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

###  <a name="bkmk_openDAC"></a> 打开 DAC（专用管理员连接）  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了专用管理员连接 (DAC)。 即使服务器对其他客户端连接停止响应，管理员也可以使用 DAC 访问正在运行的 SQL Server 数据库引擎实例来排除服务器上的故障。 `sqlcmd` 实用工具和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都包含 DAC。  
  
 有关通过 SSMS 或 `sqlcmd` 使用 DAC 的指导，请参阅[用于数据库管理员的诊断连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 采取纠正措施  
 要处理 OOM 情况，需要通过减少使用量释放现有内存，或者为内存中表提供更多可用内存。  
  
#### <a name="free-up-existing-memory"></a>释放现有内存  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>删除不重要的内存优化表行并等待垃圾收集  
 您可以删除内存优化表中不重要的行。 垃圾收集器将这些行使用的内存返回可用内存 内存中 OLTP 引擎能够积极回收垃圾。 但是，长时间运行的事务可能会妨碍垃圾收集。 例如，如果有一个事务运行 5 分钟，在事务活动期间，无法对所有因更新/删除操作而创建的行版本进行垃圾收集。  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>将一行或多行移到基于磁盘的表  
 下面的 TechNet 文章提供有关将行从内存优化表移到基于磁盘的表的指导。  
  
-   [应用程序级分区](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [用于对内存优化表进行分区的应用程序模式](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>增加可用内存  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>增加资源池的 MAX_MEMORY_PERCENT 值  
 如果尚未为内存中表创建命名资源池，应该创建一个，并将 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 数据库与其绑定。 有关如何创建并将 [数据库与资源池绑定的指南，请参阅主题](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) 将具有内存优化表的数据库绑定至资源池 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 。  
  
 如果 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 数据库绑定至资源池，可以增加资源池可访问的内存百分比。 有关如何更改资源池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 值的指南，请参阅子主题 [更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 。  
  
 增加 MAX_MEMORY_PERCENT 值。   
此代码段将资源池 PoolHk 的 MAX_MEMORY_PERCENT 更改为所安装内存的 70%。  
  
> [!IMPORTANT]  
>  如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 设置为相同值。   
> 有关详细信息，请参阅主题 [在 VM 环境下使用内存中 OLTP 的最佳做法](#bkmk_VMs)。  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 有关 MAX_MEMORY_PERCENT 最大值的信息，请参阅主题部分 [可用于内存优化表和索引的内存百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
##### <a name="install-additional-memory"></a>安装更多内存  
 如果可能，最终的最佳解决方案是安装更多物理内存。 这时，请注意，还是可以增加 MAX_MEMORY_PERCENT 的值（请参阅子主题[更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)），因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能不需要更多内存，当新安装的内存不能都用于此资源池时，这可以得到最好的效果。  
  
> [!IMPORTANT]  
>  如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 设置为相同值。   
> 有关详细信息，请参阅主题 [在 VM 环境下使用内存中 OLTP 的最佳做法](#bkmk_VMs)。  
  
##  <a name="bkmk_PageAllocFailure"></a> 在提供足够内存时，解决由于内存不足导致的页分配失败问题  
 如果可用物理内存足以分配页时，在错误日志中收到错误消息 `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'https://go.microsoft.com/fwlink/?LinkId=330673' for more information.`，可能是因为禁用了 Resource Governor。 在资源调控器被禁用时，MEMORYBROKER_FOR_RESERVE 导致虚假内存压力。  
  
 若要解决此问题，您需要启用资源调控器。  
  
 有关使用对象资源管理器、资源调控器属性或 Transact-SQL 启用资源调控器的限制和局限以及指导的信息，请参阅 [启用资源调控器](../../relational-databases/resource-governor/enable-resource-governor.md) 。  
 
## <a name="bkmk_VMs"></a>在 VM 环境下使用内存中 OLTP 的最佳做法
服务器虚拟化可以帮助你改进应用程序配置、维护、可用性和备份/恢复流程，进而降低 IT 资本和运营成本并提高 IT 效率。 由于近年来的技术进步，可以更轻松地使用虚拟化来合并复杂的数据库工作负载。 本主题说明了在虚拟化环境中使用 SQL Server 内存中 OLTP 的最佳做法。

### <a name="memory-pre-allocation"></a>内存预先分配
对于虚拟化环境中的内存，更好的性能和增强的支持是两个重要的注意事项。 您必须能够根据不同虚拟机的要求（高峰负载和非高峰负载）快速将内存分配到虚拟机，同时确保不浪费内存。 通过 Hyper-V 动态内存功能，可以更灵活地在主机上运行的虚拟机之间分配和管理内存。

当虚拟化带有内存优化表的数据库时，需要修改一些用于虚拟化和管理 SQL Server 的最佳做法。 对于不带有内存优化表的数据库，可遵循两个最佳做法：
-  如果使用 min server memory，最好只分配需要的内存量，以便保留足够内存以用于其他进程（从而避免分页）。
-  不要将内存预先分配值设置得过高。 否则，其他进程可能无法在需要时获得足够内存，这可能会导致内存分页。

如果在数据库带有内存优化表时遵循上述做法，尝试还原和恢复数据库可能会导致数据库处于“恢复挂起”状态，即使你拥有可恢复数据库的足够内存时也是如此。 原因在于，与动态内存分配功能将内存分配至数据库相比，内存中 OLTP 在启动时以更主动的方式将数据存入内存。

### <a name="resolution"></a>解决方法
要缓解此问题，请将足够内存预先分配至数据库以恢复或重新启动数据库，而不要分配最小值，依靠动态内存在需要时分配更多内存。
  
## <a name="see-also"></a>另请参阅  
 [管理内存中 OLTP 的内存](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [内存使用情况的监视和故障排除](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [数据库与资源池绑定的指南，请参阅主题](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [内存管理体系结构指南](../../relational-databases/memory-management-architecture-guide.md)  
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
