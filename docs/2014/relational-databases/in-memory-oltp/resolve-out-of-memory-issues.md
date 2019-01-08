---
title: 解决内存不足问题 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9588b40fa253c3866ab0e7f7ce328edf22aa1789
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364829"
---
# <a name="resolve-out-of-memory-issues"></a>解决内存不足问题
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 相比， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 随着需求的不断增加，为 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 安装和分配的内存量可能会不足。 这时内存就会不足。 本主题介绍如何从 OOM 情况恢复。 有关可帮助你避免很多 OOM 情况的指南，请参阅 [内存使用情况的监视和故障排除](monitor-and-troubleshoot-memory-usage.md) 。  
  
## <a name="covered-in-this-topic"></a>本主题的内容  
  
|主题|概述|  
|-----------|--------------|  
|[解决 OOM 导致的数据库还原故障](resolve-out-of-memory-issues.md#bkmk_resolverecoveryfailures)|收到错误消息“由于资源池 '\<resourcePoolName>' 内存不足，数据库 '\<databaseName>' 的还原操作失败”时应采取的操作。|  
|[消除工作负荷的低内存或 OOM 情况的影响](resolve-out-of-memory-issues.md#bkmk_recoverfromoom)|发现内存不足问题对性能产生负面影响时应采取的操作。|  
|[在提供足够内存时，解决由于内存不足导致的页分配失败问题](resolve-out-of-memory-issues.md#bkmk_pageallocfailure)|收到错误消息“由于资源池 '\<resourcePoolName>' 内存不足，不允许对数据库 '\<databaseName>' 进行页分配”时应采取的操作。 ……”当可用内存足以进行操作时。|  
  
##  <a name="bkmk_resolveRecoveryFailures"></a> 解决 OOM 导致的数据库还原故障  
 尝试还原数据库时，可能会收到错误消息："还原的数据库操作失败*\<databaseName >* 由于资源池内存不足*\<resourcePoolName >*'。"必须先通过使更多内存可用来解决内存不足问题，然后才能成功还原数据库。  
  
 若要解决 OOM 导致的还原故障，请使用以下任何或所有方法以便增加可用内存，来暂时增加可用于恢复操作的内存。  
  
-   临时关闭正在运行的应用程序。   
    通过关闭一个或多个正在运行的应用程序，如 Visual Studio、Internet Explorer、OneNote 等，可以将它们使用的内存用于还原操作。 您可以在成功还原后重新启动这些应用程序。  
  
-   增加 MAX_MEMORY_PERCENT 值。   
    此代码段将资源池 PoolHk 的 MAX_MEMORY_PERCENT 更改为所安装内存的 70%。  
  
    > [!IMPORTANT]  
    >  如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 设置为与 MAX_MEMORY_PERCENT 相同的值。   
    > 有关详细信息，请参阅主题[最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)有关详细信息。  
  
    ```tsql  
  
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
  
     有关 MAX_MEMORY_PERCENT 最大值的信息，请参阅主题部分 [可用于内存优化表和索引的内存百分比](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
-   重新配置**最大服务器内存**。  
    有关如何配置**最大服务器内存**[使用内存配置选项优化服务器性能](https://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx)  
  
##  <a name="bkmk_recoverFromOOM"></a> 消除工作负荷的低内存或 OOM 情况的影响  
 当然，最好不要出现低内存或 OOM（内存不足）情况。 好的计划和监视有助于避免 OOM 情况。 但再好的计划也并不总能预见实际情况，最后仍有可能遇到低内存或 OOM 情况。 从 OOM 恢复有两个步骤：  
  
1.  [打开 DAC（专用管理员连接）](resolve-out-of-memory-issues.md#bkmk_opendac)  
  
2.  [采取纠正措施](resolve-out-of-memory-issues.md#bkmk_takecorrectiveaction)  
  
###  <a name="bkmk_openDAC"></a> 打开 DAC（专用管理员连接）  
 Microsoft SQL Server 提供了专用管理员连接 (DAC)。 即使服务器对其他客户端连接停止响应，管理员也可以使用 DAC 访问正在运行的 SQL Server 数据库引擎实例来排除服务器上的故障。 DAC 可通过 `sqlcmd` 实用工具和 SQL Server Management Studio (SSMS) 获得。  
  
 有关如何使用 `sqlcmd` 和 DAC 的指南，请参阅 [使用专用管理员连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。 有关通过 SSMS 使用 DAC 的指南，请参阅[如何：使用 SQL Server Management Studio 中使用专用的管理员连接](https://msdn.microsoft.com/library/ms178068.aspx)。  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 采取纠正措施  
 要处理 OOM 情况，需要通过减少使用量释放现有内存，或者为内存中表提供更多可用内存。  
  
#### <a name="free-up-existing-memory"></a>释放现有内存  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>删除不重要的内存优化表行并等待垃圾收集  
 您可以删除内存优化表中不重要的行。 垃圾收集器将这些行使用的内存返回可用内存 . 内存中 OLTP 引擎能够积极回收垃圾。 但是，长时间运行的事务可能会妨碍垃圾收集。 例如，如果有一个事务运行 5 分钟，在事务活动期间，无法对所有因更新/删除操作而创建的行版本进行垃圾收集。  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>将一行或多行移到基于磁盘的表  
 下面的 TechNet 文章提供有关将行从内存优化表移到基于磁盘的表的指导。  
  
-   [应用程序级分区](https://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [用于对内存优化表进行分区的应用程序模式](https://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>增加可用内存  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>增加资源池的 MAX_MEMORY_PERCENT 值  
 如果尚未为内存中表创建命名资源池，应该创建一个，并将 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 数据库与其绑定。 有关如何创建并将 [数据库与资源池绑定的指南，请参阅主题](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) 将具有内存优化表的数据库绑定至资源池 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 。  
  
 如果 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 数据库绑定至资源池，可以增加资源池可访问的内存百分比。 有关如何更改资源池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 值的指南，请参阅子主题 [更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 。  
  
 增加 MAX_MEMORY_PERCENT 值。   
此代码段将资源池 PoolHk 的 MAX_MEMORY_PERCENT 更改为所安装内存的 70%。  
  
> [!IMPORTANT]  
>  如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 设置为相同值。   
> 有关详细信息，请参阅主题[最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)有关详细信息。  
  
```tsql  
  
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
  
 有关 MAX_MEMORY_PERCENT 最大值的信息，请参阅主题部分 [可用于内存优化表和索引的内存百分比](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
##### <a name="install-additional-memory"></a>安装更多内存  
 如果可能，最终的最佳解决方案是安装更多物理内存。 这时，请注意，还是可以增加 MAX_MEMORY_PERCENT 的值（请参阅子主题[更改现有池的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)），因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能不需要更多内存，当新安装的内存不能都用于此资源池时，这可以得到最好的效果。  
  
> [!IMPORTANT]  
>  如果服务器在虚拟机上运行，并且不是专用服务器，请将 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 设置为相同值。   
> 有关详细信息，请参阅主题[最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)有关详细信息。  
  
##  <a name="bkmk_PageAllocFailure"></a> 在提供足够内存时，解决由于内存不足导致的页分配失败问题  
 如果收到错误消息"不允许为数据库分配页面 '*\<databaseName >* 由于资源池内存不足*\<resourcePoolName >*'. 请参阅<https://go.microsoft.com/fwlink/?LinkId=330673>有关详细信息。" ，这可能是因为禁用了资源调控器。 在资源调控器被禁用时，MEMORYBROKER_FOR_RESERVE 导致虚假内存压力。  
  
 若要解决此问题，您需要启用资源调控器。  
  
 有关使用对象资源管理器、资源调控器属性或 Transact-SQL 启用资源调控器的限制和局限以及指导的信息，请参阅 [启用资源调控器](https://technet.microsoft.com/library/bb895149.aspx) 。  
  
## <a name="see-also"></a>请参阅  
 [管理内存中 OLTP 的内存](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [内存使用情况的监视和故障排除](monitor-and-troubleshoot-memory-usage.md)   
 [数据库与资源池绑定的指南，请参阅主题](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [最佳做法：在虚拟机环境中使用内存中 OLTP](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
