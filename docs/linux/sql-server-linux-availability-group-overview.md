---
title: "Always On 可用性组在 Linux 上的 SQL server |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: bfd36553e4ac30b6d551e60cde02d57a7eec8fbc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Always On Linux 上的可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南介绍了在基于 Linux 的 Alwayson 可用性组 （承载个可用性组） 的特征[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安装。 它还介绍了 Linux 和 Windows Server 故障转移群集 (WSFC) 之间的差异的基于承载个可用性组。 请参阅[基于 Windows 的文档](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)的基础知识的承载个可用性组，因为他们处理的相同 Windows 和 Linux WSFC 除外。

高级的角度来看，从可用性组下[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上相同与它们时基于 WSFC 的实现上实现。 这意味着所有的限制和功能都相同，但出现一些异常。 主要差异包括：

-   在 Linux 中不支持 Microsoft 分布式事务处理协调器 (DTC) [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果你的应用程序需要使用分布式事务，并且需要可用性组，部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Windows 上。
-   基于 Linux 的部署而不是 WSFC 使用 Pacemaker。
-   与大多数配置中为承载在 Windows 上个可用性组除外工作组群集方案，不同 Pacemaker 从不需要 Active Directory 域服务 (AD DS)。
-   如何失败从一个节点到另一个可用性组的不同 Linux 和 Windows 之间。
-   某些设置，例如`required_synchronized_secondaries_to_commit`而 WSFC 基于安装使用 TRANSACT-SQL 仅可以通过在 Linux 上，Pacemaker 更改。

## <a name="number-of-replicas-and-cluster-nodes"></a>副本和群集节点数

中的可用性组[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]可以具有两个总副本： 一个主数据库以及一个仅用于实现可用性目标的辅助数据库。 它不能进行任何其它，如可读查询操作。 中的可用性组[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]可以具有最多 9 个总副本： 一个主要和最多八个辅助数据库，其中最多三 （包括主） 可以是同步的。 如果使用一个基础群集，可以有最多 16 节点总涉及 Corosync 时。 可用性组可以跨最多九个 16 个节点与[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]，另外两个[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。

需要自动故障转移到另一个副本的能力的两个副本配置需要仅配置副本，请使用中所述[仅配置副本和仲裁](#configuration-only-replica-and-quorum)。 中引入了仅配置副本[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]累积更新 1 (CU1)，因此，应该部署此配置的最小版本。

如果使用 Pacemaker 时，它必须正确配置使它保持启动并正在运行。 这意味着，仲裁和 STONITH 必须实现正确从 Pacemaker 的角度看，除了任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]要求，如仅配置副本。

可读辅助副本仅支持与[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。

## <a name="cluster-type-and-failover-mode"></a>群集类型和故障转移模式

新手[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是承载个可用性组的群集类型的简介。 对于 Linux，有两个有效的值： 外部和 None。 一种群集类型的外部意味着，将会 Pacemaker 使用可用性组的下方。 对于群集类型要求的故障转移模式以及设置到外部使用外部 (中还新增[!INCLUDE[sssql17-md](../includes/sssql17-md.md)])。 支持自动故障转移，但与 WSFC 故障转移模式设置为外部，不自动使用 Pacemaker 时。 与 WSFC 不同后配置可用性组创建可用性组的 Pacemaker 部分。

群集类型为无意味着，不需要也将可用性组使用，Pacemaker。 即使在配置了Pacemaker的服务器上，如果AG配置的群集类型为None，Pacemaker将不会看到或管理该AG。 为无群集类型仅支持从主以手动方式故障转移到辅助副本。 为读取-横向扩展方案，以及升级主要面向任何创建可用性组。 尽管它可以运行在灾难恢复或没有自动故障转移是必需的本地可用性等的情况下，不建议。 侦听器情景还有更复杂而无需 Pacemaker。

群集类型存储在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]动态管理视图 (DMV) `sys.availability_groups`，列中`cluster_type`和`cluster_type_desc`。

## <a name="requiredsynchronizedsecondariestocommit"></a>required\_synchronized\_secondaries\_to\_commit

新手[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是设置，可供承载个可用性组调用`required_synchronized_secondaries_to_commit`。 这将告知可用性组必须与主保持同步的辅助副本的数目。 这使等自动故障转移 （仅在与群集类型为外部 Pacemaker 集成），并控制等的主可用性的行为，如果适当数量的辅助副本是联机还是脱机。 若要了解有关此工作原理的详细信息，请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 `required_synchronized_secondaries_to_commit`值是默认设置和维护由 Pacemaker /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 你可以手动重写此值。

组合`required_synchronized_secondaries_to_commit`和新的序列号 (存储在`sys.availability_groups`) 通知 Pacemaker 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，例如，可能发生自动故障转移。 在这种情况下，辅助副本将具有相同序列号的主数据库，这意味着它最新的最新的所有配置信息。

有三个可以为设置的值`required_synchronized_secondaries_to_commit`: 0、 1 或 2。 它们控制的副本变得不可用，会发生什么情况的行为。 数字对应于必须与主同步的辅助副本的数目。 行为，如下所示是在 Linux 下：

-   0 – 无自动故障转移功能为可能，因为没有辅助副本需要同步。 任何时候，主数据库都可用。
-   1 – 一个辅助副本必须位于与主; 的同步状态自动故障转移的情况。 可用辅助同步副本之前，主数据库不可用。
-   2-三个或多个节点可用性组配置中的两个辅助副本必须与主; 同步自动故障转移的情况。

`required_synchronized_secondaries_to_commit`控制不仅的同步副本，但数据丢失的故障转移行为。 值为 1 或 2，辅助副本时始终需要同步，因此始终将数据冗余。 这意味着不会丢失数据。

若要更改的值`required_synchronized_secondaries_to_commit`，使用以下语法。

>[!NOTE]
>更改值会导致资源来重新启动，这意味着短暂的停机。 若要避免这种情况的唯一方法是设置不受群集暂时的资源。

**Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

```bash
sudo pcs resource update <AGResourceName>-master required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

其中*AGResourceName*是针对可用性组中，配置的资源的名称和*值*是 0、 1 或 2。 若要将其设置回 Pacemaker 管理参数的默认值，请执行带有任何值的相同语句。

满足以下条件时，可能会自动故障转移的可用性组：

-   主和辅助副本设置为同步的数据移动。
-   辅助数据库已同步 （不同步），这意味着两个位于相同的数据点的状态。
-   群集类型设置为外部。 自动故障转移不能与群集类型为无。
-   `sequence_number`将成为辅助副本的主具有最高的序列号-换而言之，辅助副本的`sequence_number`匹配从原始主副本。

如果满足这些条件，承载主副本的服务器失败，则可用性组将将所有权更改为同步的副本。 同步副本的行为 (的其中可以有三个总： 一个主节点和两个辅助副本) 进一步可通过控制`required_synchronized_secondaries_to_commit`。 这在 Windows 和 Linux 上配合承载个可用性组，但配置完全不同。 在 Linux 上，通过该可用性组资源本身上的群集自动配置的值。

## <a name="configuration-only-replica-and-quorum"></a>仅配置副本和仲裁

中还新增[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]截至 CU1 是仅配置副本。 因为 Pacemaker 不同于 WSFC，尤其是当涉及到仲裁和需要 STONITH，只需两个节点配置将无法工作时涉及到可用性组。 Fci，提供 Pacemaker 的仲裁机制可以是不错，因为所有 FCI 故障转移仲裁都发生在群集层。 对于可用性组，在 Linux 下的仲裁都会在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、 所有元数据的存储位置。 这是仅配置副本就会起作用。

如果没有任何其他内容，第三个节点和至少一个同步的副本将是所需。 这不适用于[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]，因为它可以仅有两个参与可用性组的副本。 仅配置副本存储在 master 数据库中，相同的可用性组配置中的其他副本 AG 配置。 仅配置副本没有参与可用性组的用户数据库。 从主来同步发送配置数据。 无论它们是自动还是手动的故障转移期间，然后使用此配置数据。

为保持仲裁并启用群集类型为外部的自动故障转移可用性组，它是数据库必须：

-   有三个同步副本 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]仅); 或
-   有两个副本 （主要和次要），以及配置的唯一副本。

手动故障转移可能会发生情况是否使用外部或无群集的可用性组配置的类型。 虽然可以使用具有群集类型为无可用性组配置仅配置副本，它不建议，因为它使部署变得复杂。 对于这些配置，手动修改`required_synchronized_secondaries_to_commit`具有至少为 1，一个值，以便有至少一个同步的副本。

仅配置副本可以承载在任何版本的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，包括[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。 这将授权成本降到最低，并确保它与承载个可用性组中结合使用[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。 这意味着第三个所需服务器只需要满足的最小规范[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，因为它不接收针对可用性组的用户事务流量。

当使用仅配置副本时，它具有以下行为：

-   默认情况下，`required_synchronized_secondaries_to_commit`设置为 0。 这可以手动修改为 1 必要。
-   如果主站点故障和`required_synchronized_secondaries_to_commit`为 0，辅助副本将变为新的主并可供读取和写入。 如果值为 1，自动故障转移将会发生，但将不接受新事务，直到另一个副本处于联机状态。
-   如果辅助副本失败和`required_synchronized_secondaries_to_commit`为 0，主副本仍接受的事务，但如果主站点在此时故障，将以数据也不是故障转移可能没有保护 （手动或自动），因为辅助副本不可用。
-   如果仅配置副本失败，可用性组将正常工作，但是可能不会自动故障转移。
-   如果同步的辅助副本和仅配置副本出现故障，主无法接受的事务，并且没有地方的故障到主站点。

CU1 中是一个已知的 bug，通过生成 corosync.log 文件中记录`mssql-server-ha`。 如果不能成为可用的所需副本数目由于主辅助副本，则当前消息将显示为"在应当收到 1 的序列号，但仅接收 2。 没有足够的副本处于联机状态以安全地提升的本地副本。" 应逆转数字，并且它应该显示为"在应当收到 2 序列号，但仅接收 1。 没有足够的副本处于联机状态以安全地提升的本地副本。" 

## <a name="multiple-availability-groups"></a>多个可用性组 

每个 Pacemaker 群集或一组服务器，可以创建多个可用性组。 唯一的限制是系统资源。 可用性组所有权显示为 master。 不同承载个可用性组可以拥有的不同节点;并非所有需要的同一节点上运行它们。

## <a name="drive-and-folder-location-for-databases"></a>数据库的驱动器和文件夹位置

在基于 Windows 的承载个可用性组，如参与可用性组的用户数据库的驱动器和文件夹结构应相同。 例如，如果用户数据库位于`/var/opt/mssql/userdata`服务器 A 上，在该相同的文件夹应位于服务器 b。唯一的例外节中所述[与基于 Windows 的可用性组和副本互操作性](#interoperability-with-windows-based-availability-groups-and-replicas)。

## <a name="the-listener-under-linux"></a>在 Linux 下侦听器

侦听器是可用性组的可选功能。 它对所有连接 （读/写到的主副本和/或只读的辅助副本） 上提供单一入口点，以便应用程序和最终用户不需要知道哪个服务器承载数据。 在 WSFC 中，这是网络名称资源和 IP 资源，然后在 AD DS （如果需要） 中注册的组合以及 DNS。 在与可用性组资源本身组合使用，它提供该抽象。 有关侦听器的详细信息，请参阅[侦听器、 客户端连接和应用程序故障转移](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)。

在 Linux 下的侦听器配置不同，但其功能是相同的。 没有 Pacemaker 中的网络名称资源的概念也不在 AD DS; 创建为一个对象没有只需在可以在任何节点运行的 Pacemaker 中创建一个 IP 地址资源。 与 IP 资源的 DNS 中具有"友好名称"的侦听器关联的条目将需要创建。 侦听器的 IP 资源将只能承载该可用性组的主副本的服务器上处于活动状态。

如果使用 Pacemaker 和 IP 地址资源创建与侦听器相关联，将有短暂的停机的 IP 地址会在一台服务器上停止和启动另一方面，无论它是自动还是手动故障转移。 尽管这提供了通过单个名称和 IP 地址的组合的抽象，它不会屏蔽中断。 应用程序必须能够处理具有某种形式的功能，可检测到这种并重新连接的断开连接。

但是，组合的 DNS 名称和 IP 地址是仍不足以提供所有的侦听器在 WSFC 上提供，如辅助副本只读路由的功能。 在配置可用性组时，"侦听器"仍然需要在中配置[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 这可以在向导和 TRANSACT-SQL 语法中看到。 有两种方法，这可以将配置为在功能上相同 Windows 上：

-   群集类型为外部 ag，与"侦听器"中创建关联的 IP 地址[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应在 Pacemaker 中创建的资源的 IP 地址。
-   对于群集类型为无创建可用性组，使用与主副本关联的 IP 地址。

然后与提供的 IP 地址关联的实例将成为只读路由请求，从应用程序之类的内容的协调器。

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>与基于 Windows 的可用性组和副本互操作性 

具有外部或其中一个是 WSFC 群集类型可用性组不能具有跨平台及其副本。 这是 true 可用性组是否[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]或[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。 在传统的可用性组配置中使用一个基础群集这意味着，一个副本不能为 WSFC 和 Pacemaker 使用 Linux 上其他。

群集类型为一个可用性组可以让其跨 OS 边界，因此同一可用性组中可能有两个基于 Linux 和 Windows 的副本的副本。 其中的主副本是基于 Windows 的辅助数据库上的 Linux 分发之一时，一个示例所示。

![混合无](./media/sql-server-linux-availability-group-overview/image1.png)

分布式可用性组还可以跨 OS 边界。 有关如何配置情况，如外部为配置了一个基础承载个可用性组绑定的规则仅 Linux，但无法使用 WSFC 配置联接到可用性组。 以下是一个示例。

![混合 Dist 可用性组](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>后续步骤
[在 Linux 上的 SQL Server 配置可用性组](sql-server-linux-availability-group-configure-ha.md)

[在 Linux 上的 SQL Server 配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)

[添加可用性组群集资源在 RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[添加可用性组群集资源在 SLES](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上添加可用性组群集资源](sql-server-linux-availability-group-cluster-ubuntu.md)

[配置跨平台可用性组](sql-server-linux-availability-group-cross-platform.md)

