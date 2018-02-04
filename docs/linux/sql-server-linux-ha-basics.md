---
title: "SQL Server 可用性 Linux 部署的基础知识 |Microsoft 文档"
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
ms.workload: On Demand
ms.openlocfilehash: d53e54c6e8e74970316de557ddf3bd60a09e9ffe
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>SQL Server 可用性 Linux 部署的基础知识

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

从开始[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]支持 Linux 和 Windows 上。 像基于 Windows 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]数据库和实例需要在 Linux 下高度可用。 本文介绍如何规划和部署高度可用的技术方面基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]数据库和实例，以及从基于 Windows 的安装的区别。 因为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 专业人员和 Linux 可能用于的新功能可能新[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]专业人员、 文章有时介绍了可能是为某些所熟悉并且不给其他人熟悉的概念。

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]对于 Linux 部署的可用性选项
除了备份和还原，相同的三个可用性功能均可用在 Linux 上与基于 Windows 的部署:
-   Always On 可用性组 （承载个可用性组）
-   Always On 故障转移群集实例 (Fci)
-   [日志传送](sql-server-linux-use-log-shipping.md)

在 Windows 上，Fci 始终要求基础的 Windows Server 故障转移群集 (WSFC)。 根据部署方案中，可用性组通常需要基础 WSFC 中，使用的例外是新 variant 中无[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 WSFC Linux 中不存在。 群集在 Linux 中的实现下面将讨论在[Pacemaker Alwayson 可用性组和故障转移群集实例在 Linux 上](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux)。

## <a name="a-quick-linux-primer"></a>快速的 Linux 入门
虽然某些 Linux 安装，可能会安装接口大多数但不是，这意味着在操作系统层几乎所有操作通过命令行。 Linux 世界上的此命令行的常用术语是*bash shell*。

在 Linux 中，很多命令需要执行使用提升的权限，一样很多东西需要以管理员身份的 Windows Server 中完成。 有两个主要方法使用提升的权限执行：
1. 在正确的用户的上下文中运行。 若要将更改为不同的用户，使用命令`su`。 如果`su`执行其自身上没有用户名，只要你知道的密码，你现在将作为 shell 中*根*。
   
2. 多个常规和安全意识运行的方式操作是使用`sudo`之前执行任何操作。 在此示例的许多文章使用`sudo`。

某些常用命令，其中每个都有各种开关和可以联机研究的选项：
-   `cd`– 将目录更改
-   `chmod`– 更改的文件或目录的权限
-   `chown`– 更改的文件或目录的所有权
-   `ls`– 显示一个目录的内容
-   `mkdir`– 驱动器上创建文件夹 （目录）
-   `mv`-将文件从一个位置移到另一个
-   `ps`– 显示的所有工作进程
-   `rm`– 删除本地服务器上的文件
-   `rmdir`– 删除文件夹 （目录）
-   `systemctl`– 启动、 停止或启用服务
-   文本编辑器命令。 在 Linux 上，有各种文本编辑器选项，如 vi 和 emacs。

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>常见任务的可用性配置[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上
本部分介绍任务所共有的基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

### <a name="ensure-that-files-can-be-copied"></a>确保可以复制文件
一件事情的任何人都使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上应能够执行是将文件从一台服务器复制到另一个。 此任务是非常重要的可用性组配置。

在 Linux 上以及在基于 Windows 的安装，可以存在权限问题等。 但是，熟悉如何在 Windows 上复制从服务器到服务器的那些可能不熟悉如何在 Linux 上执行。 一种常用方法是使用命令行实用工具`scp`，这代表安全的复制。 在后台，`scp`使用 OpenSSH。 SSH 代表安全 shell。 Linux 分发中，可能未安装了 OpenSSH 本身。 如果不是这样，OpenSSH 将需要先安装。 有关配置 OpenSSH 的详细信息，请参阅以下链接了解每个分布的信息：
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

使用时`scp`，如果不是源或目标，必须提供服务器的凭据。 例如，使用

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

将文件 MyAGCert.cer 复制到指定的其他服务器上的文件夹。 请注意，你必须拥有权限 –，还可能要复制，因此的文件的所有权 –`chown`可能还需要在复制前使用。 同样，在接收端，适当的用户需要访问和操作的文件。 例如，若要还原该证书的文件，`mssql`用户必须能够访问它。

Samba，这是服务器消息块 (SMB) 的 Linux 变体，还可以用于创建共享访问的 UNC 路径如`\\SERVERNAME\SHARE`。 有关配置 Samba 的详细信息，请参阅以下链接了解每个分布的信息：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

此外可以使用基于 Windows 的 SMB 共享;SMB 共享不需要是基于 Linux 的只要在 Linux 服务器承载上正确配置 Samba 的客户端部分[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和共享具有正确的访问权限。 对于那些在混合环境，这将是一种方法以利用现有基础结构的基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署。

非常重要的一点是 Samba 部署的版本应为符合 SMB 3.0。 在添加 SMB 的支持时[!INCLUDE[sssql11-md](../includes/sssql11-md.md)]，它需要给支持 SMB 3.0 的所有共享。 如果使用 Samba 共享和不 Windows Server，Samba 4.0 或更高版本，理想情况下 4.3 和更高版本，支持 SMB 3.1.1 应使用基于 Samba 共享。 良好的 SMB 和 Linux 上的信息来源是[Samba 中的 SMB3](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf)。

最后，使用的网络文件系统 (NFS) 共享是一个选项。 使用 NFS 不是基于 Windows 的部署上选项[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，并且仅用于基于 Linux 的部署。

### <a name="configure-the-firewall"></a>配置防火墙
类似于 Windows，Linux 分发版具有内置的防火墙。 如果你的公司使用外部防火墙的服务器，禁用在 Linux 中的防火墙可能是接受的。 但是，无论都启用了防火墙端口需要打开。 下表描述所需的公共端口高度可用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上的部署。

| 端口号 | 类型     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba （如果使用） – 终结点映射程序                                                                                          |
| 137         | UDP      | Samba （如果使用） – NetBIOS 名称服务                                                                                      |
| 138         | UDP      | Samba （如果使用） – NetBIOS 数据报                                                                                          |
| 139         | TCP      | Samba （如果使用） – NetBIOS 会话                                                                                           |
| 445         | TCP      | Samba （如果使用） – 通过 TCP 的 SMB                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – 默认端口，则为如果需要，可以更改与`mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP、UDP | NFS （如果使用）                                                                                                               |
| 2224        | TCP      | Pacemaker – 使用通过`pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker – 所需是否存在 Pacemaker 远程节点                                                                    |
| 3260        | TCP      | iSCSI 发起程序 （如果使用） – 可以在修改`/etc/iscsi/iscsid.config`(RHEL)，但应匹配的 iSCSI 目标端口 |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 的默认端口用于可用性组终结点;创建终结点时，可以更改                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker – 如果使用多播的 UDP，Corosync 所需                                                                     |
| 5405        | UDP      | Pacemaker – 所需的 Corosync                                                                                            |
| 21064       | TCP      | Pacemaker – 所需的资源使用 DLM                                                                                 |
| 变量    | TCP      | 可用性组终结点端口，则为默认值为 5022                                                                                           |
| 变量    | TCP      | NFS – 端口用于`LOCKD_TCPPORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                              |
| 变量    | UDP      | NFS – 端口用于`LOCKD_UDPPORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                              |
| 变量    | TCP/UDP  | NFS – 端口用于`MOUNTD_PORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                                |
| 变量    | TCP/UDP  | NFS – 端口用于`STATD_PORT`(位于`/etc/sysconfig/nfs`RHEL 上)                                                 |

对于 Samba 可能使用的其他端口，请参阅[Samba 端口用法](https://wiki.samba.org/index.php/Samba_Port_Usage)。

相反，在 Linux 下服务的名称也都可以作为异常而不是端口; 添加例如，`high-availability`使 Pacemaker。 如果这是你想要使用的方向，请参阅你的分发的名称。 例如，在 RHEL Pacemaker 中添加的命令是

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**防火墙文档：**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>安装[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]可用性的包
在基于 Windows 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安装，而有些则不是即使在基本引擎的安装中，安装某些组件。 在仅限 Linux[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]作为安装过程的一部分安装引擎。 其他所有内容是可选的。 为高度可用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 下的实例，应与安装两个包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]:[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理 (*mssql server 代理*) 和高可用性 (HA) 包 (*mssql-服务器-ha*)。 虽然[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理是从技术上讲可选的它是[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的计划程序作业和所必需的日志传送，因此，建议安装。 在基于 Windows 的安装，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理不是可选的。

>[!NOTE]
>对于那些新手[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的内置作业计划程序。 它是有关 Dba 计划等备份和其他的常用方法[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]维护。 与不同的基于 Windows 的安装[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]其中[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理是一个完全不同的服务，在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]上下文中运行代理[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]本身。

当承载个可用性组或 Fci 在基于 Windows 的配置中配置时，它们是群集感知。 群集感知意味着[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]具有特定资源 WSFC 就会了解有关 （sqagtres.dll 和 Fci，承载个可用性组的 hadrres.dll 的 sqsrvres.dll） 的 Dll 和 WSFC 用于确保[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]群集的功能已启用、 运行，和正常工作。 因为群集外部不是仅为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]但 Linux 本身、 Microsoft 不得不代码基于 Linux 的可用性组和 FCI 部署的资源 DLL 的等效项。 这是*mssql-服务器-ha*包，也称为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Pacemaker 的资源代理。 若要安装*mssql-服务器-ha*包，请参阅[安装高可用性和 SQL Server 代理包](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages)。

有关其他可选包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的全文搜索 (*mssql server fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql 服务器是*)，不是所需的高可用性，FCI 或可用性组。

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>为 Alwayson 可用性组和 Linux 上的故障转移群集实例的 pacemaker
如上所述，于承载个可用性组和 Fci 当前支持 Microsoft 的唯一聚类分析机制是与 Corosync Pacemaker。 本部分介绍基本的信息，以了解该解决方案，以及如何规划和部署为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]配置。

### <a name="ha-add-onextension-basics"></a>HA 上加载/扩展基础知识
所有当前受支持的分发提供高可用性加载-上/扩展，该扩展基于群集堆栈 Pacemaker。 此堆栈包含两个关键组件： Pacemaker 和 Corosync。 堆栈的所有组件都包括：
-   Pacemaker – 群集组件，请在群集的计算机之间执行诸如坐标的核心。
-   Corosync – 一个 framework 和一组 api，提供了诸如仲裁，重新启动失败过程和等等的能力。
-   libQB – 提供像日志记录。
-   资源代理 – 提供，以便应用程序可以与 Pacemaker 集成的特定功能。
-   围墙代理 – 脚本/功能帮助隔离节点，如果它们也有问题处理它们。
    
> [!NOTE]
> 群集堆栈通常称为 Pacemaker Linux 世界上的。

此解决方案是在某些方面相似，但在许多方面不同于部署使用 Windows 的群集的配置。 在 Windows 中，可用性形式的群集，称为 Windows Server 故障转移群集 (WSFC)，内置于操作系统，并允许创建 WSFC，故障转移群集，默认情况下禁用的功能。 在 Windows 中，承载个可用性组和 Fci 的构建基于 WSFC 中，和共享的紧密集成，因为特定资源 DLL，即提供[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 此紧密耦合的解决方案是可能一般说来因为它是所有从一个供应商联系。

![](./media/sql-server-linux-ha-basics/image1.png)

在 Linux 上，而每个支持的分发具有 Pacemaker 可用，则每个分布可自定义并使略有不同的实现和版本。 一些差异将反映在本文中的说明进行操作。 聚类分析层是开放源代码，因此，即使它附带了分布时，它不紧密集成的方式相同 WSFC 都是在 Windows 下。 这就是 Microsoft 提供了原因*mssql-服务器-ha*，以便[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]和 Pacemaker 堆栈可以提供接近，但不完全相同，遇到 Fci 承载个可用性组以及在 Windows 下如。

Pacemaker 的完整文档，其中包括的所有内容是使用完整的参考信息，以及 RHEL SLES 什么的更深入说明：
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu 没有可用性的指南。

有关整个堆栈的详细信息，另请参阅官方[Pacemaker 文档页](http://clusterlabs.org/doc/)Clusterlabs 站点上。

### <a name="pacemaker-concepts-and-terminology"></a>Pacemaker 概念和术语
本部分介绍了常见的概念和术语 Pacemaker 实现。

#### <a name="node"></a>节点
节点是参与到群集中的服务器。 Pacemaker 群集以本机方式支持最多 16 节点。 如果未在其他节点上运行 Corosync 但 Corosync 是所必需的可能会超过此数字[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 因此，最大节点数的群集可拥有任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-基于的配置为 16; 这是 Pacemaker 限制，并且有与承载个可用性组或 Fci 强加的最大限制无关[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 

#### <a name="resource"></a>资源
WSFC 和 Pacemaker 群集具有资源的概念。 资源是在该群集，如磁盘或 IP 地址的上下文中运行的特定功能。 例如下 Pacemaker, FCI 和可用性组资源可以获取创建。 这不是在 WSFC 中，你会看到其中执行什么操作到不同[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]为 FCI 资源或配置可用性组时的可用性组资源，但较不完全相同方式存在差异的基础[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]与 Pacemaker 集成。

Pacemaker 没有标准版和克隆的资源。 克隆资源是在所有节点上同时运行。 示例是实现负载平衡的多个节点运行的 IP 地址。 获取为 Fci 创建任何资源使用标准资源，因为在任何给定时间，只有一个节点可以承载 FCI。

创建可用性组时，它需要一种特殊的形式的名为多状态的资源的克隆资源。 尽管可用性组仅有一个主副本，可用性组本身正在运行，在所有节点配置为使用，并可能允许只读访问权限等。 由于这是节点的"实时"使用时，资源都具有两个状态的概念： 主从。 有关详细信息，请参阅[多状态资源： 具有多个模式的资源](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html)。

#### <a name="resource-groupssets"></a>资源组/设置
类似于在 WSFC 中的角色，Pacemaker 群集提供的资源组的概念。 资源组 （称为 SLES 中的一组） 是一起工作，并且可以从故障转移一个节点到另一个作为一个单元的资源的集合。 资源组不能包含配置为主/从; 的资源因此，它们不用于承载个可用性组。 虽然资源组可以用于在多个 Fci 中，它不通常是建议的配置。

#### <a name="constraints"></a>约束
WSFCs 具有资源，以及依赖关系，可告诉的两个不同的资源之间的父/子关系 WSFC 等的各种参数。 依赖关系是只是告诉 WSFC 哪些资源需要首先处于联机状态的规则。

Pacemaker 群集不具有依赖关系的概念，但有一些约束。 有三种类型的约束： 归置、 位置和排序。
-   归置约束强制执行应在同一个节点上运行两个资源。
-   位置约束告知 Pacemaker 群集资源可以 （或不能） 运行的位置。
-   排序约束告知 Pacemaker 群集应启动资源所在的顺序。

> [!NOTE]
> 由于所有这些都被视为单个单元，归置约束不需要的资源组中的资源。

#### <a name="quorum-fence-agents-and-stonith"></a>仲裁、 围墙代理和 STONITH
某种程度上类似于在概念的 WSFC 仲裁 Pacemaker 下。 群集的仲裁机制的整个目的是确保群集保持启动并正在运行。 WSFC 和的 Linux 分发版的 HA 外接程序具有的概念的投票，其中每个节点都将计入仲裁。 您要将大多数投票，否则，在最差的情况下，群集将关闭。

与不同的 WSFC 中，用于仲裁没有见证资源。 如 WSFC，目的是使选民奇数数目。 仲裁配置有不同的比 Fci 承载个可用性组的注意事项。

WSFCs 监视参与节点的状态，并出现问题时处理它们。 更高版本的 WSFCs 提供诸如功能隔离错误或不可用的节点 （节点不在、 网络通信已关闭，等等）。 在 Linux 端中，由围墙代理提供这种类型的功能。 这一概念有时称为隔离。 但是，这些围墙代理通常特定于部署，并且通常由硬件供应商和一些软件供应商，例如那些提供虚拟机监控程序提供。 例如，VMware 提供可用于使用 vSphere 虚拟化的 Linux Vm 的围墙代理。

仲裁和到另一个概念防御等同值调用 STONITH，或投篮机会控制在头在其他节点。 STONITH 需要具有支持的 Pacemaker 群集上的所有 Linux 分发。 有关详细信息，请参阅[防御在 Red Hat 高可用性群集](https://access.redhat.com/solutions/15575)(RHEL)。

#### <a name="corosyncconf"></a>corosync.conf
`corosync.conf`文件包含的群集配置。 它位于`/etc/corosync`。 在过程中日常操作中，此文件应永远不需要如果群集已正确设置了编辑。

#### <a name="cluster-log-location"></a>群集日志位置
Pacemaker 群集的日志位置因分发而异。
-   RHEL 和 SLES-`/var/log/cluster/corosync.log`
-   Ubuntu –`/var/log/corosync/corosync.log`

若要更改默认日志记录位置，请修改`corosync.conf`。

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>计划 Pacemaker 群集[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
本部分讨论 Pacemaker 群集的重要规划点。

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>群集管理基于 Linux 的虚拟化 Pacemaker[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
使用虚拟机部署基于 Linux 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]承载个可用性组和 Fci 的部署涵盖的与基于 Windows 的对应相同的规则。 没有一组基本的规则可支持性的虚拟化[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]部署由 Microsoft 在[Microsoft 支持 KB 956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment)。 Microsoft 的 HYPER-V 和 VMware 的 ESXi 等的不同虚拟机监控程序可能存在差异导致的平台本身除此之外，具有不同的方差。

当它涉及到承载个可用性组和 Fci 下虚拟化时，请确保给定 Pacemaker 群集的节点设置反相关性。 托管的虚拟机以实现高可用性在可用性组或 FCI 配置中，配置时[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应永远不会在同一虚拟机监控程序主机上运行。 例如，如果部署两个节点 FCI，存在需要*至少*因此的某处出现主机故障，请转到宿主节点 Vm 之一尤其是当使用功能的三个虚拟机监控程序主机如 Live迁移或 vMotion。

有关详细信息，请参阅：
-   Hyper V 文档 –[使用来宾群集以实现高可用性](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   白皮书 （面向那些使用基于 Windows 的部署，但大部分仍概念应用） –[规划高度可用的任务关键 SQL 服务器部署，与 VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL 与 Pacemaker 群集与 STONITH 尚不支持 hyper-v 中。 直到，都支持，有关详细信息和更新，请查阅[RHEL 高可用性群集的支持策略](https://access.redhat.com/articles/29440#3physical_host_mixing)。

### <a name="networking"></a>网络
与 WSFC 不同 Pacemaker 不需要专用的名称或至少一个专用的 IP 地址为 Pacemaker 群集本身。 承载个可用性组和 Fci 将需要 IP 地址 （请参阅有关详细信息的每个文档），但不是包括名称，因为没有任何网络名称资源。 SLES 允许管理目的的 IP 地址配置，但它不是必需的如下所示在[创建 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md#create)。

WSFC，如 Pacemaker 希望使用冗余的网络，这意味着不同的网卡 （Nic 或实现的物理 pNICs） 具有单个 IP 地址。 根据群集配置中，每个 IP 地址都称为自己环。 但是，与 WSFCs 今天，很多实现虚拟化或公共云其中实际上只有一个虚拟化向服务器提供的 NIC (vNIC)。 如果所有 pNICs 和 vNICs 都连接到同一个物理或虚拟交换机，则没有真正的冗余在网络层上，因此配置多个 Nic 是一种具有错觉到虚拟机的位。 网络冗余通常内置到虚拟机监控程序的虚拟化部署，并且明确内置于公有云。

具有多个 Nic 和 Pacemaker 与 WSFC 的一个区别是 Pacemaker 在同一子网，允许多个 IP 地址而 WSFC 却没有。 多个子网和 Linux 群集的详细信息，请参阅文章[配置多个子网](sql-server-linux-configure-multiple-subnet.md)。

### <a name="quorum-and-stonith"></a>仲裁和 STONITH
仲裁配置和要求相关的可用性组或特定于 FCI 的部署到[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

有关支持的 Pacemaker 群集需要 STONITH。 使用从分发的文档来配置 STONITH。 一个示例是在[基于存储的隔离](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html)sles。 此外，还有用于基于 ESXI 的解决方案的 VMware vCenter STONITH 代理。 有关详细信息，请参阅[Stonith 适用于 VMWare VM VCenter SOAP 防御 (Unofficial) 插件代理](https://github.com/olafrv/fence_vmware_soap)。

> [!NOTE]
> 截止本文撰写时，HYPER-V 有一种解决方案的 STONITH。 这适用于在本地部署，并还会影响使用如 RHEL 某些分发的基于 Azure 的 Pacemaker 部署。

### <a name="interoperability"></a>互操作性
本节介绍与 WSFC 或 Linux 的其他分发版与基于 Linux 的群集的交互方式。

#### <a name="wsfc"></a>WSFC
目前，为协同工作的 WSFC 和 Pacemaker 群集没有直接的方法。 这意味着没有方法来创建可用性组或 FCI 的可以跨 WSFC 和 Pacemaker 工作。 但是，有两个互操作性解决方案，这两种旨在用于承载个可用性组。 FCI 可以参与跨平台配置的唯一方法是如果它在这两个方案的一个实例作为参与：
-   群集类型为一个可用性组。 有关详细信息，请参阅 Windows[可用性组文档](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)。
-   分布式可用性组，这是一种特殊类型的允许两个不同承载个可用性组配置为自己的可用性组的可用性组。 分布式承载个可用性组的详细信息，请参阅文档[分布式可用性组](../database-engine/availability-groups/windows/distributed-availability-groups.md)。

#### <a name="other-linux-distributions"></a>其他 Linux 分发
在 Linux 上，Pacemaker 群集的所有节点都必须位于相同的分布。 例如，这意味着 RHEL 节点不能为具有的 SLES 节点 Pacemaker 群集的一部分。 上面提到这的主要原因： 分发可能具有不同的版本和功能，因此操作可能无法正常工作。 混合使用分发具有混合 WSFCs 和 Linux 的文字部分： 使用无或分布式承载个可用性组。

## <a name="next-steps"></a>后续步骤
[在 Linux 上的 SQL Server 的部署 Pacemaker 群集](sql-server-linux-deploy-pacemaker-cluster.md)
