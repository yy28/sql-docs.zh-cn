---
title: 配置 Ubuntu 群集 SQL Server 可用性组
titleSuffix: SQL Server
description: 了解如何创建可用性组群集的 Ubuntu
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 39753e86cc4d6f82d8bddb0c10356d9be172e90f
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834333"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>配置 Ubuntu 群集和可用性组资源

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文档介绍如何在 Ubuntu 上创建一个三节点群集并将以前创建的可用性组添加为群集中的资源。 Linux 上的可用性组以实现高可用性，需要三个节点-请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。

> [!NOTE] 
> 此时，在 Linux 上 SQL Server 与 Pacemaker 的集成不及与在 Windows 上与 WSFC 集成的耦合性高。 从在 SQL 中，没有任何群集存在相关知识，所有业务流程是外部中，服务由 Pacemaker 控制作为独立的实例。 此外，虚拟网络名称特定于 WSFC，Pacemaker 中无相同的等效项。 Always On 动态管理视图查询群集信息返回为空的行。 你仍可创建一个侦听器，以将其用于故障转移后，透明重新连接，但您必须手动注册侦听器名称的 DNS 服务器中创建虚拟 IP 资源 （如以下各节中所述） 所使用的 IP。

以下各部分介绍了设置故障转移群集解决方案的步骤。 

## <a name="roadmap"></a>路线图

在 Linux 服务器上创建可用性组以获得高可用性的步骤不同于 Windows Server 故障转移群集上的步骤。 以下列表介绍的高级步骤： 

1. [群集节点上配置 SQL Server](sql-server-linux-setup.md)。

2. [创建可用性组](sql-server-linux-availability-group-configure-ha.md)。 

