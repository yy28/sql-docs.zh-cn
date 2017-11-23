---
title: "配置 SQL Server 可用性组的 Ubuntu 群集 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.workload: Inactive
ms.openlocfilehash: cc6eee565499d696c4f634d6eedc562547bc8253
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>配置 Ubuntu 群集和可用性组资源

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文档说明如何在 Ubuntu 上创建一个三节点群集并将以前创建的可用性组添加为群集中的资源。 在 Linux 上的可用性组以实现高可用性，需要三个节点-请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。

> [!NOTE] 
> 此时，在 Linux 上 SQL Server 与 Pacemaker 的集成不及与在 Windows 上与 WSFC 集成的耦合性高。 在 SQL 内部，无法了解到群集是否存在，所有业务流程都是由外至内，并且 Pacemaker.将该服务作为一个独立实例控制。 此外，虚拟网络名称特定于 WSFC，Pacemaker 中无相同的等效项。 AlwaysOn 动态管理视图查询群集信息，返回空行。 你仍可创建一个侦听器，以将其用于故障转移后，透明重新连接，但你将需要使用手动注册侦听器名称在 DNS 服务器中用于创建虚拟 IP 资源 （如下所述） 的 IP。

以下各部分介绍了设置故障转移群集解决方案的步骤。 

## <a name="roadmap"></a>路线图

在 Linux 服务器上创建可用性组以获得高可用性的步骤不同于 Windows Server 故障转移群集上的步骤。 下面的列表对高级别步骤进行了说明： 

1. [群集节点上配置 SQL Server](sql-server-linux-setup.md)。

2. [创建可用性组](sql-server-linux-availability-group-configure-ha.md)。 

