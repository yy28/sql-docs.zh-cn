---
title: "Always On Linux 上的 SQL Server 可用性组 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c5c7e602ac1beedb028072b4c82578e9948af43d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="availability-groups-for-sql-server-on-linux"></a>适用于 Linux 上的 SQL Server 的可用性组

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server AlwaysOn 可用性组是一种高可用性 (HA)、灾难恢复 (DR) 和横向扩展的解决方案。 它在直接附加的存储上为数据库组提供高可用性。 它支持多个辅助以实现集成的高可用性和灾难恢复、自动故障检测、快速透明故障转移和读取负载均衡。 凭借此一系列广泛的功能，可以实现工作负荷的最佳可用性 SLA。

SQL Server 可用性组在 SQL Server 2012 中首次引入，并在随后的每个版本中都有所改进。 现在可以在 Linux 上使用此功能。 若要适应具有严格的业务连续性要求 SQL Server 工作负荷上所有支持, 可用性组运行[Linux 操作系统分发](sql-server-linux-release-notes.md)。 此外，使可用性组成为灵活、集成和高效的 HA DR 解决方案的所有功能也可以在 Linux 上使用。 其中包括： 

- **多数据库故障转移**可用性组支持一组用户数据库，称为可用性数据库的故障转移环境。
- **快速故障检测和故障转移**为高可用性群集中的资源，可用性组受益于内置群集智能即时故障转移检测和故障转移操作。
- **使用虚拟 IP 资源的透明故障转移**启用客户端使用单个连接字符串保存到主在故障转移。 需要与群集管理器集成。
- **多个同步和异步辅助副本**可用性组支持最多八个辅助副本。 凭借同步副本，主要副本等待提交事务，主副本等待事务写入事务日志上的磁盘中。 主要副本不会等待异步同步副本上的写入。  
- **手动或自动故障转移**故障转移到同步的辅助副本可以自动触发的群集或按需由数据库管理员。
- **活动辅助副本可用于读取和备份的工作负荷**可以配置一个或多个辅助副本，以支持对辅助数据库的只读访问和/或若要允许对辅助数据库的备份。
- **自动种子设定**SQL Server 会自动创建可用性组中的每个数据库的辅助副本。
- **只读路由**SQL Server 将传入连接路由到到配置为允许只读工作负荷的辅助副本的可用性组侦听器。 
- **数据库级别的运行状况监视和故障转移触发器**增强的数据库级别监视和诊断。 
- **灾难恢复配置**与分布式的可用性组或多子网可用性组设置。 
- **读取缩放功能**中 SQL Server 自 2017 年你可以创建可用性组和不带 HA 横向扩展只读操作。 


有关 SQL Server 可用性组的详细信息，请参阅[SQL Server Always On 可用性组](http://msdn.microsoft.com/library/hh510230.aspx)。

## <a name="availability-group-terminology"></a>可用性组术语

可用性组支持的故障转移环境适用于一组可以共同进行故障转移的离散用户数据库（称为可用性数据库）。 一个可用性组支持一组读写主要数据库以及一至八组对应的辅助数据库。 （可选）可使辅助数据库能进行只读访问和/或某些备份操作。 一个可用性组定义一个包含两个或更多故障转移伙伴（称为可用性副本）的集合。 “可用性副本”是可用性组的组件。 有关详细信息，请参阅[概述的 Alwayson 可用性组 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)。

以下术语介绍了 SQL Server 可用性组解决方案的主要部分：

 可用性组 (availability group)  
 一个容器，用于一组共同实现故障转移的数据库（“可用性数据库”）。  
  
 可用性数据库 (availability database)  
 属于可用性组的数据库。 对于每个可用性数据库，可用性组将保留一个读写副本（“主数据库”）和一个到八个只读副本（“辅助数据库”）。  
  
 主数据库 (primary database)  
 可用性数据库的读写副本。  
  
 辅助数据库 (secondary database)  
 可用性数据库的只读副本。  
  
 可用性副本  
 可用性组的实例化，该可用性组由特定的 SQL Server 实例承载，并维护属于该可用性组的每个可用性数据库的本地副本。 存在两种类型的可用性副本：一个 *主副本* 和一至八个 *辅助副本*。  
  
 主副本  
 使主数据库可用于来自客户端的读写连接并用于将每个主数据库的事务日志记录发送到每个辅助副本的可用性副本。  
  
 辅助副本 (secondary replica)  
 维护各可用性数据库的辅助副本的可用性副本，充当可用性组的潜在故障转移目标。 或者，辅助副本可以支持对辅助数据库进行只读访问，并支持对辅助数据库创建备份。  
  
 可用性组侦听器 (availability group listener)  
 一个服务器名称，客户端可连接到此服务器以访问可用性组的主副本或辅助副本中的数据库。 可用性组侦听器将传入连接定向到主副本或只读辅助副本。  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>可用性组在 SQL Server 2017 中的新增功能

SQL Server 2017 引入了可用性组的新功能。

**CLUSTER_TYPE**使用`CREATE AVAILABILITY GROUP`。 标识管理可用性组的服务器群集管理器的类型。 可以为以下类型之一：

   - **WSFC**此处 server 故障转移群集。 在 Windows 上，它是 CLUSTER_TYPE 的默认值。
   - **外部**不 Windows server 故障转移群集-例如，位于 Linux Pacemaker 使用群集管理器。
   - **无**没有群集管理器。 用于读取缩放可用性组。

有关这些选项的详细信息，请参阅[CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx)或[ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx)。

**保证在同步辅助副本上提交**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. 当`required_synchronized_secondaries_to_commit`设置为大于 0，数据库将等待，直到事务将在指定的数提交该主副本上的事务的值**同步辅助**副本数据库事务日志。 如果足够同步的辅助副本都没有联机，直到足够的辅助副本与通信恢复将拒绝所有连接到主副本。

**读取缩放可用性组**

创建不含群集的可用性组来支持读取缩放工作负荷。 请参阅[读取缩放可用性组](../database-engine/availability-groups/windows/read-scale-availability-groups.md)。

## <a name="next-steps"></a>后续步骤

[在 Linux 上的 SQL Server 配置可用性组](sql-server-linux-availability-group-configure-ha.md)

[在 Linux 上的 SQL Server 配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)

[添加可用性组群集资源在 RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[添加可用性组群集资源在 SLES](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上添加可用性组群集资源](sql-server-linux-availability-group-cluster-ubuntu.md)