3. 配置 Pacemaker 之类的群集资源管理器。 本文档中包含这些说明。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 本文档中的演示不使用隔离代理。 演示仅用于测试和验证目的。 
   
   >Linux 群集使用隔离将群集返回到已知状态。 配置隔离的方式取决于分发和环境。 此时，隔离在某些云环境中不可用。 请参阅[RHEL 高可用性群集的虚拟化平台的支持策略](https://access.redhat.com/articles/29440)有关详细信息。

5.  [将可用性组添加为群集中的资源](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每个群集节点上安装和配置 Pacemaker

1. 在所有节点上打开防火墙端口。 对 Pacemaker 高可用性服务、SQL Server 实例和可用性组终结点打开此端口。 运行 SQL Server 的服务器默认 TCP 端口是 1433。  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   或者，只需禁用防火墙：
        
   ```bash
   sudo ufw disable
   ```

1. 安装 Pacemaker 包。 在所有节点上，运行以下命令：

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在所有节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>启用并启动 pcsd 服务和 Pacemaker

以下命令启用并启动 pcsd 服务和 Pacemaker。 在所有节点上运行。 这样，节点将可以在重新启动后重新加入群集。 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>启用 pacemaker 命令可能会完成，出现错误 pacemaker 默认启动不包含运行级别，正在中止。 这无关紧要，群集配置可继续进行。 

## <a name="create-the-cluster"></a>创建群集

1. 从所有节点中删除任何现有的群集配置。 

   运行“sudo apt-get install pcs”将同时安装 pacemaker、corosync 和 pcs，并开始运行这 3 个服务。  启动 corosync 将生成“/etc/cluster/corosync.conf”模板文件。  若要成功完成此文件的下一个步骤，不应存在的解决办法是停止 pacemaker / corosync 并删除 / etc/cluster/corosync.conf，然后下一步骤已成功完成。 pcs cluster destroy 执行相同操作，并可以将其用作一个一次性初始群集安装步骤。
   
   以下命令将删除所有现存群集配置文件并停止所有群集服务。 这会永久性销毁群集。 请在预生产环境中将其作为第一个步骤运行。 请注意，“pcs cluster destroy”已禁用 Pacemaker 服务，需重新启用。 在所有节点上运行以下命令。
   
   >[!WARNING]
   >该命令会销毁任何现有的群集资源。

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 创建群集。 

   >[!WARNING]
   >由于的已知问题的调查、 启动群集服务供应商 (pcs cluster start)，群集将故障发生以下错误。 这是因为在其中运行群集安装程序命令时创建，这是错误的 /etc/corosync/corosync.conf 中配置日志文件。 若要解决此问题，请更改到的日志文件： /var/log/corosync/corosync.log。 或者可创建 /var/log/cluster/corosync.log 文件。
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
以下命令创建一个三节点群集。 在运行该脚本之前，替换 `< ... >` 之内的值。 在主节点上运行以下命令。 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >如果以前已在相同节点上配置了群集，则需要在运行“pcs cluster setup”时使用“--force”选项。 请注意，这相当于运行“pcs cluster destroy”，需要使用“sudo systemctl enable pacemaker”重新启用 pacemaker 服务。


## <a name="configure-fencing-stonith"></a>配置隔离 (STONITH)

Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 群集资源管理器无法确定节点或节点上资源的状态时，将使用隔离使群集再次处于已知状态。 资源级别隔离主要确保在因配置资源引起服务中断时，不会发生数据损坏。 例如，可将资源级别隔离用于 DRBD（分布式复制块设备），从而在通信链接出现故障时将节点上的磁盘标记为过时。 节点级别隔离确保节点不会运行任何资源。 重置节点可实现此目的，其 Pacemaker 实现被称为 STONITH (shoot the other node in the head)，即关闭其他节点。 Pacemaker 支持多种隔离设备，例如不间断电源或服务器的管理接口卡。 有关详细信息，请参阅[Pacemaker 从头开始群集](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/)和[隔离和 Stonith](https://clusterlabs.org/doc/crm_fencing.html) 

由于节点级别隔离配置很大程度取决于你的环境，我们禁用它 （它可以配置在更高版本时） 在本教程。 在主节点上运行以下脚本： 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>禁用 STONITH 仅出于测试目的。 如果计划在生产环境中使用 Pacemaker，则应根据环境计划 STONITH 实现，并使其处于启用状态。 请注意，目前不对任何云环境（包括 Azure）或 Hyper-V 提供隔离代理。 因此，群集供应商未提供在这些环境中运行生产群集相关的支持。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>设置群集属性群集重新检查间隔

`cluster-recheck-interval` 指示检查群集资源参数、 约束或其他群集选项中的更改的轮询间隔。 如果副本出现故障，群集将尝试重新启动的时间间隔，由绑定的副本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`设置为 60 秒和`cluster-recheck-interval`设置为 120 秒，在重新启动尝试的时间间隔大于 60 秒，但不超过 120 秒。 我们建议将故障超时设置为 60 秒和群集重新检查的间隔超过 60 秒的值。 不建议将群集重新检查间隔设置为较小的值。

若要将属性值更新为`2 minutes`运行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果已有由 Pacemaker 群集的可用性组资源，请记下的所有分发都使用最新可用 Pacemaker 包 1.1.18-11.el7 都引入开始失败-是的致命群集设置时的行为更改其值为 false。 此更改会影响故障转移工作流。 如果主副本发生服务中断，群集应故障转移到其中一个可用的辅助副本。 相反，用户会注意到该群集会一直尝试启动失败的主副本。 如果该主永远不会处于联机状态 （由于的永久中断），群集永远不会故障转移到另一个可用的辅助副本。 由于此更改，以前推荐的配置来设置开始失败-是的致命将不再有效，需要恢复回其默认值设置`true`。 此外，需要更新，以包含 AG 资源`failover-timeout`属性。 
>
>若要将属性值更新为`true`运行：
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>更新现有的可用性组资源属性`failure-timeout`到`60s`运行 (替换`ag1`可用性组资源的名称):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>安装 SQL Server 资源代理以与 Pacemaker 集成

在所有节点上运行以下命令。 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>为 Pacemaker 创建 SQL Server 登录名

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>创建可用性组资源

若要创建可用性组资源，请使用`pcs resource create`命令并设置资源属性。 以下命令创建`ocf:mssql:ag`master/slave 类型的具有名称的可用性组的资源`ag1`。 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>创建虚拟 IP 资源

若要创建虚拟 IP 地址资源，请在一个节点上运行以下命令。 使用网络中的可用静态 IP 地址。 运行该脚本之前，之间的值替换为`< ... >`具有有效的 IP 地址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker 中不存在等效的虚拟服务器名称。 若要使用指向字符串服务器名称的连接字符串而不使用 IP 地址，请在 DNS 中注册 IP 资源地址和所需的虚拟服务器名称。 对于 DR 配置，请在主站点和 DR 站点上通过 DNS 服务器注册所需的虚拟服务器名称和 IP 地址。

## <a name="add-colocation-constraint"></a>添加主机托管约束

Pacemaker 群集中几乎所有的决定（例如，选择资源运行的位置）都靠比较分数来制定。 分数按资源计算，群集资源管理器选择特定资源分数最高的节点。 （如果节点的某一资源分数为负，则该资源无法在此节点上运行。）使用约束来配置群集的决策。 约束具有一个分数。 如果约束的分数低于 INFINITY，则仅为建议项。 分数为 INFINITY 意味着它是强制的。 若要确保主副本和虚拟 ip 资源位于同一主机上，定义一个分数为 INFINITY 的主机托管约束。 若要添加主机托管约束，请在一个节点上运行以下命令。 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>添加排序约束

主机托管约束具有隐式排序约束。 在移动可用性组资源前，它将移动虚拟 IP 资源。 默认事件序列为：

1. 用户问题`pcs resource move`到可用性组主副本从节点 1 到节点 2。
1. 虚拟 IP 资源停止 node1 上。
1. 节点 2 上启动的虚拟 IP 资源。

   >[!NOTE]
   >此时，IP 地址暂时指向节点 2 同时节点 2 仍为故障转移前的辅助。 
   
1. 可用性组在 node1 上主副本降级为次要副本。
1. 可用性组节点 2 上次要副本升级为主要副本。 

若要防止 IP 地址暂时指向具有故障转移前的次要副本的节点，请添加排序约束。 

若要添加排序约束，请在一个节点上运行以下命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>配置群集并将可用性组添加为群集资源后，无法使用 Transact-SQL 对可用性组资源进行故障转移。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 RHEL 或 Ubuntu 中使用`pcs`。 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>后续步骤

[操作 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)

