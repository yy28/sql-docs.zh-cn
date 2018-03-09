---
title: "管理可用性组故障转移-在 Linux 上的 SQL Server |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 086cf16e243810452a3bace411abdc3689e74ff8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="always-on-availability-group-failover-on-linux"></a>在 Linux 上的 alwayson 可用性组故障转移

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在上下文中的可用性组 (AG) 的主角色和辅助角色的可用性副本都通常可互换的过程称为故障转移。 存在三种故障转移形式：自动故障转移（无数据丢失）、计划的手动故障转移（无数据丢失）和强制手动故障转移（可能丢失数据）。最后一种形式通常称为“强制故障转移”。 自动和计划的手动故障转移保留所有数据。 可用性组在可用性副本级别进行故障转移。 也就是说，可用性组故障转移到其辅助副本 （当前故障转移目标） 之一。 

有关故障转移的背景信息，请参阅[故障转移和故障转移模式](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。

## <a name="failover"></a>手动故障转移

使用群集管理工具进行故障转移可用性组管理的外部群集管理器。 例如，如果解决方案使用 Pacemaker 管理的 Linux 群集，则使用`pcs`在 RHEL 或 Ubuntu 上执行手动故障转移。 在 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在正常操作中，请勿使用 Transact-SQL 或 SQL Server 管理工具（如 SSMS 或 PowerShell）进行故障转移。 当`CLUSTER_TYPE = EXTERNAL`，仅可接受的值`FAILOVER_MODE`是`EXTERNAL`。 借助这些设置，所有手动或自动故障转移操作都由外部群集管理器执行。 有关强制故障转移可能丢失数据的说明，请参阅[强制故障转移](#forceFailover)。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手动故障转移步骤

若要故障转移，将成为主副本的辅助副本必须同步。 如果辅助副本是异步的[更改的可用性模式](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)。

手动故障转移中两个步骤。

   首先，[手动故障转移移动可用性组资源](#manualMove)从拥有这些资源来对新节点的群集节点。

   群集故障转移的可用性组资源，并将位置约束添加。 此约束配置要在新节点上运行的资源。 为了成功地故障转移在将来删除此约束。

   第二个，[删除的位置约束](#removeLocConstraint)。

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">步骤 1。 手动故障转移移动可用性组资源

若要手动故障转移可用性组资源名称为*ag_cluster*到名为的群集节点*nodeName2*，运行于你的分发的相应命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 示例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>手动故障转移资源后，你需要删除自动添加的位置约束。

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 步骤 2。 删除位置约束

在手动故障转移，期间`pcs`命令`move`或`crm`命令`migrate`添加针对要放置在新的目标节点上的资源的位置约束。 若要查看新约束，请在手动移动资源后运行以下命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES 示例**

   ```bash
   crm config show
   ```

因此，将来的故障转移-包括自动故障转移-成功，请删除该位置约束。 

若要删除该约束，请运行以下命令： 

- **RHEL/Ubuntu 示例**

   在此示例中`ag_cluster-master`是故障转移的资源的名称。 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES 示例**

   在此示例中`ag_cluster`是故障转移的资源的名称。 

   ```bash
   crm resource clear ag_cluster
   ```

或者，可以运行以下命令删除位置约束。  

- **RHEL/Ubuntu 示例**

   在以下命令中，`cli-prefer-ag_cluster-master` 是需要删除的约束的 ID。 `sudo pcs constraint --full` 会返回此 ID。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **SLES 示例**

   在下面的命令`cli-prefer-ms-ag_cluster`是约束的 ID。 `crm config show` 会返回此 ID。 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>自动故障转移不会添加位置约束，因此不需要进行清除。 

详细信息：
- [Red Hat - 管理群集资源](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker-手动移动资源](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES 管理指南-资源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> 强制故障转移 

强制故障转移严格限制用于灾难恢复。 在这种情况下，你无法故障转移群集管理工具与因为主数据中心已关闭。 如果您强制故障转移到某一未同步的辅助副本，则可能会丢失一些数据。 如果您必须立即将服务还原到可用性组，并且愿意承担丢失数据的风险，仅强制故障转移。

如果无法进行交互与群集-例如，使用群集管理工具，如果群集中的主数据中心的灾难事件由于停止响应，你可能需要强制故障转移，以绕过的外部群集管理器。 此过程不建议正常操作因为风险数据丢失。 在群集管理工具无法执行故障转移操作时，请使用它。 就功能而言，此过程非常类似于[执行强制的手动故障转移](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)在 Windows 中的可用性组上。
 
强制故障转移此过程是特定于在 Linux 上的 SQL Server。

1. 验证可用性组资源不由管理群集更。 

      - 在目标群集节点上设置到非托管模式的资源。 此命令发出信号停止资源监视和管理资源代理。 例如： 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 如果未能将资源模式设置为非托管模式，请删除该资源。 例如：

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >当您删除某个资源时，它也会删除所有关联的约束。 

1. 在承载辅助副本的 SQL Server 实例中，设置会话上下文变量`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 故障转移使用 Transact SQL 可用性组。 在以下示例中，将`<MyAg>`替换为你的可用性组的名称。 连接到托管目标次要副本的 SQL Server 实例，并运行以下命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  强制故障转移后，将可用性组到正常状态之前重新启动的群集资源监视和管理或重新创建可用性组资源。 查看[强制故障转移后的重要任务](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)。

1.  请重新启动群集资源监视和管理：

   若要重新启动的群集资源监视和管理，请运行以下命令：

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   如果你删除群集资源，重新创建它。 要重新创建群集资源，请遵循的说明[创建可用性组资源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。

>[!Important]
>不要为灾难恢复练习中使用前面的步骤，因为它们的危险数据丢失。 而是更改异步副本添加到同步和的说明[正常的手动故障转移](#manualFailover)。

## <a name="database-level-monitoring-and-failover-trigger"></a>数据库级别监视和故障转移触发器

有关`CLUSTER_TYPE=EXTERNAL`，故障转移触发器语义是不同相比 WSFC。 在 WSFC 中的 SQL Server 实例上可用性组时，转换外`ONLINE`状态的数据库会导致可用性组运行状况报告错误。 在响应中，群集管理器将触发故障转移操作。 在 Linux 上，SQL Server 实例不能与群集通信。 监视以完成操作数据库运行状况*外而内*。 如果用户选择用于监视数据库级别的故障转移和故障转移 (通过设置选项`DB_FAILOVER=ON`创建可用性组时)，群集将检查数据库状态是否为`ONLINE`每次它运行监视的操作时。 群集查询中的状态`sys.databases`。 不同于任何状态`ONLINE`，自动 （如果满足自动故障转移条件），它将触发故障转移。 故障转移的实际时间取决于监视操作的频率以及 sys.databases 中正在更新的数据库状态。

自动故障转移要求至少一个同步副本。

## <a name="next-steps"></a>后续步骤

[配置 SQL Server 可用性组群集资源的 Red Hat Enterprise Linux 群集](sql-server-linux-availability-group-cluster-rhel.md)

[为 SQL Server 可用性组群集资源配置 SUSE Linux Enterprise Server 群集](sql-server-linux-availability-group-cluster-sles.md)

[配置 SQL Server 可用性组群集资源的 Ubuntu 群集](sql-server-linux-availability-group-cluster-ubuntu.md)
