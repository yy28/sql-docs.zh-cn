---
title: 有关 Linux 部署的 SQL Server 可用性基础知识
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d597033e6ad09a735e621518883cedda6bef29a2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243590"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>有关 Linux 部署的 SQL Server 可用性基础知识

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

从 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 开始，Linux 和 Windows 都支持 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 与基于 Windows 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署一样，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 数据库和实例需要在 Linux 下高度可用。 本文介绍了规划和部署基于 Linux 的高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 数据库和实例的技术方面，以及与基于 Windows 的安装的一些区别。 因为 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 对于 Linux 专业人员来说可能是新内容，而 Linux 对于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 专业人员来说可能是新内容，所以这篇文章有时会介绍一些人熟悉，而其他人不熟悉的概念。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Linux 部署的可用性选项
除备份和还原之外，Linux 上还提供了与基于 Windows 的部署相同的三种可用性功能：
-   Always On 可用性组 (AG)
-   Always On 故障转移群集实例 (FCI)
-   [日志传送](sql-server-linux-use-log-shipping.md)

在 Windows 上，FCI 始终需要一个基础 Windows Server 故障转移群集 (WSFC)。 根据部署方案，AG 通常需要基础 WSFC，但 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] 中的新 None 变量除外。 在 Linux 中不存在 WSFC。 Linux 中的群集实现将在 [Linux 上 Always On 可用性组和故障转移群集实例的 Pacemaker](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux) 一节进行讨论。

## <a name="a-quick-linux-primer"></a>Linux 快速入门
虽然有些 Linux 安装可以通过接口完成，但大多数安装都不是，这意味着操作系统层的几乎所有工作都是通过命令行完成的。 在Linux 环境中，此命令行的常用术语是 bash shell  。

在 Linux 中，许多命令需要以提升的权限执行，就像作为管理员需要在 Windows 服务器中执行许多操作一样。 使用提升的权限执行有两种主要方法：
1. 在适当用户的上下文中运行。 若要更改为其他用户，请使用命令 `su`。 如果 `su` 在没有用户名的情况下独立执行，那么只要你知道密码，你现在就将作为根处于 shell 中  。
   
2. 运行事务更常见、更安全的做法是，在执行任何操作之前使用 `sudo`。 本文中的许多示例都使用了 `sudo`。

一些常见命令，每个命令都包含各种可联机研究的开关和选项：
-   `cd` - 更改目录
-   `chmod` - 更改文件或目录的权限
-   `chown` - 更改文件或目录的所有权
-   `ls` - 显示目录的内容
-   `mkdir` - 在驱动器上创建文件夹（目录）
-   `mv` - 将文件从一个位置移动到另一个位置。
-   `ps` -显示所有工作进程
-   `rm` - 在服务器上本地删除文件
-   `rmdir` - 删除文件夹（目录）
-   `systemctl` - 启动、停止或启用服务
-   文本编辑器命令。 在 Linux 上，有各种文本编辑器选项，例如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Linux 上的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的可用性配置的常见任务
本节介绍所有基于 Linux 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署的常见任务。

### <a name="ensure-that-files-can-be-copied"></a>确保可以复制文件
将文件从一台服务器复制到另一台服务器是一项任何人使用 Linux 上的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 都应该能够完成的任务。 此任务对 AG 配置非常重要。

在 Linux 和基于 Windows 的安装上都可能存在权限等问题。 但是，那些熟悉如何在 Windows 上从服务器复制到服务器的人可能不熟悉在 Linux 上如何完成此操作。 常见方法是使用代表安全复制的命令行实用工具 `scp`。 在后台，`scp` 使用 OpenSSH。 SSH 代表安全外壳。 根据 Linux 分发版，可能未安装 OpenSSH 本身。 如果未安装，则需要先安装 OpenSSH。 有关配置 OpenSSH 的详细信息，请参阅以下链接中有关每个分发版的信息：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

使用 `scp` 时，如果服务器不是源或目标，则必须提供服务器的凭据。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

将文件 MyAGCert.cer 复制到另一台服务器上指定的文件夹。 请注意，必须具有要复制文件的权限（可能还包括所有权），因此在复制之前可能还需要使用 `chown`。 同样，在接收端，正确的用户需要访问权限来操作文件。 例如，要还原该证书文件，`mssql` 用户必须能够访问该文件。

Samba 是服务器消息块 (SMB) 的 Linux 变体，也可用于创建由 UNC 路径（例如 `\\SERVERNAME\SHARE`）访问的共享。 有关配置 Samba 的详细信息，请参阅以下链接中有关每个分发版的信息：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

