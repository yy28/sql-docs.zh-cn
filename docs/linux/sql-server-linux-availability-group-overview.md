---
title: Always On Linux 上的 SQL Server 可用性组 |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: cec05fbb83bf3b86babfa26df619ebc8f9a2a34d
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671283"
---
# <a name="always-on-availability-groups-on-linux"></a>Always On Linux 上的可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍在基于 Linux 的 Always On 可用性组 (Ag) 的特征[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安装。 它还介绍了 Linux 和 Windows Server 故障转移群集 (WSFC) 之间的差异-基于 Ag。 请参阅[基于 Windows 的文档](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)有关的基本知识的 Ag，在 Windows 和 Linux 除外 WSFC 上处理相同。

从高层次的角度来看，可用性组下[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上是相同的基于 WSFC 的实现上。 这意味着，所有的限制和功能相同，有一些例外情况。 主要区别包括：

-   在 Linux 中不支持 Microsoft 分布式事务处理协调器 (DTC) [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您的应用程序需要使用分布式事务，并且需要 AG，部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Windows 上。
-   基于 Linux 的部署而不是 WSFC 使用 Pacemaker。
-   与大多数配置中的 Ag 在 Windows 上的工作组群集方案除外，Pacemaker 从不需要 Active Directory 域服务 (AD DS)。
-   如何将故障从一个节点到另一个 AG 是 Linux 和 Windows 之间的差异。
-   某些设置，例如`required_synchronized_secondaries_to_commit`只能更改通过 Pacemaker 在 Linux 上，而基于 WSFC 的安装使用 Transact SQL。

## <a name="number-of-replicas-and-cluster-nodes"></a>副本和群集节点数

在 AG[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]可以有两个总副本： 一个主节点和一个辅助数据库的仅用于可用性目的。 它不能用于任何其他内容，例如可读的查询。 在 AG[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]可以具有最多九个总副本： 一个主要和多达八个辅助数据库，其中最多三 （包括主数据库） 可以是同步的。 如果使用的基础群集，可以有 16 个节点总数最多涉及 Corosync 时。 可用性组可以跨最多有九个具有 16 个节点[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]，另外两个[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。

要求能够自动故障转移到另一个副本的两个副本配置需要仅配置副本，请使用如中所述[仅配置副本和仲裁](#configuration-only-replica-and-quorum)。 中引入了仅配置副本[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]累积更新 1 (CU1)，因此，应该部署此配置的最小版本。

如果使用 Pacemaker，则它必须正确配置使其保持启动并运行。 这意味着，仲裁和 STONITH 必须加以正确实现从 Pacemaker 的角度看，除了任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]要求，如仅配置副本。

可读辅助副本仅在使用支持[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。

## <a name="cluster-type-and-failover-mode"></a>群集类型和故障转移模式

为新[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是 Ag 群集类型的介绍。 对于 Linux，有两个有效的值：External 和 None。 外部群集类型是指，将可用性组的下方使用 Pacemaker。 使用外部群集类型需要故障转移模式也设置为 External (中的其他新增[!INCLUDE[sssql17-md](../includes/sssql17-md.md)])。 支持自动故障转移，但与不同的 WSFC 故障转移模式设置为 External，不自动使用 Pacemaker 时。 与不同的 WSFC 后配置可用性组创建可用性组的 Pacemaker 部分。

群集类型为 None 意味着，没有任何要求，也不将可用性组使用，Pacemaker。 即使在配置了Pacemaker的服务器上，如果AG配置的群集类型为None，Pacemaker将不会看到或管理该AG。 为无群集类型仅支持从主以手动方式故障转移到辅助副本。 读取横向扩展方案，以及升级为主要面向具有无创建 AG。 尽管它可以运行灾难恢复或其中任何自动故障转移所需的本地可用性等方案中，不建议。 侦听器情景也是更复杂而无需 Pacemaker。

群集类型存储在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]动态管理视图 (DMV) `sys.availability_groups`，在列中`cluster_type`和`cluster_type_desc`。

## <a name="requiredsynchronizedsecondariestocommit"></a>所需\_同步\_辅助副本\_到\_提交

熟悉[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是一个设置，由名为 Ag `required_synchronized_secondaries_to_commit`。 这将告知可用性组必须与主数据库保持同步的辅助副本数目。 这使诸如自动故障转移 （仅当与 Pacemaker 群集类型为外部集成），并控制等，主数据库的可用性的行为，如果适当数量的次要副本是联机还是脱机。 若要了解有关此工作原理的详细信息，请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 `required_synchronized_secondaries_to_commit`值是默认情况下设置和维护的 Pacemaker / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 您可以手动重写此值。

组合`required_synchronized_secondaries_to_commit`新的序列号 (这存储在`sys.availability_groups`) 通知 Pacemaker 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，例如，可能发生自动故障转移。 在这种情况下，辅助副本将具有相同的序列号的主数据库，这意味着它最新的最新的所有配置信息。

有三个值可以为设置`required_synchronized_secondaries_to_commit`:0、 1 或 2。 它们控制在副本变得不可用时所发生的行为。 数字对应于必须与主数据库同步的辅助副本数目。 行为，如下所示是 Linux 下：

-   0-辅助副本不需要与主数据库同步状态。 如果不同步的辅助数据库，但是也会有任何自动故障转移。 
-   1-一个辅助副本必须位于与主; 同步状态可以自动故障转移。 可用次要同步副本之前，主数据库不可用。
-   2 的在三个或多个节点可用性组配置中两个辅助副本必须与主; 同步可以自动故障转移。

`required_synchronized_secondaries_to_commit` 控制不只同步副本，但数据丢失的故障转移行为。 值为 1 或 2，辅助副本时始终需要同步，因此始终将数据冗余。 这意味着不会丢失数据。

若要更改的值`required_synchronized_secondaries_to_commit`，使用以下语法：

>[!NOTE]
>更改的值会导致资源来重新启动，这意味着短暂的中断。 若要避免此问题的唯一方式是设置管理的资源不是由群集暂时。

**Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

其中*AGResourceName*是针对可用性组中，配置的资源的名称和*值*是 0、 1 或 2。 若要将其设置回默认值为 Pacemaker 管理参数，执行相同的语句不带有任何值。

满足以下条件时，可能会自动故障转移的可用性组：

-   主副本和辅助副本设置为同步数据移动。
-   辅助数据库已同步 （不同步），这意味着两个位于相同的数据点的状态。
-   群集类型设置为外部。 自动故障转移不能为无群集类型。
-   `sequence_number`的辅助副本成为主数据库具有最高的序列号-即，在辅助副本的`sequence_number`从原始主副本相匹配。

如果满足这些条件承载主副本的服务器发生故障，可用性组将更改为同步副本的所有权。 同步副本的行为 (的其中可能有三个总： 一个主节点和两个辅助副本) 可进一步控制通过`required_synchronized_secondaries_to_commit`。 这适用于 Ag 上 Windows 和 Linux，但配置完全不同。 在 Linux 上，通过 AG 资源本身上的群集自动配置的值。

## <a name="configuration-only-replica-and-quorum"></a>仅配置副本和仲裁

中的其他新增[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]截至 CU1 是仅配置副本。 因为 Pacemaker 不同于 WSFC，尤其是当涉及到仲裁和需要 STONITH，拥有只需两个节点配置时将不工作涉及到 AG。 对于 FCI，提供的 Pacemaker 仲裁机制可能没有什么问题，因为在群集层进行所有 FCI 故障转移仲裁。 为 AG，发生在 Linux 下的约束性仲裁[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，所有元数据的存储位置。 这是仅配置副本派上用场。

而无需任何其他内容，第三个节点和至少一个同步的副本将所需。 仅配置副本的可用性组配置中的其他副本相同的 master 数据库中存储的可用性组配置。 仅配置副本不具有参与可用性组的用户数据库。 配置数据从主要以同步方式发送。 无论它们是自动还是手动在故障转移过程，然后使用此配置数据。

为维持仲裁并启用自动故障转移的外部群集类型 AG，它是必须：

-   有三个同步副本 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]仅); 或
-   有两个副本 （主要和辅助），以及仅配置副本。

是否使用外部，可能会发生手动故障转移或无群集可用性组配置的类型。 在可以使用的群集类型为 None 的 AG 配置仅配置副本，不建议，因为它使部署变得复杂。 这些配置中，手动修改`required_synchronized_secondaries_to_commit`具有至少为 1，一个值，以便在至少一个同步的副本。

仅配置副本可以承载在任何版本的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，其中包括[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。 这将授权成本降至最低并确保它适用于在 Ag [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。 这意味着第三个需要服务器只需要满足的最小规范[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，因为它未收到针对可用性组的用户事务流量。

使用仅配置副本时，它具有以下行为：

-   默认情况下，`required_synchronized_secondaries_to_commit`设置为 0。 这可以手动修改为 1 如果所需的。
-   如果主要副本发生故障和`required_synchronized_secondaries_to_commit`为 0，则辅助副本将成为新主数据库，可用于读取和写入。 如果值为 1，自动故障转移时，将发生，但将不接受新事务，直到另一个副本处于联机状态。
-   如果辅助副本失败和`required_synchronized_secondaries_to_commit`为 0，主副本仍会接受的事务，但如果主此时失败，则不保护数据和可能的故障转移 （手动或自动），因为辅助副本不可用。
-   如果仅配置副本失败，AG 会正常运行，但没有自动故障转移的情况。
-   如果同步的辅助副本和仅配置副本失败，主数据库不能接受的事务，并且没有地方主到失败。

在 CU1 没有已知的 bug 中通过生成 corosync.log 文件中的日志记录`mssql-server-ha`。 如果辅助副本不能有多个可用的所需副本为主，当前消息指出"预期接收 1 的序列号，但仅接收 2。 没有足够的副本处于联机状态以安全地将升级本地副本。" 应撤消数字，并且它应该显示为"预期接收 2 序列号，但仅接收 1。 没有足够的副本处于联机状态以安全地将升级本地副本。" 

## <a name="multiple-availability-groups"></a>多个可用性组 

每个 Pacemaker 群集或一组服务器，可以创建多个可用性组。 唯一的限制是系统资源。 可用性组所有权是由主机所示。 可由不同节点; 拥有不同的 Ag并非所有需要在同一节点上运行它们。

## <a name="drive-and-folder-location-for-databases"></a>数据库的驱动器和文件夹位置

与在基于 Windows 的 Ag 上加入可用性组的用户数据库的驱动器和文件夹结构应相同。 例如，如果用户数据库位于`/var/opt/mssql/userdata`服务器 A 上，在同一个文件夹中应位于服务器 b。唯一的例外部分所述[与基于 Windows 的可用性组和副本互操作性](#interoperability-with-windows-based-availability-groups-and-replicas)。

## <a name="the-listener-under-linux"></a>在 Linux 下侦听器

侦听器是 AG 的可选功能。 它适用于所有连接 （读/写主副本和/或只读的辅助副本） 上提供单一入口点，以便应用程序和最终用户不需要知道哪个服务器承载数据。 在 WSFC 中，这是网络名称资源和随后在 AD DS （如果需要） 中注册的 IP 资源的组合以及 DNS。 与可用性组资源本身组合，它提供了该抽象。 有关侦听器的详细信息，请参阅[侦听器、 客户端连接和应用程序故障转移](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)。

在 Linux 下的侦听器配置不同，但其功能是相同的。 Pacemaker 中的网络名称资源没有概念，也不在 AD DS; 中创建为对象没有只是在可以在任何节点运行的 Pacemaker 中创建的 IP 地址资源。 需要创建的 DNS 中具有"友好名称"的侦听器 IP 资源与关联的条目。 侦听器的 IP 资源只会在承载该可用性组的主副本的服务器上活动。

如果使用 Pacemaker，并且创建与侦听器相关联的 IP 地址资源，将有短暂的中断的 IP 地址在一台服务器上停止并启动其他，如是否自动或手动故障转移。 尽管这提供了通过单一名称和 IP 地址的组合的抽象，它不会屏蔽中断。 应用程序必须能够通过某种形式的检测到这种并重新连接的功能处理断开连接。

但是，DNS 名称和 IP 地址的组合是仍不足以提供对 WSFC 上的侦听程序提供，例如，对辅助副本的只读路由的所有功能。 "侦听器"在配置可用性组时，仍需要为其配置中[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 这可在该向导，以及 TRANSACT-SQL 语法。 有两种方法，这可以将配置为在功能与在 Windows 上相同：

-   IP 地址与"侦听器"中创建的外部群集类型 AG，关联[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应为 Pacemaker 中创建的资源的 IP 地址。
-   对于群集类型 none 创建 AG，使用与主副本关联的 IP 地址。

然后与提供的 IP 地址关联的实例将成为只读路由请求从应用程序之类的内容的处理协调器。

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>与基于 Windows 的可用性组和副本互操作性 

在群集类型为 External 或其中一个是 WSFC 可用性组不能具有跨平台及其副本。 这是 true 可用性组是否[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]或[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。 这意味着，使用基础群集的传统可用性组配置中，一个副本不能为 WSFC 和 Pacemaker 使用 Linux 上其他。

为无群集类型 AG 可以具有其副本跨 OS 边界，因此在同一 AG 中可能有两个基于 Linux 和 Windows 的副本。 其中主要副本是基于 Windows 的辅助数据库上的 Linux 分发版之一时，一个示例是如下所示。

![混合 None](./media/sql-server-linux-availability-group-overview/image1.png)

分布式的 AG 也可以跨越 OS 边界。 基础 Ag 绑定的规则及其配置方式，例如使用外部被配置为仅限 Linux 的但无法使用 WSFC 配置联接到可用性组。 请看下面的示例：

![混合 Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>后续步骤
[Linux 上的 SQL Server 配置可用性组](sql-server-linux-availability-group-configure-ha.md)

[Linux 上的 SQL Server 配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)

[在 RHEL 上添加可用性组群集资源](sql-server-linux-availability-group-cluster-rhel.md)

[在 SLES 上添加可用性组群集资源](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上添加可用性组群集资源](sql-server-linux-availability-group-cluster-ubuntu.md)

[配置跨平台可用性组](sql-server-linux-availability-group-cross-platform.md)

