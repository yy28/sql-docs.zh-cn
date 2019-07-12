---
title: 管理可用性组故障转移-Linux 上的 SQL Server
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: f758b70e0b518418a95a79ebb4e9b7322f33f31f
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834252"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Linux 上的 always On 可用性组故障转移

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在可用性组 (AG) 的上下文中，主角色和辅助可用性副本的角色是通常可互换的过程称为故障转移。 存在三种故障转移形式：自动故障转移（无数据丢失）、计划的手动故障转移（无数据丢失）和强制手动故障转移（可能丢失数据）。最后一种形式通常称为“强制故障转移”  。 自动和计划的手动故障转移会保留所有数据。 在可用性副本级别将 AG 故障转移。 也就是说，AG 故障转移到其中一个辅助副本 （当前故障转移目标）。 

有关故障转移的背景信息，请参阅[故障转移和故障转移模式](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。

## <a name="failover"></a>手动故障转移

使用群集管理工具进行故障转移 AG 由外部群集管理器管理。 例如，如果解决方案使用 Pacemaker 管理 Linux 群集，使用`pcs`RHEL 或 Ubuntu 上执行手动故障转移。 在 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在正常操作中，请勿使用 Transact-SQL 或 SQL Server 管理工具（如 SSMS 或 PowerShell）进行故障转移。 当`CLUSTER_TYPE = EXTERNAL`，仅可接受的值`FAILOVER_MODE`是`EXTERNAL`。 借助这些设置，所有手动或自动故障转移操作都由外部群集管理器执行。 若要强制故障转移可能丢失数据的说明，请参阅[强制故障转移](#forceFailover)。

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">手动故障转移步骤

若要故障转移，将成为主副本的辅助副本必须同步。 如果辅助副本是异步的[更改的可用性模式](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)。

手动故障转移在两个步骤。

   首先，[手动故障转移将 AG 资源移](#manualMove)从拥有到新节点的资源的群集节点。

   在群集故障转移可用性组资源，并且添加位置约束。 此约束配置要在新节点上运行的资源。 为了成功地故障转移在将来删除此约束。

   第二个，[删除位置约束](#removeLocConstraint)。

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">第 1 步。 手动故障转移移动可用性组资源

若要手动故障转移一个名为可用性组资源*ag_cluster*到群集节点名为*nodeName2*，运行于分发版的相应命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 示例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>手动故障转移资源后，你需要删除位置约束，会自动添加。

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> 第 2 步。 删除位置约束

在手动故障转移期间`pcs`命令`move`或`crm`命令`migrate`添加新的目标节点上放置的资源的位置约束。 若要查看新约束，请在手动移动资源后运行以下命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs constraint list --full
   ```

- **SLES 示例**

   ```bash
   crm config show
   ```

约束的手动故障转移而创建的示例。 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **RHEL/Ubuntu 示例**

   在以下命令中，`cli-prefer-ag_cluster-master` 是需要删除的约束的 ID。 `sudo pcs constraint list --full` 会返回此 ID。 
   
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
- [Red Hat - 管理群集资源](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker-手动移动资源](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_manually_moving_resources_around_the_cluster.html)
 [SLES 管理指南-资源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> 强制故障转移 

强制故障转移严格限制用于灾难恢复。 在这种情况下，您无法故障转移群集管理工具与因为主数据中心处于断开状态。 如果您强制故障转移到某一未同步的辅助副本，则可能会丢失一些数据。 如果您必须立即将服务还原到可用性组，并且愿意承担丢失数据的风险，仅强制故障转移。

如果不能使用群集管理工具与群集-例如，进行交互，如果群集不响应由于灾难事件中的主数据中心，您可能需要强制故障转移，以绕过外部群集管理器。 此过程不被建议用于常规操作，因为数据丢失的风险。 在群集管理工具无法执行故障转移操作时，请使用它。 就功能而言，此过程非常类似于[执行强制手动故障转移](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)AG 在 Windows 上。
 
有关强制故障转移此过程是特定于 Linux 上的 SQL Server。

1. 验证可用性组资源不由管理群集任何更多。 

      - 在目标群集节点上设置为非托管模式的资源。 此命令向发出信号停止资源监视和管理的资源代理。 例如： 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - 如果未能将资源模式设置为非托管模式，请删除该资源。 例如：

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >当你删除某个资源时，还将删除所有关联的约束。 

1. 在承载辅助副本的 SQL Server 实例中，设置会话上下文变量`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 使用 Transact SQL AG 故障转移。 在以下示例中，将为`<MyAg>`在可用性组的名称。 连接到托管目标次要副本的 SQL Server 实例，并运行以下命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  在强制故障转移后将可用性组恢复到正常状态之前重新启动的群集资源监视和管理或重新创建可用性组资源。 审阅[强制故障转移后的重要任务](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp)。

1.  请重新启动群集资源监视和管理：

   若要重新启动的群集资源监视和管理，请运行以下命令：

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   如果你删除群集资源，重新创建它。 若要重新创建群集资源，请按照的说明[创建可用性组资源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。

>[!Important]
>不要为灾难恢复演练中使用上述步骤，因为它们可能会丢失数据。 而是更改异步副本添加到同步的及其使用说明[正常的手动故障转移](#manualFailover)。

## <a name="database-level-monitoring-and-failover-trigger"></a>数据库级别监视和故障转移触发器

有关`CLUSTER_TYPE=EXTERNAL`，故障转移触发器语义会不同于 WSFC。 当可用性组的 WSFC 中的 SQL Server 实例上时，转换带`ONLINE`状态将在数据库会导致可用性组运行状况报告错误。 在响应中，群集管理器将触发故障转移操作。 在 Linux 上，SQL Server 实例不能与群集通信。 监视数据库运行状况*由外而内*。 如果用户选择的数据库级别的故障转移监视和故障转移 (通过将选项设置`DB_FAILOVER=ON`创建可用性组时)，群集将检查数据库状态是否`ONLINE`每次运行监视操作。 群集查询中的状态`sys.databases`。 不同于任何状态`ONLINE`，它将触发故障转移，自动 （如果满足自动故障转移条件）。 故障转移的实际时间取决于监视操作的频率以及 sys.databases 中正在更新的数据库状态。

自动故障转移要求至少一个同步副本。

## <a name="next-steps"></a>后续步骤

[配置 SQL Server 可用性组群集资源的 Red Hat Enterprise Linux 群集](sql-server-linux-availability-group-cluster-rhel.md)

[为 SQL Server 可用性组群集资源配置 SUSE Linux Enterprise Server 群集](sql-server-linux-availability-group-cluster-sles.md)

[配置 Ubuntu 群集 SQL Server 可用性组群集资源](sql-server-linux-availability-group-cluster-ubuntu.md)