也可以使用基于 Windows 的 SMB 共享；SMB 共享不需要基于 Linux，只要在托管 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 Linux 服务器上正确配置 Samba 的客户端部分，且共享具有正确的访问权限。 对于混合环境中的用户，通过这种方法可利用基于 Linux 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署的现有基础结构。

重要的一点是，部署的 Samba 版本应符合 SMB 3.0 标准。 在 [!INCLUDE[sssql11-md](../includes/sssql11-md.md)] 中添加 SMB 支持时，它需要所有共享支持 SMB 3.0。 如果使用 Samba 作为共享而不是 Windows Server，则基于 Samba 的共享应使用 Samba 4.0 或更高版本，理想情况下应使用支持 SMB 3.1.1 的 4.3 或更高版本。 有个 SMB 和 Linux 的信息，请参阅 [Samba 中的 SMB3](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)。

最后，可选择使用网络文件系统 (NFS) 共享。 在基于 Windows 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署中，无法使用 NFS，只能在基于 Linux 的部署中使用 NFS。

### <a name="configure-the-firewall"></a>配置防火墙
与 Windows 类似，Linux 分发版也具有内置防火墙。 如果你的公司正在服务器上使用外部防火墙，那么在 Linux 中禁用防火墙可能是可以接受的。 但是，无论在何处启用防火墙，都需要打开端口。 下表列出了 Linux 上高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署所需的公共端口。

