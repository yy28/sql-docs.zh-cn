---
title: 使用 SQL Server 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
caps.latest.revision: 47
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 14bcf7edf62b499c5a50beb73ea8526c67807dc3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125393"
---
# <a name="use-sql-server-objects"></a>使用 SQL Server 对象
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了对象和计数器，系统监视器可以使用它们监视运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机中的活动。 对象可以是任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 锁或 Windows 进程。 每个对象有一个或多个计数器，用于确定所要监视对象的各方面信息。 例如， **SQL Server Locks** 对象包含名为 **Number of Deadlocks/sec** 和 **Lock Timeouts/sec**的计数器。  
  
 如果计算机上有某一个给定资源类型的多个资源，则一些对象会有几个实例。 例如，如果一个系统有多个处理器，则 **Processor** 对象类型会有多个实例。 对于 **上的每个数据库，** Databases [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象类型都有一个实例。 某些对象类型（例如， **Memory Manager** 对象）只有一个实例。 如果一个对象类型有多个实例，则可以增加计数器以跟踪每个实例的统计信息，另外在许多情况下，同时跟踪所有实例的统计信息。 默认实例计数器以 SQLServer:\<对象名称> 格式显示。 命名实例计数器以 MSSQL$\<实例名>:\<计数器名称> 或 SQLAgent$\<实例名>:\<计数器名称> 格式显示****。  
  
 通过在图表中添加或删除计数器并保存图表设置，可以指定系统监视器启动后监视的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象和计数器。  
  
 可以配置系统监视器显示任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计数器中的统计信息。 另外，可以为任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计数器设置一个阈值，当计数器超过阈值时生成一个警报。 有关设置警报的详细信息，请参阅 [创建 SQL Server 数据库警报](create-a-sql-server-database-alert.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例后，才会显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 统计信息。 如果停止并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，统计信息的显示将中断，然后自动恢复。 还请注意，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 没有运行，您也会在系统监视器管理单元中看到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计数器。 在群集实例中，性能计数器只在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行的节点上发挥作用。  
  
 本主题包含以下各节：  
  
-   [SQL Server 代理性能对象](#SQLServerAgentPOs)  
  
-   [Service Broker 性能对象](#ServiceBrokerPOs)  
  
-   [SQL Server 性能对象](#SQLServerPOs)  
  
-   [SQL Server 复制性能对象](#SQLServerReplicationPOs)  
  
-   [SSIS 管道计数器](#SsisPipelineCounters)  
  
-   [所需的权限](#RequiredPermissions)  
  
##  <a name="SQLServerAgentPOs"></a> SQL Server 代理性能对象  
 下表列出了为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理提供的性能对象：  
  
|性能对象|Description|  
|------------------------|-----------------|  
|[SQLAgent:Alerts](sql-server-agent-alerts-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报的信息。|  
|[SQLAgent:Jobs](sql-server-agent-jobs-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的信息。|  
|[SQLAgent:JobSteps](sql-server-agent-jobsteps-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的信息。|  
|[SQLAgent:Statistics](sql-server-agent-statistics-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的常规信息。|  
  
##  <a name="ServiceBrokerPOs"></a> Service Broker 性能对象  
 下表列出了为 [!INCLUDE[ssSB](../../includes/sssb-md.md)]代理提供的性能对象：  
  
|性能对象|Description|  
|------------------------|-----------------|  
|[SQLServer:Broker Activation](sql-server-broker-activation-object.md)|提供有关已激活 [!INCLUDE[ssSB](../../includes/sssb-md.md)]的任务的信息。|  
|[SQLServer:Broker Statistics](sql-server-broker-statistics-object.md)|提供 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的常规信息。|  
|[SQLServer:Broker Transport](sql-server-broker-dbm-transport-object.md)|提供有关 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 网络的信息。|  
  
##  <a name="SQLServerPOs"></a> SQL Server 性能对象  
 下表介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象：  
  
|性能对象|Description|  
|------------------------|-----------------|  
|[SQLServer:Access Methods](sql-server-access-methods-object.md)|搜索并度量 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象的分配（例如，索引搜索数或分配给索引和数据的页数）。|  
|[SQLServer:Backup Device](sql-server-backup-device-object.md)|提供有关备份和还原操作使用的备份设备的信息，如备份设备的吞吐量。|  
|[SQLServer:Buffer Manager](sql-server-buffer-manager-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的内存缓冲区的信息，如 **freememory** 和 **buffer cache hit ratio**。|  
|[SQL Server:Buffer Node](sql-server-buffer-node.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 请求和访问可用页的频率的信息。|  
|[SQLServer:CLR](sql-server-clr-object.md)|提供有关公共语言运行时 (CLR) 的信息。|  
|[SQLServer:Cursor Manager by Type](sql-server-cursor-manager-by-type-object.md)|提供游标信息。|  
|[SQLServer:Cursor Manager Total](sql-server-cursor-manager-total-object.md)|提供游标信息。|  
|[SQLServer:Database Mirroring](sql-server-database-mirroring-object.md)|提供有关数据库镜像的信息。|  
|[SQLServer:Databases](sql-server-databases-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的信息，如可用的日志空间量或数据库中的活动事务数。 这个对象可有多个实例。|  
|[SQL Server:Deprecated Features](sql-server-deprecated-features-object.md)|对使用不推荐使用的功能的次数进行计数。|  
|[SQLServer:Exec Statistics](sql-server-execstatistics-object.md)|提供了有关执行统计信息的信息。|  
|[SQLServer:General Statistics](sql-server-general-statistics-object.md)|提供有关服务器范围内的常规活动的信息，如连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的用户数。|  
|[SQL Server：HADR 可用性副本](sql-server-availability-replica.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 可用性副本的信息。|  
|[SQL Server：HADR 数据库副本](sql-server-database-replica.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 数据库副本的信息。|  
|[SQLServer:Latches](sql-server-latches-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所用内部资源（如数据库页）上的闩锁的信息。|  
|[SQLServer:Locks](sql-server-locks-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行的单个锁请求的信息，如锁超时和死锁。 这个对象可有多个实例。|  
|[SQLServer:Memory Manager](sql-server-memory-manager-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存使用量的信息，如当前分配的锁结构总数。|  
|[SQLServer:Plan Cache](sql-server-plan-cache-object.md)|提供有关用于存储对象（如存储过程、触发器和查询计划）的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 缓存的信息。|  
|[SQLServer: Resource Pool Stats](sql-server-resource-pool-stats-object.md)|提供了有关资源调控器资源池统计的信息。|  
|[SQLServer:SQL Errors](sql-server-sql-errors-object.md)|提供有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的信息。|  
|[SQLServer:SQL Statistics](sql-server-sql-statistics-object.md)|提供有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询各个方面的信息，如 [!INCLUDE[tsql](../../includes/tsql-md.md)] 收到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句的批数。|  
|[SQLServer:Transactions](sql-server-transactions-object.md)|提供了有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中活动事务的信息，如事务总数和快照事务数。|  
|[SQLServer:User Settable](sql-server-user-settable-object.md)|执行自定义监视。 每个计数器可以是一个自定义的存储过程，也可以是任何返回一个被监视值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。|  
|[SQLServer: Wait Statistics](sql-server-wait-statistics-object.md)|提供有关等待的信息。|  
|[SQLServer: Workload Group Stats](sql-server-workload-group-stats-object.md)|提供了有关资源调控器工作负荷组统计的信息。|  
  
##  <a name="SQLServerReplicationPOs"></a> SQL Server 复制性能对象  
 下表列出了为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制提供的性能对象：  
  
|性能对象|Description|  
|------------------------|-----------------|  
|**SQLServer:Replication Agents**<br /><br /> **SQLServer:Replication Snapshot**<br /><br /> **SQLServer:Replication Logreader**<br /><br /> **SQLServer:Replication Dist.**<br /><br /> **SQLServer:Replication Merge**<br /><br /> 有关详细信息，请参阅 [Monitoring Replication with System Monitor](../replication/monitor/monitoring-replication-with-system-monitor.md)。|提供有关复制代理活动的信息。|  
  
##  <a name="SsisPipelineCounters"></a> SSIS 管道计数器  
 有关 **SSIS 管道** 计数器的信息，请参阅 [性能计数器](../../integration-services/performance/performance-counters.md)。  
  
##  <a name="RequiredPermissions"></a> 所需的权限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的使用取决于 Windows 权限（ **SQLAgent:Alerts**除外）。 只有 **sysadmin** 固定服务器角色的成员可以使用 **SQLAgent:Alerts**。  
  
## <a name="see-also"></a>请参阅  
 [使用性能对象](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