3. 配置 Pacemaker 之类的群集资源管理器。 本文档中包含这些说明。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 本文档中的演示不使用隔离代理。 演示仅用于测试和验证目的。 
   
   >Linux 群集使用隔离将群集返回到已知状态。 配置隔离的方式取决于分发和环境。 此时，隔离在某些云环境中不可用。 请参阅[RHEL 高可用性群集的虚拟化平台的支持策略](https://access.redhat.com/articles/29440)有关详细信息。

5.  [为群集中的资源添加到可用性组](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)。 

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
>启用 Pacemaker 命令完成，出现错误“Pacemaker 默认启动不包含运行级别，正在中止”。 这无关紧要，群集配置可继续进行。 我们正在联系群集供应商修复该问题。

## <a name="create-the-cluster"></a>创建群集

1. 从所有节点中删除任何现有的群集配置。 

   运行“sudo apt-get install pcs”将同时安装 pacemaker、corosync 和 pcs，并开始运行这 3 个服务。  启动 corosync 将生成“/etc/cluster/corosync.conf”模板文件。  能够成功此文件的后续步骤应不存在 – 因此解决方法是停止 pacemaker / corosync 和删除 ' / etc/cluster/corosync.conf，然后接下来的步骤将成功完成。 电脑群集销毁执行同样的操作，并可以将其用作一个时间初始群集安装步骤。
   
   以下命令将删除所有现存群集配置文件并停止所有群集服务。 这会永久性销毁群集。 请在预生产环境中将其作为第一个步骤运行。 请注意，“pcs cluster destroy”已禁用 Pacemaker 服务，需重新启用。 在所有节点上运行以下命令。
   
   >[!WARNING]
   >该命令会销毁任何现有群集资源。

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 创建群集。 

   >[!WARNING]
   >由于出现一个已知问题（群集服务供应商正在对其进行调查），启动群集（“pcs cluster start”）将失败，并出现以下错误。 这是因为 /etc/corosync/corosync.conf 中配置的日志文件出现错误。 若要解决此问题，请将日志文件更改为 /var/log/corosync/corosync.log。 或者可创建 /var/log/cluster/corosync.log 文件。
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
以下命令将创建一个三节点群集。 在运行该脚本之前，替换 `**< ... >**` 之内的值。 在主节点上运行以下命令。 

   ```bash
   sudo pcs cluster auth **<node1>** **<node2>** **<node3>** -u hacluster -p **<password for hacluster>**
   sudo pcs cluster setup --name **<clusterName>** **<node1>** **<node2…>** **<node3>**
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >如果以前已在相同节点上配置了群集，则需要在运行“pcs cluster setup”时使用“--force”选项。 请注意，这相当于运行“pcs cluster destroy”，需要使用“sudo systemctl enable pacemaker”重新启用 pacemaker 服务。


## <a name="configure-fencing-stonith"></a>配置隔离 (STONITH)

Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 群集资源管理器无法确定节点或节点上资源的状态时，将使用隔离使群集再次处于已知状态。 资源级别隔离主要确保在因配置资源引起服务中断时，不会发生数据损坏。 例如，可将资源级别隔离用于 DRBD（分布式复制块设备），从而在通信链接出现故障时将节点上的磁盘标记为过时。 节点级别隔离确保节点不会运行任何资源。 重置节点可实现此目的，其 Pacemaker 实现被称为 STONITH (shoot the other node in the head)，即关闭其他节点。 Pacemaker 支持多种隔离设备，例如不间断电源或服务器的管理接口卡。 有关更多详细信息，请参阅[从头 Pacemaker 群集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)和[隔离和 Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

因为防御配置的节点级别很大程度取决于你的环境，我们将本教程中 （它可以配置在更高版本时） 来禁用它。 在主节点上运行以下脚本： 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>禁用 STONITH 仅出于测试目的。 如果计划在生产环境中使用 Pacemaker，则应根据环境计划 STONITH 实现，并使其处于启用状态。 请注意，目前不对任何云环境（包括 Azure）或 Hyper-V 提供隔离代理。 因此，群集供应商未提供在这些环境中运行生产群集相关的支持。 我们正在研究解决方案弥补该漏洞，并在将来版本中推出。

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Set cluster property start-failure-is-fatal to false

`start-failure-is-fatal`指示是否无法在节点上启动资源将阻止进一步开始尝试在该节点上。 当设置为`false`，群集将决定是否要尝试恢复使用基于资源的当前故障计数和迁移阈值的同一节点上启动。 因此，故障转移发生后，在 SQL 实例可用时，Pacemaker 将重新尝试在先前主节点上启动可用性组资源。 Pacemaker 将降级为辅助副本和它将自动重新加入可用性组。 

若要更新属性值设置为`false`运行以下脚本：

```bash
sudo pcs property set start-failure-is-fatal=false
```


>[!WARNING]
>自动故障转移后，当`start-failure-is-fatal = true`资源管理器将尝试启动资源。 如果在第一次尝试失败则必须手动运行`pcs resource cleanup <resourceName>`清理资源失败计数和重置配置。

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>安装 SQL Server 资源代理以与 Pacemaker 集成

在所有节点上运行以下命令。 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>为 Pacemaker 创建 SQL Server 登录名

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>创建可用性组资源

若要创建可用性组资源，使用`pcs resource create`命令和设置资源属性。 以下命令创建`ocf:mssql:ag`主/从具有名称的可用性组的类型资源`ag1`。 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>创建虚拟 IP 资源

若要创建虚拟 IP 地址资源，请在一个节点上运行以下命令。 使用网络中的可用静态 IP 地址。 在运行该脚本之前，将之间的值`**< ... >**`带有有效的 IP 地址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

Pacemaker 中不存在等效的虚拟服务器名称。 若要使用指向字符串服务器名称的连接字符串而不使用 IP 地址，请在 DNS 中注册 IP 资源地址和所需的虚拟服务器名称。 对于 DR 配置，请在主站点和 DR 站点上通过 DNS 服务器注册所需的虚拟服务器名称和 IP 地址。

## <a name="add-colocation-constraint"></a>添加主机托管约束

Pacemaker 群集中几乎所有的决定（例如，选择资源运行的位置）都靠比较分数来制定。 分数按资源计算，群集资源管理器选择特定资源分数最高的节点。 （如果节点的某一资源分数为负，则该资源无法在此节点上运行。）我们可以使用约束来控制群集的决定。 约束具有一个分数。 如果约束的分数低于 INFINITY，则仅为建议项。 分数为 INFINITY 则表明它是必需项。 我们需要确保可用性组主要副本和虚拟 IP 资源在同一主机上运行，因此我们定义一个分数为 INFINITY 的主机托管约束。 若要添加主机托管约束，请在一个节点上运行以下命令。 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>添加排序约束

主机托管约束具有隐式排序约束。 在移动可用性组资源前，它将移动虚拟 IP 资源。 默认事件序列为：

1. 用户问题`pcs resource move`到可用性组主从节点 1 到节点 2。
1. 在节点 1 上停止的虚拟 IP 资源。
1. Node2 上启动的虚拟 IP 资源。

   >[!NOTE]
   >此时的 IP 地址暂时指向 node2 node2 仍是以前故障转移时辅助。 
   
1. 主节点 1 上的可用性组降级为辅助。
1. 辅助节点 2 上的可用性组将提升为主要。 

若要防止 IP 地址暂时指向具有故障转移前的次要副本的节点，请添加排序约束。 

若要添加排序约束，请在一个节点上运行以下命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>配置群集并将可用性组添加为群集资源后，无法使用 Transact-SQL 对可用性组资源进行故障转移。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 RHEL 或 Ubuntu 使用`pcs`。 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>后续步骤

[运行 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)