| 端口号 | 类型     | 说明                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS - `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba（如果使用）- 终结点映射程序                                                                                          |
| 137         | UDP      | Samba（如果使用）- NetBIOS 名称服务                                                                                      |
| 138         | UDP      | Samba（如果使用）- NetBIOS 数据报                                                                                          |
| 139         | TCP      | Samba（如果使用）- NetBIOS 会话                                                                                           |
| 445         | TCP      | Samba（如果使用）- SMB over TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - 默认端口；如果需要，可以随 `mssql-conf set network.tcpport <portnumber>` 改变                       |
| 2049        | TCP、UDP | NFS（如果使用）                                                                                                               |
| 2224        | TCP      | Pacemaker - 由 `pcsd` 使用                                                                                                |
| 3121        | TCP      | Pacemaker - 如果存在 Pacemaker 远程节点，则为必需项                                                                    |
| 3260        | TCP      | iSCSI 发起程序（如果使用）- 可以在 `/etc/iscsi/iscsid.config` (RHEL) 中更改，但应与 iSCSI 目标的端口匹配 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] - 用于 AG 终结点的默认端口；可以在创建终结点时更改                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker - 如果使用多播 UDP，则为 Corosync 所需                                                                     |
| 5405        | UDP      | Pacemaker - Corosync 所需                                                                                            |
| 21064       | TCP      | Pacemaker - 使用 DLM 的资源所需                                                                                 |
| 变量    | TCP      | AG 终结点端口；默认值是 5022                                                                                           |
| 变量    | TCP      | NFS - `LOCKD_TCPPORT` 的端口（位于 RHEL 上的 `/etc/sysconfig/nfs` 中）                                              |
| 变量    | UDP      | NFS - `LOCKD_UDPPORT` 的端口（位于 RHEL 上的 `/etc/sysconfig/nfs` 中）                                              |
| 变量    | TCP/UDP  | NFS - `MOUNTD_PORT` 的端口（位于 RHEL 上的 `/etc/sysconfig/nfs` 中）                                                |
| 变量    | TCP/UDP  | NFS - `STATD_PORT` 的端口（位于 RHEL 上的 `/etc/sysconfig/nfs` 中）                                                 |

有关 Samba 可能使用的其他端口，请参阅 [Samba 端口使用情况](https://wiki.samba.org/index.php/Samba_Port_Usage)。

相反，Linux 下的服务名称也可以添加为异常而不是端口；例如，Pacemaker 为 `high-availability`。 如果这是你想要采用的方向，请参阅分发版中的名称。 例如，在 RHEL 上，要在 Pacemaker 中添加的命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火墙文档：**
-   [RHEL](https://access.redhat.com/documentation/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>安装 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 包以实现可用性
在基于 Windows 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 安装中，有些组件甚至可以在基本引擎安装中安装，而其他组件则不能。 在 Linux 下，只有 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 引擎作为安装过程的一部分进行安装。 其他全部内容都是可选的。 对于 Linux 下的高可用性 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 实例，应使用 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 安装两个包：[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理 (mssql-server-agent) 和高可用性 (HA) 包 (mssql-server-ha)   。 虽然 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理在技术上是可选的，但它是 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的作业计划程序，并且是日志传送所必需的，因此建议安装。 在基于 Windows 的安装中，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理是不可选的。

>[!NOTE]
>对于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的新用户，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理是 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的内置作业计划程序。 这是 DBA 计划备份和其他 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 维护等内容的常见方法。 与 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的基于 Windows 的安装不同，其中 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理是完全不同的服务，在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理在 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 自身的上下文中运行。

在基于 Windows 的配置上配置 AG 或 FCI 时，它们可识别群集。 群集感知意味着 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 具有 WSFC 了解的特定资源 DLL（用于 FCI 的 sqagtres.dll 和 sqsrvres.dll 以及用于 AG 的 hadrres.dll），并由 WSFC 使用以确保 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 群集功能正常启动和运行。 由于群集不仅对于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 是外部的，而且对于 Linux 本身也是外部的，因此 Microsoft 必须为基于 Linux 的 AG 和 FCI 部署编写与资源 DLL 等价的代码。 这是 mssql-server-ha 包，也称为 Pacemaker 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 资源代理  。 若要安装 mssql-server-ha 包，请参阅[安装 HA 和 SQL Server 代理包](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)  。

其他用于 Linux 上的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 全文搜索 (mssql-server-fts) 和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (mssql-server-is) 的可选包对于高可用性、FCI 或 AG 都不是必需的   。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Linux 上的 AlwaysOn 可用性组和故障转移群集实例的 Pacemaker
如前所述，目前 Microsoft 支持的唯一用于 AG 和 FCI 的群集机制就是具有 Corosync 的 Pacemaker。 本节介绍理解该解决方案的基本信息，以及如何为 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 配置规划和部署该解决方案。

### <a name="ha-add-onextension-basics"></a>HA 加载项/扩展基础知识
所有当前支持分发版都提供基于 Pacemaker 群集堆栈的高可用性加载项/扩展。 此堆栈包含两个关键组件：Pacemaker 和 Corosync。 堆栈的所有组件如下：
-   Pacemaker - 核心群集组件，可以在群集计算机之间进行协调。
-   Corosync - 框架和一组 API，提供仲裁、重启失败进程等功能。
-   libQB - 提供日志记录等功能。
-   资源代理 - 提供特定功能，以便应用程序可以与 Pacemaker 集成。
-   Fence 代理 - 脚本/功能，有助于隔离节点并在遇到问题时对其进行处理。
    
> [!NOTE]
> 在 Linux 环境中，群集堆栈通常被称为 Pacemaker。

此解决方案在某些方面与使用 Windows 部署群集配置相似，但在许多方面不同。 在 Windows 中，群集的可用性形式称为 Windows 服务器故障转移群集 (WSFC)，它内置于操作系统中，并且默认情况下启用创建 WSFC（故障转移群集）的功能处于禁用状态。 在 Windows 中，AG 和 FCI 基于 WSFC 构建，并且由于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 提供的特定资源 DLL 而共享紧密集成。 这种紧密耦合的解决方案在很大程度上是可能的，因为它都来自一个供应商。

![](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上，虽然每个支持的分发版都有可用的 Pacemaker，但每个分发版都可以自定义，且具有稍微不同的实现和版本。 本文说明部分将介绍其中一些差异。 群集层是开放源代码，因此即使它随分发版一起发布，也不像 Windows 下的 WSFC 那样紧密集成。 这就是 Microsoft 提供 mssql-server-ha 的原因，这样 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 和 Pacemaker 堆栈就可以为 AG 和 FCI 提供接近但不完全相同的体验，就像在 Windows 下一样  。

有关 Pacemaker 的完整文档，包括关于 RHEL 和 SLES 的所有内容更深入的阐释和完整的参考信息：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 没有可用性指南。

有关整个堆栈的详细信息，另请参阅 Clusterlabs 站点上的官方 [Pacemaker 文档页](https://clusterlabs.org/doc/)。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念和术语
本节介绍了 Pacemaker 实现的常见概念和术语。

#### <a name="node"></a>节点
节点是参与群集的服务器。 Pacemaker 群集本机最多支持 16 个节点。 如果 Corosync 未在其他节点上运行，则可以超过此数量，但 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 需要 Corosync。 因此，对于任何基于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的配置，群集可以拥有的最大节点数都是 16；这是 Pacemaker 限制，与 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 施加的 AG 或 FCI 的最大限制无关。 

#### <a name="resource"></a>资源
WSFC 和 Pacemaker WSFC 群集都有资源的概念。 资源是在群集上下文中运行的特定功能，例如磁盘或 IP 地址。 例如，在 Pacemaker 下，可以创建 FCI 和 AG 资源。 这与在 WSFC 中完成的操作没有什么不同，在配置 AG 时，你可以看到 FCI 或 AG 资源的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 资源，但是由于 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 与 Pacemaker 集成方式的潜在差异，又并不完全相同。

Pacemaker 具有标准资源和克隆资源。 克隆资源是在所有节点上同时运行的资源。 例如，在多个节点上运行以实现负载均衡的 IP 地址。 为 FCI 创建的任何资源都使用标准资源，因为在任何给定时间只有一个节点可以托管 FCI。

创建 AG 时，它需要一种特殊形式的克隆资源（称为多状态资源）。 虽然 AG 只有一个主要副本，但 AG 本身可以跨所有配置的节点运行，并且可能允许诸如只读访问之类的操作。 因为这是对节点的“实时”使用，所以资源有两种状态的概念：主状态和从状态。 有关详细信息，请参阅[多状态资源：具有多种模式的资源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>资源组/集
与 WSFC 中的角色类似，Pacemaker 群集也具有资源组的概念。 资源组（在 SLES 中称为“集”）是一起运行的资源集合，可以作为单个单元从一个节点故障转移到另一个节点。 资源组不能包含配置为主/从的资源；因此，它们不能用于 AG。 虽然资源组可用于 FCI，但通常不建议使用该配置。

#### <a name="constraints"></a>约束
WSFC 具有各种资源参数以及依赖项，以此说明 WSFC 两个不同资源之间的父/子关系。 依赖项只是一个规则，指示 WSFC 哪个资源需要首先联机。

Pacemaker 群集没有依赖项的概念，但有一些约束。 有三种约束：托管、位置和排序。
-   托管约束强制执行是否应在同一节点上运行两个资源。
-   位置约束指示 Pacemaker 群集资源可以（或无法）运行的位置。
-   排序约束指示 Pacemaker 群集资源应该开始的顺序。

> [!NOTE]
> 资源组中的资源不需要托管约束，因为所有这些资源都被视为一个单元。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁、隔离代理和 STONITH
Pacemaker 下的仲裁在概念上与 WSFC 有些相似。 群集仲裁机制的主要目的是确保群集保持正常运行。 用于 Linux 分发版的 WSFC 和 HA 加载项都具有投票的概念，其中每个节点都计入仲裁。 你需要大多数投票支持，否则，在最糟糕的情况下，群集将被关闭。

与 WSFC 不同，没有见证资源可用于仲裁。 与 WSFC 一样，目标都是保持投票人数为奇数。 仲裁配置对 AG 的考虑因素与 FCI 不同。

WSFC 监视参与节点的状态，并在出现问题时进行处理。 WSFC 更高版本提供了诸如隔离行为不正常或不可用的节点（节点未打开、网络通信关闭等）等功能。 在 Linux 端，这种类型的功能是由隔离代理提供的。 此概念有时被称为隔离。 不过，这些隔离代理通常是特定于部署的，并且通常由硬件供应商和部分软件供应商（例如提供虚拟机监控程序的供应商）提供。 例如，VMware 提供了一个隔离代理，可用于使用 vSphere 虚拟化的 Linux VM。

仲裁和隔离与另一个称为 STONITH（或“爆头”）的概念联系到一起。 STONITH 需要在所有 Linux 分发版上都支持 Pacemaker 群集。 有关更多信息，请参阅 [高可用性群集中的隔离](https://access.redhat.com/solutions/15575) (RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf` 文件包含群集的配置。 该文件位于 `/etc/corosync`。 在正常日常操作过程中，如果群集设置正确，则永远不必编辑此文件。

