---
title: 用于 SQL Server 可用性组配置 SLES 群集 |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: dc6298c55104aeabcf2da799be4ed1977ea39620
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>为 SQL Server 可用性组配置 SLES 群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南介绍了如何为 SQL Server 上 SUSE Linux 企业服务器 (SLES) 12 SP2 创建一个三节点群集。 在 Linux 上的可用性组以实现高可用性，需要三个节点-请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 聚类分析层基于 SUSE[高可用性扩展 (HAE)](https://www.suse.com/products/highavailability)基础上构建[Pacemaker](http://clusterlabs.org/)。 

群集配置、 资源代理选项、 管理、 最佳实践，和建议的详细信息，请参阅[SUSE Linux Enterprise 高可用性扩展 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

>[!NOTE]
>此时，在 Linux 上 SQL Server 与 Pacemaker 的集成不及与在 Windows 上与 WSFC 集成的耦合性高。 Linux 上的 SQL Server 服务无法识别群集。 Pacemaker 控制所有的群集资源，包括可用性组资源的业务流程。 在 Linux 上，你不应依赖于始终在可用性组动态管理视图 (Dmv) 提供群集信息，如 sys.dm_hadr_cluster。 此外，虚拟网络名称特定于 WSFC，Pacemaker 中无相同的等效项。 你仍可创建一个侦听器，以将其用于故障转移后，透明重新连接，但你将需要使用手动注册侦听器名称在 DNS 服务器中用于创建虚拟 IP 资源 （如以下各节中所述） 的 IP。


## <a name="roadmap"></a>路线图

有关创建可用性组以实现高可用性的过程 Linux 服务器和 Windows Server 故障转移群集之间存在不同。 以下列表描述的高级步骤： 

1. [群集节点上配置 SQL Server](sql-server-linux-setup.md)。

2. [创建可用性组](sql-server-linux-availability-group-failover-ha.md)。 

3. 配置 Pacemaker 之类的群集资源管理器。 本文档中包含这些说明。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 这篇文章中的示例不使用隔离代理。 它们是用于测试和验证仅。 
   
   >Pacemaker 群集使用隔离群集返回到已知的状态。 配置隔离的方式取决于分发和环境。 此时，隔离在某些云环境中不可用。 请参阅[SUSE Linux Enterprise 高可用性扩展](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. [为群集中的资源添加到可用性组](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)。 

## <a name="prerequisites"></a>必要條件

若要完成以下的端到端方案，你需要三台计算机部署三个节点群集。 以下步骤概述了如何配置这些服务器。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>在每个群集节点上安装和配置操作系统 

第一步是在群集节点上配置操作系统。 对于此演练，将 SLES 12 SP2 用于 HA 加载项的有效订阅。

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>在每个群集节点上安装和配置 SQL Server 服务

1. 安装和设置的所有节点上的 SQL Server 服务。 有关详细说明，请参阅[在 Linux 上安装 SQL Server](sql-server-linux-setup.md)。

1. 将一个节点指定为主节点和其他节点作为辅助副本。 在本指南中使用这些术语。

1. 确保要成为群集部分的节点可互相通信。

   下面的示例演示`/etc/hosts`其中添加名为 SLES1、 SLES2 和 SLES3 的三个节点的内容。

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   所有群集节点都必须能够通过 SSH 相互访问。 工具如`hb_report`或`crm_report`（进行故障排除） 并且 Hawk 的历史记录资源管理器需要节点之间不需要密码 SSH 访问权限，否则它们可以仅从收集数据的当前节点。 如果你使用非标准 SSH 端口，使用-X 选项 (请参阅`man`页)。 例如，如果你的 SSH 端口，3479 调用`crm_report`使用：

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   有关详细信息，请参阅[SLES 管理指南-杂项部分](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)。


## <a name="create-a-sql-server-login-for-pacemaker"></a>为 Pacemaker 创建 SQL Server 登录名

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>配置 AlwaysOn 可用性组

在 Linux 服务器上配置可用性组，然后配置群集资源。 若要配置可用性组，请参阅[配置 Alwayson 可用性组在 Linux 上的 SQL server](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每个群集节点上安装和配置 Pacemaker

1. 安装高可用性扩展

   有关参考，请参阅[安装 SUSE Linux Enterprise Server 和高可用性扩展](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. 在这两个节点上安装 SQL Server 资源代理包。

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>设置第一个节点

   请参阅[SLES 安装说明](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. 以登录`root`到物理计算机或你想要用作群集节点的虚拟机。
2. 执行如下命令，启动该启动脚本：
   ```bash
   sudo ha-cluster-init
   ```

   如果 NTP 尚未配置为在启动时启动，则会显示一条消息。 

   如果你决定仍要继续，该脚本将自动生成密钥 SSH 访问权限和 Csync2 同步工具，并启动同时所需的服务。 

3. 配置群集通信层 (Corosync)： 

   a. 输入要绑定到的网络地址。 默认情况下，该脚本将建议 eth0 的网络地址。 或者，输入一个不同的网络地址，例如 bond0 地址。 

   b. 输入一个多播地址。 该脚本推荐一个随机地址，可将其用作默认地址。 

   c. 输入一个多播端口。 该脚本推荐将 5405 用作默认端口。 

   d. 若要配置`SBD ()`，输入你想要用于 SBD 的块设备的分区持久的路径。 该路径在群集中所有节点之间必须一致。 
   最后，该脚本将启动 Pacemaker 服务，从而使此单节点群集处于联机状态并启用 Web 管理接口 Hawk2。 要用于 Hawk2 的 URL 将显示在屏幕上。 

4. 安装过程的任何详细信息，请`/var/log/sleha-bootstrap.log`。 现在便有一个正在运行的单节点群集。 使用 crm status 检查群集状态：

   ```bash
   sudo crm status
   ```

   你还可以看到与群集配置`crm configure show xml`或`crm configure show`。

5. 此启动过程创建一个名为 hacluster 的 Linux 用户，密码为 linux。 请尽快使用安全密码替换此默认密码： 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>将节点添加到现有群集

如果运行的群集包含一个或多个节点，可使用 ha-cluster-join 启动脚本添加更多群集节点。 该脚本仅需现有节点访问权限，然后可自动在当前计算机上完成基本设置。 使用以下步骤：

如果配置了与现有的群集节点`YaST`群集模块，请确保在运行之前满足以下先决条件`ha-cluster-join`:
- 现有节点上根用户的 SSH 密钥已就绪，无需密码即可登录。 
- `Csync2` 现有的节点上进行配置。 有关详细信息，请参阅与 YaST 配置 Csync2。 

1. 以根用户身份登录到要加入群集的物理计算机或虚拟计算机。 
2. 执行如下命令，启动该启动脚本： 

   ```bash
   sudo ha-cluster-join
   ```

   如果 NTP 尚未配置为在启动时启动，则会显示一条消息。 

3. 如果仍要继续，系统将提示输入现有节点的 IP 地址。 输入 IP 地址。 

4. 如果尚未配置这两个计算机之间的无密码 SSH 访问，系统还将提示输入现有节点的根密码。 

   登录后到指定的节点，该脚本将 Corosync 配置复制，配置 SSH 和`Csync2`，并使新的群集节点作为当前联机的计算机。 除了，它将启动所需的 Hawk 服务。 如果已配置共享的存储，与使用`OCFS2`，它还会自动创建的装载点目录`OCFS2`文件系统。 

5. 你想要添加到群集的所有计算机重复前面的步骤。 

6. 过程的详细信息，请检查`/var/log/ha-cluster-bootstrap.log`。 

1. 检查群集状态的`sudo crm status`。 如果已成功添加第二个节点，则输出将如下所示：

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 是一个单节点群集初始安装过程中配置虚拟 IP 群集资源。

添加所有节点后，检查是否需要调整全局群集选项中的 no-quorum-policy。 这对双节点群集尤为重要。 有关详细信息，请参阅部分 4.1.2，选项否仲裁策略。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>设置群集属性群集重新检查间隔

`cluster-recheck-interval` 指示检查群集中的资源参数、 约束或其他群集选项的更改的轮询间隔。 如果副本出现故障，群集将尝试通过绑定的时间间隔重新启动副本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`设置为 60 秒和`cluster-recheck-interval`设置为 120 秒、 重新启动尝试大于 60 秒，但不超过 120 秒的时间间隔。 我们建议将故障超时设置为 60 和群集重新检查的间隔超过 60 秒的值。 不建议将群集重新检查间隔设置为较小的值。

若要更新属性值设置为`2 minutes`运行：

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果你已有由 Pacemaker 群集的可用性组资源，请注意使用最新可用 Pacemaker 包 1.1.18-11.el7 的所有分发都引入开始失败-是-严重群集设置时的行为更改其值为 false。 此更改会影响故障转移工作流。 如果主副本发生了服务中断，群集会出现故障转移到其中一个可用的辅助副本。 相反，用户会发现群集保留尝试启动失败的主副本。 如果该主永远不会处于联机状态 （由于的永久中断），群集永远不会故障转移到另一个可用的辅助副本。 由于此更改，以前推荐的配置设置开始失败-是-严重将不再有效，该设置需要还原为其默认值为`true`。 此外，需要更新，以包含可用性组资源`failover-timeout`属性。 
>
>若要更新属性值设置为`true`运行：
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>更新现有的可用性组资源属性`failure-timeout`到`60s`运行 (替换`ag1`替换为你的可用性组资源的名称): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Pacemaker 群集属性的详细信息，请参阅[配置群集资源](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)。

# <a name="configure-fencing-stonith"></a>配置隔离 (STONITH)
Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 群集资源管理器无法确定节点或节点上资源的状态时，将使用隔离使群集再次处于已知状态。

资源级别隔离主要确保通过配置资源有任何服务中断期间的数据损坏。 例如，可将资源级别隔离用于 DRBD（分布式复制块设备），从而在通信链接出现故障时将节点上的磁盘标记为过时。

节点级别隔离确保节点不会运行任何资源。 重置节点可实现此目的，其 Pacemaker 实现被称为 STONITH (shoot the other node in the head)，即关闭其他节点。 Pacemaker 支持大量防御设备，如服务器不间断电源提供或管理接口卡。

有关详细信息，请参阅[从头 Pacemaker 群集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)，[隔离和 Stonith](http://clusterlabs.org/doc/crm_fencing.html)和[SUSE HA 文档： 隔离和 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)。

在群集初始化时，如果检测不到任何配置，则禁用 STONITH。 它可以通过运行以下命令来更高版本启用：

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>禁用 STONITH 仅出于测试目的。 如果计划在生产环境中使用 Pacemaker，则应根据环境计划 STONITH 实现，并使其处于启用状态。 SUSE 不提供针对任何云环境 （包括 Azure） 或 HYPER-V 隔离代理。 因此，群集供应商未提供在这些环境中运行生产群集相关的支持。 我们正在研究解决方案弥补该漏洞，并在将来版本中推出。


## <a name="configure-the-cluster-resources-for-sql-server"></a>为 SQL Server 配置群集资源

请参阅[SLES 管理 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>创建可用性组资源

以下命令创建并配置三个副本的可用性组 [ag1] 的可用性组资源。 监视操作和超时必须基于这一事实超时高度取决于工作负荷，并需要仔细调整为每个部署在 SLES 中显式指定。
在群集中的一个节点上运行命令：

1. 运行`crm configure`打开 crm 提示：

   ```bash
   sudo crm configure 
   ```

1. 在 crm 提示符下，运行以下命令以配置资源属性。

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>创建虚拟 IP 资源

如果你未在运行时创建的虚拟 IP 资源`ha-cluster-init`可以立即创建此资源。 以下命令将创建一个虚拟 IP 资源。 替换`<**0.0.0.0**>`与你的网络中的可用地址和`<**24**>`具有在 CIDR 子网掩码的位数。 在一个节点上运行。

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>添加主机托管约束
Pacemaker 群集中几乎所有的决定（例如，选择资源运行的位置）都靠比较分数来制定。 分数按资源计算，群集资源管理器选择特定资源分数最高的节点。 （如果节点的某一资源分数为负，则该资源无法在此节点上运行。）我们可以使用约束来控制群集的决定。 约束具有一个分数。 如果约束的分数低于 INFINITY，则仅为建议项。 分数为 INFINITY 则表明它是必需项。 我们想要确保主可用性组和虚拟 ip 资源运行在同一主机上，因此我们定义分数为无穷大归置约束。 

若要将主机托管约束设置为虚拟 IP 在作为主节点的节点上运行，请在一个节点上运行以下命令：

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>添加排序约束
主机托管约束具有隐式排序约束。 在移动可用性组资源前，它将移动虚拟 IP 资源。 默认事件序列为： 

1. 用户发出 resource migrate，将资源从节点 1 的可用性组主要副本移动到节点 2。
2. 节点 1 上虚拟 IP 资源停止。
3. 节点 2 上虚拟 IP 资源启动。 此时，IP 地址暂时指向节点 2，同时节点 2 仍为故障转移前的次要副本。 
4. 节点 1 上的可用性组主要副本降级为从属副本。
5. 节点 2 上的可用性组从属副本升级为主要副本。 

若要防止 IP 地址暂时指向具有故障转移前的次要副本的节点，请添加排序约束。 若要添加排序约束，请在一个节点上运行以下命令： 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>配置群集并将可用性组添加为群集资源后，无法使用 Transact-SQL 对可用性组资源进行故障转移。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 SLES 使用`crm`。 

手动故障转移的可用性组`crm`。 不启动与 TRANSACT-SQL 的故障转移。 有关详细信息，请参阅[故障转移](sql-server-linux-availability-group-failover-ha.md#failover)。


有关详细信息，请参阅：
- [管理群集资源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)。   
- [HA 概念](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker 快速参考](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>后续步骤

[运行 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)
