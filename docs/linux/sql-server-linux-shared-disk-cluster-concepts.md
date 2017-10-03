---
title: "故障转移群集实例-在 Linux 上的 SQL Server |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 229c6a989a4707921eae3046e3c9707b05bb0306
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---

# <a name="failover-cluster-instances---sql-server-on-linux"></a>故障转移群集实例-在 Linux 上的 SQL Server

此文章介绍了在 Linux 上的 SQL Server 故障转移群集实例 (FCI) 与相关的概念。 

若要在 Linux 上创建 SQL Server FCI，请参阅[在 Linux 上配置 SQL Server 的 FCI](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>聚类分析层

* RHEL，聚类分析层基于 Red Hat Enterprise Linux (RHEL) 上[HA 外接程序](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)。 

    > [!NOTE] 
    > Red Hat HA 外接程序和文档的访问要求一个订阅。 

* 在 SLES，聚类分析层基于 SUSE Linux Enterprise[高可用性扩展 (HAE)](https://www.suse.com/products/highavailability)。

    群集配置、 资源代理选项、 管理、 最佳实践，和建议的详细信息，请参阅[SUSE Linux Enterprise 高可用性扩展 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

RHEL HA 外接程序和 SUSE HAE 基于[Pacemaker](http://clusterlabs.org/)。

如下图所示，存储将呈现给两个服务器。 群集组件 - Corosync 和 Pacemaker - 协调通信和资源管理。 一台服务器具有到存储资源和 SQL Server 的活动连接。 当 Pacemaker 检测到故障时，群集组件负责管理将资源移到另一个节点。  

![Red Hat Enterprise Linux 7 共享磁盘 SQL 群集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 此时，在 Linux 上 SQL Server 与 Pacemaker 的集成不及与在 Windows 上与 WSFC 集成的耦合性高。 在 SQL 内部，无法了解到群集是否存在，所有业务流程都是由外至内，并且 Pacemaker.将该服务作为一个独立实例控制。 此外，虚拟网络名称特定于 WSFC，Pacemaker 中无相同的等效项。 它预期的 @@servername和 sys.servers 以返回节点名称，而群集 dmv sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 不将任何记录。 为了使用指向字符串服务器名称的连接字符串，且不使用 IP，它们需要在其 DNS 服务器中注册用于创建使用选定服务器名称的虚拟 IP 资源的 IP（如下文所述）。

## <a name="number-of-instances-and-nodes"></a>实例数和节点

在 Linux 上的 SQL Server 的一个主要区别是，只能有一个 SQL Server 的每个 Linux 服务器的安装。 该安装，称为实例。 这意味着，Windows Server 支持的每个 Windows Server 故障转移群集 (WSFC) 的最多 25 个 Fci，与基于 Linux 的 FCI 将仅具有单个实例。 此一个实例也是默认实例;没有在 Linux 上的命名实例的概念。 

Pacemaker 群集只能有最多 16 节点当 Corosync 涉及到，因此单个 FCI 可以跨达 16 台服务器。 使用 SQL Server 标准版实现 FCI 支持最多两个节点群集的即使 Pacemaker 群集具有最大 16 个节点。

在 SQL Server FCI，SQL Server 实例是上一个节点或其他处于活动状态。

## <a name="ip-address-and-name"></a>IP 地址和名称
在 Linux Pacemaker 群集上，每个 SQL Server FCI 将需要其自己的唯一的 IP 地址和名称。 如果 FCI 配置跨多个子网，一个 IP 地址都会要求提供每个子网。 唯一的名称和 IP 地址用于访问 FCI，以便应用程序和最终用户不需要知道哪些基础 Pacemaker 群集的服务器。

在 DNS 中在 FCI 的名称应为获取 Pacemaker 群集中创建的 FCI 资源的名称相同。
必须在 DNS 中注册的名称和 IP 地址。

## <a name="shared-storage"></a>共享存储
所有 Fci，无论它们是在 Linux 或 Windows Server 上都需要某种形式的共享存储。 向可能可以承载 FCI 中，所有服务器都提供此存储，但只有一台服务器可以为使用存储 FCI 在任何给定时间。 可用于在 Linux 下的共享存储的选项是：

- iSCSI
- 网络文件系统 (NFS)
- 服务器消息块 (SMB) 在 Windows Server，有略有不同的选项。 当前不支持基于 Linux 的 Fci 的一个选项是使用 TempDB，这是 SQL Server 的临时工作区中的节点的本地磁盘的能力。

在配置中跨多个位置，在一个数据中心存储的内容必须同步包含其他。 发生故障转移时，FCI 将能够进入联机状态，因此存储很相同。 实现此目的将需要一些外部方法的存储复制，不管是通过基础存储硬件或某些基于软件的实用工具。 

>[!NOTE]
>有关 SQL Server 自 2017 年，必须使用 XFS 或 EXT4 格式化基于 Linux 的部署使用直接向此类的服务器显示的磁盘。 当前不支持其他文件系统。 此处将会反映任何更改。

提供共享的存储的过程是相同的受支持的不同方法：

- 配置共享的存储
- 作为向将充当 FCI Pacemaker 群集的节点的服务器文件夹中装入存储
- 如果需要，将 SQL Server 系统数据库移到共享存储
- SQL Server 的工作方式从每个服务器的测试已连接到共享存储

与在 Linux 上的 SQL Server 的一个主要区别是，虽然您可以配置默认用户数据和日志文件位置，系统数据库必须始终存在在`/var/opt/mssql/data`。 Windows Server 上没有能够移动包括 TempDB 系统数据库。 为 FCI 配置如何共享存储到的播放这一事实。

可以使用更改的默认路径为非系统数据库`mssql-conf`实用程序。 有关如何更改默认设置，[默认数据或日志目录位置更改](sql-server-linux-configure-mssql-conf.md#datadir)。 您还可以存储 SQL Server 数据和事务在其他位置，只要它们具有适当的安全性，即使它不是默认位置;位置将需要为所述。

以下主题说明如何为基于 Linux 的 SQL Server FCI 配置支持的存储类型：

- [配置故障转移群集实例-iSCSI-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [配置 NFS-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [配置 SMB-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-smb.md)