#### <a name="cluster-log-location"></a>群集日志位置
Pacemaker 群集的日志位置因分发版而异。
-   RHEL 和 SLES - `/var/log/cluster/corosync.log`
-   Ubuntu - `/var/log/corosync/corosync.log`

若要更改默认日志记录位置，请修改 `corosync.conf`。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>计划 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 Pacemaker 群集
本部分讨论 Pacemaker 群集的重要规划点。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>为 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 虚拟化基于 Linux 的 Pacemaker 群集
使用虚拟机为 AG 和 FCI 部署基于 Linux 的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署的规则与基于 Windows 的对应规则相同。 Microsoft 在 [Microsoft 支持知识库 956893](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment) 中提供了一组基本规则，用于支持虚拟化 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 部署。 由于平台本身的差异，不同的虚拟机监控程序（如 Microsoft 的 Hyper-V 和 VMware 的 ESXi）可能会有不同的差异。

对于虚拟化下的 AG 和 FCI，请确保为给定 Pacemaker 群集的节点设置了反关联性。 在 AG 或 FCI 配置中配置为高可用性时，托管 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 VM 不应在同一虚拟机监控程序主机上运行。 例如，如果部署了双节点 FCI，则需要至少有三个虚拟机监控程序主机，以便在主机发生故障时，特别是使用 Live Migration 或 vMotion 等功能时，其中一个托管节点的 VM 可以找到某个位置  。

