---
title: 对 SQL Server 可用性组配置 RHEL 群集
titleSuffix: SQL Server
description: 了解可用性组群集时运行 Red Hat Enterprise Linux (RHEL)
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: c498a9ef5422f82671000d6c0e82756df85947cb
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160592"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>对 SQL Server 可用性组配置 RHEL 群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文档介绍如何为 Red Hat Enterprise Linux 上的 SQL Server 中创建三个节点的可用性组群集。 Linux 上的可用性组以实现高可用性，需要三个节点-请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 群集层基于 Red Hat Enterprise Linux (RHEL) 上[HA 加载项](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)基础上构建[Pacemaker](https://clusterlabs.org/)。 

> [!NOTE] 
> 访问 Red Hat 完整文档需要有效订阅。 

有关群集配置、 资源代理选项和管理的详细信息，请访问[RHEL 参考文档](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。

> [!NOTE] 
> SQL Server 未紧密集成与 Linux 上的 Pacemaker 这一点与 Windows Server 故障转移群集。 SQL Server 实例不识别群集。 Pacemaker 提供了群集资源的业务流程。 此外，虚拟网络名称特定于 Windows Server 故障转移群集-Pacemaker 中没有等效项。 Pacemaker 群集上，查询群集信息的可用性组动态管理视图 (Dmv) 返回空行。 若要创建故障转移后的透明重新连接的侦听器，手动在使用用于创建虚拟 IP 资源的 IP 的 DNS 中注册的侦听器名称。 

以下部分介绍为实现高可用性而设置 Pacemaker 群集以及将可用性组添加为群集中的资源的步骤。

## <a name="roadmap"></a>路线图

在 Linux 服务器上创建可用性组以获得高可用性的步骤不同于 Windows Server 故障转移群集上的步骤。 以下列表介绍的高级步骤： 

1. [群集节点上配置 SQL Server](sql-server-linux-setup.md)。

2. [创建可用性组](sql-server-linux-availability-group-configure-ha.md)。 

3. 配置 Pacemaker 之类的群集资源管理器。 本文档中包含这些说明。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 本文档中的演示不使用隔离代理。 演示仅用于测试和验证目的。 
   
   >Linux 群集使用隔离将群集返回到已知状态。 配置隔离的方式取决于分发和环境。 目前，隔离不是在某些云环境中可用的。 有关详细信息，请参阅[RHEL 高可用性群集的虚拟化平台的支持策略](https://access.redhat.com/articles/29440)。

5. [将可用性组添加为群集中的资源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>适用于 RHEL 配置高可用性

若要配置适用于 RHEL 高可用性，启用高可用性的订阅，然后配置 Pacemaker。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>启用适用于 RHEL 高可用性的订阅

在群集中每个节点必须具有相应的订阅针对 RHEL 和高可用性添加。 查看在要求[如何在 Red Hat Enterprise Linux 中安装高可用性群集包](https://access.redhat.com/solutions/45930)。 请执行以下步骤来配置的订阅和存储库：

1. 注册系统。

   ```bash
   sudo subscription-manager register
   ```

   提供用户名和密码。   

1. 列出用于注册的可用池。

   ```bash
   sudo subscription-manager list --available
   ```

   从可用池的列表，请注意高可用性订阅的池 ID。

1. 更新以下脚本。 替换为`<pool id>`的上一步中高度可用的池 id。 运行脚本以附加订阅。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 启用存储库。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

有关详细信息，请参阅[Pacemaker-打开源服务器，高可用性群集](https://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/)。 

配置了订阅后，完成配置 Pacemaker 的以下步骤：

### <a name="configure-pacemaker"></a>配置 Pacemaker

注册订阅后，完成配置 Pacemaker 的以下步骤：
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Pacemaker 配置后，使用`pcs`来与群集交互。 在群集中的一个节点上执行的所有命令。 

## <a name="configure-fencing-stonith"></a>配置隔离 (STONITH)

Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 STONITH shoot 另一个节点标头中。" 当群集资源管理器无法确定节点或节点上资源的状态时，隔离将群集放置到已知状态重新。

资源级别隔离可确保通过配置资源，没有发生中断时无数据损坏。 例如，使用资源级别隔离，若要将磁盘标记为过时时的节点上的通信链接出现故障。 

节点级别隔离确保节点不会运行任何资源。 这是重置节点。 Pacemaker 支持多种隔离设备。 例如，服务器不间断电源供应或管理接口卡。

有关 STONITH 和隔离的信息，请参阅以下文章：

* [从零开始的 pacemaker 群集](https://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [隔离和 STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Red Hat Pacemaker 高可用性加载项：隔离](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

由于节点级别隔离配置很大程度取决于你的环境，则在本教程中 （它可以配置更高版本） 的情况下禁用它。 以下脚本可以禁用节点级别隔离：

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>禁用 STONITH 仅出于测试目的。 如果计划在生产环境中使用 Pacemaker，则应根据环境计划 STONITH 实现，并使其处于启用状态。 RHEL 不对任何云环境 （包括 Azure） 或 HYPER-V 隔离代理。 因此，群集供应商未提供在这些环境中运行生产群集相关的支持。 我们正在研究解决方案弥补该漏洞，并在将来版本中推出。

## <a name="set-cluster-property-cluster-recheck-interval"></a>设置群集属性群集重新检查间隔

`cluster-recheck-interval` 指示检查群集资源参数、 约束或其他群集选项中的更改的轮询间隔。 如果副本出现故障，群集将尝试重新启动的时间间隔，由绑定的副本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`设置为 60 秒和`cluster-recheck-interval`设置为 120 秒，在重新启动尝试的时间间隔大于 60 秒，但不超过 120 秒。 我们建议将故障超时设置为 60 秒和群集重新检查的间隔超过 60 秒的值。 不建议将群集重新检查间隔设置为较小的值。

若要将属性值更新为`2 minutes`运行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> （包括 RHEL 7.3 和 7.4） 的所有使用最新可用 Pacemaker 包 1.1.18-11.el7 分布引入开始失败-是的致命群集设置的行为更改其值为 false。 此更改会影响故障转移工作流。 如果主副本发生服务中断，群集应故障转移到其中一个可用的辅助副本。 相反，用户会注意到该群集会一直尝试启动失败的主副本。 如果该主永远不会处于联机状态 （由于的永久中断），群集永远不会故障转移到另一个可用的辅助副本。 由于此更改，以前推荐的配置来设置开始失败-是的致命将不再有效，需要恢复回其默认值设置`true`。 此外，需要更新，以包含 AG 资源`failover-timeout`属性。 

若要将属性值更新为`true`运行：

```bash
sudo pcs property set start-failure-is-fatal=true
```

若要更新`ag1`资源属性`failure-timeout`到`60s`运行：

```bash
pcs resource update ag1 meta failure-timeout=60s
```


有关 Pacemaker 群集属性的信息，请参阅[Pacemaker 群集属性](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)。

## <a name="create-a-sql-server-login-for-pacemaker"></a>为 Pacemaker 创建 SQL Server 登录名

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>创建可用性组资源

若要创建可用性组资源，请使用`pcs resource create`命令并设置资源属性。 以下命令将创建`ocf:mssql:ag`master/slave 类型的具有名称的可用性组的资源`ag1`。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>创建虚拟 IP 资源

若要创建虚拟 IP 地址资源，请在一个节点上运行以下命令。 使用网络中的可用静态 IP 地址。 将 IP 地址之间为`<10.128.16.240>`具有有效的 IP 地址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker 中不存在等效的虚拟服务器名称。 若要使用指向字符串服务器名称而不是 IP 地址的连接字符串，请在 DNS 中注册的虚拟 IP 资源地址和所需的虚拟服务器名称。 对于 DR 配置，请在主站点和 DR 站点上通过 DNS 服务器注册所需的虚拟服务器名称和 IP 地址。

## <a name="add-colocation-constraint"></a>添加主机托管约束

Pacemaker 群集中几乎所有的决定（例如，选择资源运行的位置）都靠比较分数来制定。 计算分数的每个资源。 群集资源管理器将选择具有特定资源的最高分数的节点。 如果某个节点具有负的分值的资源，资源无法在该节点上运行。

在 pacemaker 群集上，您可以操作具有约束的群集的决策。 约束具有一个分数。 如果约束的分数低于`INFINITY`，Pacemaker 将它看作建议。 分数为`INFINITY`是必需的。

若要确保主副本和虚拟 ip 资源在同一主机上运行，请定义一个分数为 INFINITY 的主机托管约束。 若要添加主机托管约束，请在一个节点上运行以下命令。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>添加排序约束

主机托管约束具有隐式排序约束。 在移动可用性组资源前，它将移动虚拟 IP 资源。 默认事件序列为：

1. 用户问题`pcs resource move`到可用性组主副本从节点 1 到节点 2。
1. 节点 1 上虚拟 IP 资源停止。
1. 节点 2 上虚拟 IP 资源启动。
  
   >[!NOTE]
   >此时，IP 地址暂时指向节点 2，同时节点 2 仍为故障转移前的次要副本。 
   
1. 节点 1 上的可用性组主要副本降级为次要副本。
1. 节点 2 上的可用性组次要副本升级为主要副本。 

若要防止 IP 地址暂时指向具有故障转移前的次要副本的节点，请添加排序约束。 

若要添加排序约束，请在一个节点上运行以下命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>配置群集并将可用性组添加为群集资源后，无法使用 Transact-SQL 对可用性组资源进行故障转移。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 RHEL 或 Ubuntu 中使用`pcs`并且在 SLES 使用`crm`工具。 

使用可用性组手动故障转移`pcs`。 请勿使用 Transact-SQL 启动故障转移。 有关说明，请参阅[故障转移](sql-server-linux-availability-group-failover-ha.md#failover)。

## <a name="next-steps"></a>后续步骤

[操作 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)
