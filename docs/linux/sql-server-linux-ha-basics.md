---
title: 对于 Linux 部署 SQL Server 可用性基础知识 |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: b33acbcf74857cd6a2def74f3596e3dda2a034a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720865"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>对于 Linux 部署 SQL Server 可用性基础知识

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

从开始[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]， [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 和 Windows 上受支持。 像基于 Windows 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]数据库和实例需要具有高可用性 Linux 下。 本文介绍如何规划和部署高度可用的技术方面基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]数据库和实例，以及一些与基于 Windows 的安装的差异。 因为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 专业人员和 Linux 可能是新的可能是刚开始[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]专业人员，文章有时介绍了可能不熟悉一些和向其他人不熟悉的概念。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 部署的可用性选项
除了备份和还原，相同的三个可用性功能是可在 Linux 上与基于 Windows 的部署：
-   Always On 可用性组 (Ag)
-   Alwayson 故障转移群集实例 (Fci)
-   [日志传送](sql-server-linux-use-log-shipping.md)

在 Windows，Fci 始终要求基础 Windows Server 故障转移群集 (WSFC)。 具体取决于部署方案中，AG 通常需要基础 WSFC，例外是新变体中无[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 WSFC 在 Linux 中不存在。 聚类分析在 Linux 中的实现部分中讨论[Pacemaker Always On 可用性组和故障转移群集实例在 Linux 上](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)。

## <a name="a-quick-linux-primer"></a>快速的 Linux 入门
在某些 Linux 安装可能安装了使用接口中，大多数都是不是，这意味着，在操作系统层几乎所有内容都已通过命令行。 在 Linux 领域中该命令行使用的常用术语是*bash shell*。

在 Linux 中，很多命令需要执行使用提升的权限，就像许多事情需要以管理员身份的 Windows Server 中执行。 有两种主要方法使用提升的特权来执行：
1. 在适当的用户的上下文中运行。 若要将更改为其他用户，使用命令`su`。 如果`su`执行其自身上没有用户名，只要知道密码，您现在将在外壳程序中作为*根*。
   
2. 更常用和安全意识的方式运行操作是使用`sudo`之前执行任何操作。 在此示例的许多文章使用`sudo`。

一些常用命令，其中每个都有各种开关和可以在线研究的选项：
-   `cd` – 将目录更改
-   `chmod` – 更改文件或目录的权限
-   `chown` – 更改文件或目录的所有权
-   `ls` – 显示目录的内容
-   `mkdir` – 驱动器上创建文件夹 （目录）
-   `mv` -将文件从一个位置移动到另一个
-   `ps` – 显示所有工作进程
-   `rm` – 删除本地服务器上的文件
-   `rmdir` – 删除文件夹 （目录）
-   `systemctl` -启动、 停止或启用服务
-   文本编辑器命令。 在 Linux 上，有各种文本编辑器选项，如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>可用性配置的常见任务[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上
本部分介绍了任务所共有的基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

### <a name="ensure-that-files-can-be-copied"></a>确保可以复制文件
将文件从一台服务器复制到另一个是一项任务的任何人都使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上应该能够执行操作。 此任务是非常重要的可用性组配置。

Linux 上以及在基于 Windows 的安装上，可以存在权限问题等内容。 但是，熟悉如何在 Windows 上，将复制从服务器到服务器可能不熟悉如何在 Linux 上执行。 一种常用方法是使用命令行实用工具`scp`，这代表安全的复制。 在后台，`scp`使用 OpenSSH。 SSH 代表安全外壳。 根据 Linux 分发版，OpenSSH 本身可能未安装。 如果不是这样，OpenSSH 需要先安装。 有关配置 OpenSSH 的详细信息，请参阅以下链接，了解每个分布区中的信息：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

当使用`scp`，如果不是源或目标，必须提供服务器的凭据。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

将文件 MyAGCert.cer 复制到另一台服务器上指定的文件夹。 请注意，您必须有权限 – 和可能是复制该密钥，因此该文件的所有权-`chown`可能还需要复制之前采用。 同样，在接收端适当的用户需要访问和操作该文件。 例如，若要还原该证书文件，`mssql`用户必须能够访问它。

Samba，这是服务器消息块 (SMB) 的 Linux 变体，也可用于创建共享访问的 UNC 路径如`\\SERVERNAME\SHARE`。 有关配置 Samba 的详细信息，请参阅以下链接，了解每个分布区中的信息：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

此外可以使用基于 Windows 的 SMB 共享;SMB 共享不需要是基于 Linux 的只要承载的 Linux 服务器上正确配置 Samba 的客户端部分[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]并且共享包含正确的访问权限。 对于那些在混合环境中，这将是一种方法来利用现有基础结构基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

非常重要的一点是 Samba 部署的版本应为 SMB 3.0 兼容。 在添加对 SMB 的支持时[!INCLUDE[sssql11-md](../includes/sssql11-md.md)]，它需要支持 SMB 3.0 的所有共享。 如果使用 Samba 共享并不是 Windows Server，Samba 4.0 或更高版本，并在理想情况下 4.3 或更高版本，支持 SMB 3.1.1 应当使用基于 Samba 共享。 是很好的 SMB 和 Linux 上的信息来源[Samba 中的 SMB3](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)。

最后，使用网络文件系统 (NFS) 共享是一个选项。 使用 NFS 不上的基于 Windows 的部署选项[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，并且仅用于基于 Linux 的部署。

### <a name="configure-the-firewall"></a>配置防火墙
类似于 Windows，Linux 发行版具有内置防火墙。 如果你的公司使用的服务器的外部防火墙，禁用在 Linux 防火墙可能是可接受。 但是，无论其中启用了防火墙，端口需要打开。 下表介绍常见的端口所需的高度可用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上的部署。

| 端口号 | 类型     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | （如果使用） 的 samba – 终结点映射程序                                                                                          |
| 137         | UDP      | Samba （如果使用） – NetBIOS 名称服务                                                                                      |
| 138         | UDP      | Samba （如果使用） – NetBIOS 数据报                                                                                          |
| 139         | TCP      | Samba （如果使用） – NetBIOS 会话                                                                                           |
| 445         | TCP      | （如果使用） 的 samba – SMB 通过 TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – 默认端口;如果需要，可以更改与 `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP、UDP | NFS （如果使用）                                                                                                               |
| 2224        | TCP      | Pacemaker-通过使用 `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker-必需 Pacemaker 远程节点                                                                    |
| 3260        | TCP      | 可以在中更改 iSCSI 发起程序 （如果使用） – `/etc/iscsi/iscsid.config` (RHEL)，但应匹配的 iSCSI 目标端口 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的默认端口用于可用性组终结点;创建终结点时可以更改                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker-如果使用多播的 UDP 所需的 Corosync                                                                     |
| 5405        | UDP      | Pacemaker-所需的 Corosync                                                                                            |
| 21064       | TCP      | Pacemaker-所需的资源使用 DLM                                                                                 |
| 变量    | TCP      | 可用性组终结点端口;默认为 5022                                                                                           |
| 变量    | TCP      | NFS – 的端口`LOCKD_TCPPORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                              |
| 变量    | UDP      | NFS – 的端口`LOCKD_UDPPORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                              |
| 变量    | TCP/UDP  | NFS – 的端口`MOUNTD_PORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                                |
| 变量    | TCP/UDP  | NFS – 的端口`STATD_PORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                                 |

为 Samba 可能使用的其他端口，请参阅[Samba 端口用法](https://wiki.samba.org/index.php/Samba_Port_Usage)。

相反，在 Linux 下的服务的名称也都可以作为而不是端口，则为异常添加例如， `high-availability` Pacemaker 的。 如果这是你想要采用的方向，请参阅你的分发的名称。 例如，在 RHEL 上添加 Pacemaker 中的命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火墙文档：**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>安装[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]包可用性
在基于 Windows 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安装，而有些则不然甚至进行基本引擎安装时，安装某些组件。 在仅限 Linux[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]引擎作为安装过程的一部分安装。 其他所有内容是可选的。 为高度可用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 下的实例，应使用安装两个包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]:[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理 (*mssql server 代理*) 和高可用性 (HA) 包 (*mssql server-ha*)。 虽然[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理是可选的从技术上讲，它是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的作业的计划程序，并为所需的日志传送，因此建议安装。 在基于 Windows 的安装中，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理不可选。

>[!NOTE]
>对于那些新接触[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的内置作业计划程序。 它是可使用计划备份和其他类似的常用方法[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]维护。 与基于 Windows 的安装不同[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]其中[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理是一种完全不同的服务，在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理在上下文中运行[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]本身。

当 Ag 或 Fci 上基于 Windows 的配置中配置时，它们是能够识别群集。 群集感知意味着[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]具有特定资源 WSFC 知道 （sqagtres.dll 和 Fci 的 Ag hadrres.dll 的 sqsrvres.dll） 的 Dll 和 WSFC 用于确保[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]群集的功能已启用、 运行，并正常运行。 因为聚类分析外部不是仅为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]但 Linux 本身，Microsoft 不得不代码等效于基于 Linux 的可用性组和 FCI 部署的资源 DLL。 这是*mssql server-ha*包，也称为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的 Pacemaker 资源代理。 若要安装*mssql server-ha*包，请参阅[安装高可用性和 SQL Server 代理包](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)。

有关其他可选包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文搜索 (*mssql server fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql server 是*)，不是所需的高可用性，为 FCI 或可用性组。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Always On 可用性组和 Linux 上的故障转移群集实例的 pacemaker
与先前所述，当前支持由 Microsoft 承载和 Fci 的唯一聚类分析机制是使用 Corosync Pacemaker。 本部分介绍的基本信息来了解该解决方案，以及如何规划和部署它的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]配置。

### <a name="ha-add-onextension-basics"></a>高可用性在加载/扩展基本知识
所有当前受支持分发版提供高可用性加载-在/扩展，它基于聚类分析堆栈 Pacemaker。 此堆栈包含两个关键组件： Pacemaker 和 Corosync。 堆栈的所有组件都包括：
-   Pacemaker-聚类分析组件，在群集的计算机之间执行诸如坐标的核心。
-   Corosync – 一个框架和一组 api，提供了诸如仲裁、 重新启动失败进程等的能力。
-   libQB – 等日志记录提供内容。
-   资源代理 – 提供，以便可以将应用程序与 Pacemaker 的集成的特定功能。
-   围墙代理 – 脚本/功能帮助隔离节点，如果它们时遇到问题处理它们。
    
> [!NOTE]
> 群集堆栈通常称为 Linux 世界上的 Pacemaker。

此解决方案是在某些方面类似于，但在很多方面不同于部署使用 Windows 的群集的配置。 在 Windows，操作系统和功能，可以创建 WSFC 故障转移群集，默认情况下禁用内置的聚类分析，名为 Windows Server 故障转移群集 (WSFC) 可用性形式。 在 Windows 中，Ag 和 Fci 都基于 WSFC 和由于特定的资源 DLL 提供的共享的紧密集成[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 此紧密耦合的解决方案是可能的因为它是一家供应商所有。

![](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上，而每个受支持的分发版具有 Pacemaker 可用，可以自定义每个分布区和略有不同的实现和版本。 一些差异将反映在本文中的说明进行操作。 聚类分析层是开放源代码，因此，即使它附带了分布区，它不紧密集成以相同方式 WSFC 都是在 Windows 下。 这就是 Microsoft 提供了原因*mssql server-ha*，以便[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和 Pacemaker 堆栈可提供接近，但不完全相同，体验 Ag 和 Fci Windows 下。

Pacemaker 的完整文档，其中包括的所有内容的完整参考信息，对于 RHEL 和 SLES 是更深入的说明：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 没有可用性的指南。

有关整个堆栈的详细信息，另请参阅官方[Pacemaker 文档页](http://clusterlabs.org/doc/)Clusterlabs 站点上。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念和术语
本部分介绍常见的概念和术语的 Pacemaker 实现。

#### <a name="node"></a>节点
节点是参与群集的服务器。 Pacemaker 群集以本机方式支持最多 16 个节点。 如果未在其他节点上运行 Corosync 但 Corosync 是所必需的可能会超过此数字[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 因此，最大节点数的群集可以具有任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-基于的配置为 16; 这是 Pacemaker 限制，并且没有任何与 Ag 或 Fci 所规定的最大限制[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 

#### <a name="resource"></a>资源
WSFC 和 Pacemaker 群集具有资源的概念。 资源是在群集中，如磁盘或 IP 地址的上下文中运行的特定功能。 例如，在 Pacemaker 下 FCI 和可用性组资源可以获取创建。 这不是有别于什么是在 WSFC 中，将出现[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]FCI 的资源或配置可用性组时的可用性组资源但是不完全相同的方式根本不同之处由于[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]与 Pacemaker 集成。

Pacemaker 具有标准版和克隆的资源。 克隆资源是一种是在所有节点上同时运行。 示例是为实现负载均衡的多个节点运行的 IP 地址。 获取为 Fci 创建的任何资源使用标准资源，因为在任何给定时间，只有一个节点可以承载 FCI。

创建 AG 时，它需要名为多状态的资源的克隆资源的一种专用的形式。 虽然 AG 只能有一个主副本，可用性组本身正在运行，在所有节点，它已配置为在，并就有可能使等只读访问权限。 这是节点的"实时"使用，因为资源都具有两个状态的概念： 主 / 从。 有关详细信息，请参阅[多状态的资源： 具有多个模式的资源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>资源组/设置
类似于 WSFC 中的角色，Pacemaker 群集具有资源组的概念。 资源组 （在 SLES 中称为一） 是一系列资源，它们共同发挥作用，并可以故障转移从一个节点到另一个作为单个单元。 资源组不能包含配置为 master/slave; 的资源因此，它们不能用于 Ag。 尽管可以为 Fci 使用的资源组，但它不是通常推荐的配置。

#### <a name="constraints"></a>约束
Wsfc 具有多个参数的资源，以及诸如告诉 WSFC 的两个不同的资源之间的父/子关系的依赖项。 依赖项是只需告诉 WSFC 哪些资源必须处于联机状态的第一次的规则。

Pacemaker 群集不具有依赖关系的概念，但存在限制。 有三种类型的约束： 主机托管、 位置和排序。
-   主机托管约束强制执行应在同一节点上运行两个资源。
-   位置约束告知 Pacemaker 群集资源可以 （或无法） 运行的位置。
-   排序约束告知 Pacemaker 群集资源应在其中启动的顺序。

> [!NOTE]
> 由于所有这些都被视为单个单元，则不需要的资源在资源组中，主机托管约束。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁、 隔离代理和 STONITH
下 Pacemaker 仲裁是某种程度上类似于在概念上的 WSFC。 群集的仲裁机制的主要目的是确保群集保持启动并运行。 WSFC 和的 Linux 分发版的 HA 加载项都具有这一概念的投票，其中每个节点都将计入仲裁。 您要将大部分投票，否则，在最坏的情况下，群集将关闭。

与不同的 WSFC，没有见证服务器资源才能使用仲裁。 如 WSFC，目标是要保留的投票者奇数数目。 仲裁配置具有不同于 Fci 的 Ag 的注意事项。

Wsfc 监视参与节点的状态，并出现问题时处理它们。 Wsfc 的更高版本提供此类功能作为隔离表现不正常或不可用的节点 （节点不在、 网络通信已关闭，等等）。 在 Linux 方面，这种功能提供的隔离代理。 有时，这一概念称为隔离。 但是，这些隔离代理通常特定于部署，并且通常由硬件供应商和等的用户提供虚拟机监控程序一些软件供应商提供。 例如，VMware 提供了可用于 Linux Vm 使用 vSphere 虚拟化隔离代理。

仲裁和到另一个概念隔离等同值称为 STONITH，或对标头中的其他节点。 STONITH 需要具有在所有 Linux 分发版支持的 Pacemaker 群集。 有关详细信息，请参阅[Red Hat 高可用性群集中隔离](https://access.redhat.com/solutions/15575)(RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf`文件包含在群集的配置。 该文件位于`/etc/corosync`。 在正常日常操作过程中此文件应永远不需要进行编辑，如果群集已正确设置。

#### <a name="cluster-log-location"></a>群集日志位置
Pacemaker 群集的日志位置因分发而异。
-   RHEL 和 SLES- `/var/log/cluster/corosync.log`
-   Ubuntu – `/var/log/corosync/corosync.log`

若要更改默认日志记录位置，请修改`corosync.conf`。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>计划 Pacemaker 的群集 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
本部分讨论 Pacemaker 群集的重要规划点。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>为虚拟化的基于 Linux 的 Pacemaker 群集 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
使用虚拟机部署基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Ag 和 Fci 的部署涵盖与基于 Windows 的对应的相同规则。 还有一组基本的可支持性的规则的虚拟化[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署中 Microsoft 提供的[Microsoft 支持知识库 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)。 如 Microsoft 的 HYPER-V 和 VMware 的 ESXi 虚拟机监控程序可能具有不同的方差最重要的是，由于平台本身之间的差异。

谈到 Ag 和 Fci 下虚拟化，请确保给定的 Pacemaker 群集的节点设置反相关性。 配置以实现高可用性在 AG 或 FCI 配置中，托管的 Vm 时[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应永远不会在同一个虚拟机监控程序主机上运行。 例如，如果部署两个节点 FCI，则需要*至少*三个虚拟机监控程序主机，非常有某处个托管节点的 Vm 继续出现主机故障时，尤其是如果使用的功能如 Live迁移或 vMotion。

有关更多详细信息，请参阅：
-   Hyper V 文档 –[使用来宾群集实现高可用性](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   白皮书 （编写为基于 Windows 的部署，但大部分概念仍适用） –[规划高度可用的任务关键型 SQL Server 部署使用 VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>HYPER-V 尚不支持使用 STONITH RHEL 与 Pacemaker 群集。 支持之前，有关详细信息和更新，请查阅[RHEL 高可用性群集的支持策略](https://access.redhat.com/articles/29440#3physical_host_mixing)。

### <a name="networking"></a>网络
与不同的 WSFC，Pacemaker 不需要专用的名称或至少一个专用的 IP 地址为 Pacemaker 群集本身。 Ag 和 Fci 将需要 IP 地址 （请参阅有关详细信息的每个文档），但不是包括名称，因为没有任何网络名称资源。 SLES 允许将出于管理目的 IP 地址的配置，但它不是必需的如中所示[创建 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md#create)。

如 WSFC，Pacemaker 希望使用冗余网络，这意味着不同的网卡 （Nic 或物理机 pNICs） 具有单个 IP 地址。 根据群集配置，即其自己环必须每个 IP 地址。 但是，与 Wsfc 如今，许多实现被虚拟化或公有云在实际上只有一个虚拟化 NIC (vNIC) 提供给服务器。 如果所有 pNICs 和 Vnic 都连接到同一个物理或虚拟交换机，则没有真正的冗余在网络层上，因此配置多个 Nic 是一种虚拟到虚拟机的位。 网络冗余通常内置虚拟化部署的虚拟机监控程序，肯定构建到公有云。

使用多个 Nic 和 WSFC 和 Pacemaker 的一个区别是 Pacemaker 允许多个 IP 地址位于同一子网，而不为 WSFC。 多子网和 Linux 群集的详细信息，请参阅文章[配置多个子网](sql-server-linux-configure-multiple-subnet.md)。

### <a name="quorum-and-stonith"></a>仲裁和 STONITH
仲裁配置和要求的可用性组或特定于 FCI 的部署与相关[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

支持的 Pacemaker 群集需要 STONITH。 使用从分发的文档来配置 STONITH。 例如，在[基于存储的隔离](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)sles。 此外，还有用于基于 ESXI 的解决方案的 VMware vCenter 的 STONITH 代理。 有关详细信息，请参阅[VMWare VM VCenter SOAP 针对围栏进行过 (Unofficial) Stonith 插件代理](https://github.com/olafrv/fence_vmware_soap)。

> [!NOTE]
> 在撰写本文时，HYPER-V 并没有一种解决方案的 STONITH。 这是适用于本地部署，也会影响使用 RHEL 等某些分发版的基于 Azure 的 Pacemaker 部署。

### <a name="interoperability"></a>互操作性
本部分介绍使用 WSFC 或 Linux 其他发行版基于 Linux 的群集的交互方式。

#### <a name="wsfc"></a>WSFC
目前，为 WSFC 和 Pacemaker 群集协同工作没有直接的方法。 这意味着没有方法来创建 AG 或 FCI 跨 WSFC 和 Pacemaker。 但是，有两个互操作性解决方案，这两种专为 Ag。 FCI 可以参与跨平台配置的唯一方法是其所参与为这两种方案之一中的一个实例：
-   为无群集类型 AG。 有关详细信息，请参阅 Windows[可用性组文档](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分布式的 AG，这是一种特殊类型的允许两个不同的 Ag，若要配置为其自身的可用性组的可用性组。 分布式 Ag 的详细信息，请参阅文档[分布式可用性组](../database-engine/availability-groups/windows/distributed-availability-groups.md)。

#### <a name="other-linux-distributions"></a>其他 Linux 发行版
在 Linux 上，Pacemaker 群集的所有节点必须都位于相同的分布区上。 例如，这意味着 RHEL 节点不能为具有 SLES 节点的 Pacemaker 群集的一部分。 在以前说明主要原因： 分发可能具有不同版本和功能，因此操作可能无法正常工作。 混合使用发行版具有混合使用 Wsfc 和 Linux 位于同一文章： 使用无或分布式 Ag。

## <a name="next-steps"></a>后续步骤
[在 Linux 上的 SQL Server 的部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)
