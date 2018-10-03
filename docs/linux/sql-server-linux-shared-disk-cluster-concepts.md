---
title: 故障转移群集实例-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 14d54a9e004364db783a4462d9e941f0e513a292
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659805"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>故障转移群集实例-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍 Linux 上的 SQL Server 故障转移群集实例 (FCI) 的概念。 

若要在 Linux 上创建 SQL Server FCI，请参阅[Linux 上配置 SQL Server FCI](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>群集层

* 在 RHEL、 群集层基于 Red Hat Enterprise Linux (RHEL) 上[HA 加载项](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)。 

    > [!NOTE] 
    > 对 Red Hat HA 加载项和文档的访问需要一个订阅。 

* 在 SLES，群集层基于 SUSE Linux Enterprise[高可用性扩展 (HAE)](https://www.suse.com/products/highavailability)。

    有关群集配置、 资源代理选项、 管理、 最佳实践和建议的详细信息，请参阅[SUSE Linux Enterprise 高 Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

基于 RHEL HA 加载项和 SUSE HAE [Pacemaker](http://clusterlabs.org/)。

如以下关系图所示，存储将呈现给两个服务器。 群集组件 - Corosync 和 Pacemaker - 协调通信和资源管理。 一台服务器具有到存储资源和 SQL Server 的活动连接。 当 Pacemaker 检测到故障时，群集组件负责管理将资源移到另一个节点。  

![Red Hat Enterprise Linux 7 共享磁盘的 SQL 群集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 此时，在 Linux 上 SQL Server 与 Pacemaker 的集成不及与在 Windows 上与 WSFC 集成的耦合性高。 在 SQL 内部，无法了解到群集是否存在，所有业务流程都是由外至内，并且 Pacemaker.将该服务作为一个独立实例控制。 此外，虚拟网络名称特定于 WSFC，Pacemaker 中无相同的等效项。 它预期的 @@servername和 sys.servers 将返回的节点名称，而群集 dmv sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 将无任何记录。 若要使用指向字符串服务器名称的连接字符串而不使用 IP，他们将需要注册其 DNS 服务器中创建虚拟 IP 资源 （如以下各节中所述） 所使用的 IP 与所选的服务器名称。

## <a name="number-of-instances-and-nodes"></a>实例数和节点

Linux 上的 SQL Server 的一个主要区别是，只能有一个安装 SQL Server 的每台 Linux 服务器。 该安装称为实例。 这意味着，与 Windows Server 支持每个 Windows Server 故障转移群集 (WSFC) 最多 25 个 Fci，不同的是基于 Linux 的 FCI 将仅具有单个实例。 此实例也是默认实例;没有在 Linux 上的命名实例的概念。 

Pacemaker 群集只能有最多 16 个节点时涉及到 Corosync，因此单个 FCI 可以跨最多 16 个服务器。 FCI 实现与 Standard Edition SQL Server 支持最多两个节点的群集，即使 Pacemaker 群集有最大 16 个节点。

在 SQL Server FCI，SQL Server 实例是上一个节点或其他活动。

## <a name="ip-address-and-name"></a>IP 地址和名称
在 Linux Pacemaker 群集上，每个 SQL Server FCI 需要其自己唯一的 IP 地址和名称。 如果 FCI 配置跨多个子网，将根据子网，必须提供一个 IP 地址。 唯一的名称和 IP 地址用于访问 FCI，以便应用程序和最终用户不需要知道 Pacemaker 群集的基础服务器。

在 FCI 在 DNS 中的名称应为 Pacemaker 群集中创建的 FCI 资源名称相同。
必须在 DNS 中注册的名称和 IP 地址。

## <a name="shared-storage"></a>共享存储
所有 Fci，不管它们是在 Linux 或 Windows Server 都要求某种形式的共享存储。 此存储将呈现给可能可以承载 FCI 的所有服务器，但只有一台服务器可以存储使用 fci，在任何给定时间。 适用于 Linux 下的共享存储选项包括：

- iSCSI
- 网络文件系统 (NFS)
- 服务器消息块 (SMB) 在 Windows Server，有略有不同的选项。 目前不支持为基于 Linux 的 Fci 的一个选项是使用 tempdb，这是 SQL Server 的临时工作区节点本地磁盘的能力。

在配置中跨多个位置，在一个数据中心存储的内容必须与同步其他。 发生故障转移时，FCI 将能够进入联机状态并存储看到的相同。 实现此目的需要一些外部方法存储复制是否完成通过基础的存储硬件或某些基于软件的实用程序。 

>[!NOTE]
>对于 SQL Server，必须使用 XFS 或 EXT4 格式化使用磁盘直接向此类的服务器提供的基于 Linux 的部署。 目前不支持其他文件系统。 此处将会反映任何更改。

提供共享的存储的过程是相同的受支持的不同方法：

- 配置共享的存储
- 将存储装载为向将作为 FCI 的 Pacemaker 群集节点的服务器文件夹
- 如有必要，将 SQL Server 系统数据库移到共享存储
- 测试 SQL Server 中的每个服务器起已连接到共享存储

与 Linux 上的 SQL Server 的一个主要区别是，虽然可以配置默认的用户数据和日志文件位置，系统数据库必须始终存在在`/var/opt/mssql/data`。 在 Windows Server 上没有移动包括 TempDB 系统数据库的功能。 为 FCI 配置到如何共享存储中起着这一事实。

可以使用更改为非系统数据库的默认路径`mssql-conf`实用程序。 有关如何更改默认值，信息[更改默认数据或日志目录位置](sql-server-linux-configure-mssql-conf.md#datadir)。 您还可以将存储 SQL Server 数据和事务的其他位置，只要它们具有适当的安全性，即使它不是默认位置;位置将需要为所述。

以下主题说明如何为基于 Linux 的 SQL Server FCI 配置支持的存储类型：

- [配置故障转移群集实例-iSCSI-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [配置 NFS-Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [配置 SMB-Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-smb.md)