有关更多详细信息，请参阅：
-   Hyper-V 文档 - [Using Guest Clustering for High Availability](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)（使用来宾群集实现高可用性）
-   白皮书（专为基于 Windows 的部署编写，但大多数概念仍然适用）- [Planning Highly Available, Mission Critical SQL Server Deployments with VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)（使用 VMware vSphere 规划高可用性、关键任务 SQL Server 部署）

### <a name="networking"></a>网络
与 WSFC 不同，Pacemaker 不需要 Pacemaker 群集本身的专用名称或至少一个专用 IP 地址。 由于没有网络名称资源，AG 和 FCI 将需要 IP 地址（请参阅每个文档以获取更多信息），但不需要名称。 SLES 允许配置 IP 地址用于管理目的，但不是必需的，如[创建 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md#create)中所示。

与 WSFC 一样，Pacemaker 更倾向于使用冗余网络，即具有独立 IP 地址的不同网卡（用于物理的 NIC 或 pNIC）。 就群集配置而言，每个 IP 地址都具有所谓的其自己的环。 但是，与如今的 WSFC 一样，许多实现都是虚拟化的，或者在公有云中，实际上只有一个虚拟化 NIC (vNIC) 呈现给服务器。 如果所有 pNIC 和 vNIC 都连接到同一个物理或虚拟交换机上，那么在网络层上就没有真正的冗余，因此配置多个 NIC 对虚拟机来说是一种错觉。 网络冗余通常内置于虚拟化部署的虚拟机监控程序中，并且明确内置于公有云中。

多个 NIC 和 Pacemaker 与 WSFC 的区别在于，Pacemaker 允许在同一子网上使用多个 IP 地址，而 WSFC 则不允许。 有关多个子网和 Linux 群集的详细信息，请参阅文章[配置多个子网](sql-server-linux-configure-multiple-subnet.md)。

### <a name="quorum-and-stonith"></a>仲裁和 STONITH
仲裁配置和要求与 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的 AG 或 FCI 特定部署相关。

支持的 Pacemaker 群集需要 STONITH。 使用分发版中的文档来配置 STONITH。 相关示例，请参阅 SLES 的 [Storage-based Fencing](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)（基于存储的隔离）。 对于基于 ESXi 的解决方案，还有一个针对 VMware vCenter 的 STONITH 代理。 有关详细信息，请参阅 [Stonith Plugin Agent for VMWare VM VCenter SOAP Fencing (Unofficial)](https://github.com/olafrv/fence_vmware_soap)（适用于 VMWare VM VCenter SOAP 隔离的 Stonith 插件代理（非正式））。

### <a name="interoperability"></a>互操作性
本部分介绍基于 Linux 的群集如何与 WSFC 或 Linux 的其他分发版进行交互。

#### <a name="wsfc"></a>WSFC
目前，WSFC 和 Pacemaker 群集无法直接协同工作。 这意味着无法创建适用于 WSFC 和 Pacemaker 的 AG 或 FCI。 但是，有两种互操作性解决方案，这两种解决方案都是为 AG 设计的。 FCI 参与跨平台配置的唯一方法是，它作为以下两种情况之一的实例参与：
-   群集类型为 None 的 AG。 有关详细信息，请参阅 Windows [可用性组文档](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分布式 AG 是一种特殊类型的可用性组，允许将两个不同的 AG 配置为自己的可用性组。 有关分布式 AG 的详细信息，请参阅文档[分布式可用性组](../database-engine/availability-groups/windows/distributed-availability-groups.md)。

#### <a name="other-linux-distributions"></a>其他 Linux 分发版
在 Linux 上，Pacemaker 群集的所有节点必须位于同一分发版上。 例如，这意味着 RHEL 节点不能属于具有 SLES 节点的 Pacemaker 群集。 关于这一点，之前说明的主要原因是：分发版可能具有不同的版本和功能，因此无法正常工作。 混合分发版与混合 WSFC 和 Linux 的情况相同：使用 None 或分布式 AG。

## <a name="next-steps"></a>后续步骤
[为 Linux 上的 SQL Server 部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)
