---
title: "用于 SQL Server 可用性组配置 RHEL 群集 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.workload: Inactive
ms.openlocfilehash: 860d3571aa1edf7c467125de1cc2920a968eb704
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>对 SQL Server 可用性组配置 RHEL 群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文档说明如何为 Red Hat Enterprise Linux 上的 SQL Server 创建三节点可用性组群集。 在 Linux 上的可用性组以实现高可用性，需要三个节点-请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 聚类分析层基于 Red Hat Enterprise Linux (RHEL) 上[HA 外接程序](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)基础上构建[Pacemaker](http://clusterlabs.org/)。 

> [!NOTE] 
> 访问 Red Hat 完整文档需要有效订阅。 

群集配置、 资源代理选项和管理的详细信息，请访问[RHEL 参考文档](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。

> [!NOTE] 
> SQL Server 不为与紧密集成在 Linux 上的 Pacemaker 这一点与 Windows Server 故障转移群集。 SQL Server 实例不是群集的感知的。 Pacemaker 提供群集资源业务流程。 此外，虚拟网络名称是特定于 Windows Server 故障转移群集-Pacemaker 中没有等效项。 查询群集信息的可用性组动态管理视图 (Dmv) 在 Pacemaker 群集上返回空行。 若要创建故障转移后的透明重新连接的侦听器，手动在与用于创建虚拟 IP 资源的 IP 的 DNS 中注册的侦听器名称。 

以下部分介绍为实现高可用性而设置 Pacemaker 群集以及将可用性组添加为群集中的资源的步骤。

## <a name="roadmap"></a>路线图

在 Linux 服务器上创建可用性组以获得高可用性的步骤不同于 Windows Server 故障转移群集上的步骤。 以下列表描述的高级步骤： 

1. [群集节点上配置 SQL Server](sql-server-linux-setup.md)。

2. [创建可用性组](sql-server-linux-availability-group-configure-ha.md)。 

3. 配置 Pacemaker 之类的群集资源管理器。 本文档中包含这些说明。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 本文档中的演示不使用隔离代理。 演示仅用于测试和验证目的。 
   
   >Linux 群集使用隔离将群集返回到已知状态。 配置隔离的方式取决于分发和环境。 目前，隔离不是在某些云环境中可用的。 有关详细信息，请参阅[RHEL 高可用性群集的虚拟化平台的支持策略](https://access.redhat.com/articles/29440)。

5. [为群集中的资源添加到可用性组](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>Rhel 配置高可用性

若要配置 RHEL 高可用性，启用高可用性订阅，然后配置 Pacemaker。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>启用 RHEL 的高可用性订阅

群集中每个节点必须具有相应的订阅 RHEL 和高可用性添加。 查看在要求[如何在 Red Hat Enterprise Linux 中安装高可用性群集包](http://access.redhat.com/solutions/45930)。 请按照下列步骤配置订阅和存储库：

1. 注册系统。

   ```bash
   sudo subscription-manager register
   ```

   提供你的用户名和密码。   

1. 列出有关注册的可用池。

   ```bash
   sudo subscription-manager list --available
   ```

   从可用池的列表，请注意高可用性订阅池 ID。

1. 更新以下脚本。 替换`<pool id>`与前面步骤中的高可用性的池 ID。 运行脚本以附加订阅。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 启用存储库。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

有关详细信息，请参阅[Pacemaker – 开放源代码，高可用性群集](http://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/)。 

配置了订阅后，完成以下步骤以配置 Pacemaker:

### <a name="configure-pacemaker"></a>配置 Pacemaker

注册的订阅后，完成以下步骤以配置 Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

配置 Pacemaker 后，使用`pcs`与群集进行交互。 在从群集的一个节点上执行所有命令。 

## <a name="configure-fencing-stonith"></a>配置隔离 (STONITH)

Pacemaker 群集供应商需要启用 STONITH，并对支持的群集安装程序配置隔离设备。 STONITH 代表"投篮机会控制在另一个节点在头中。" 当群集资源管理器无法确定的一个节点或节点上的资源的状态时，隔离再次使群集到已知的状态。

资源级别隔离确保通过配置资源有发生中断时没有数据损坏。 例如，你可以使用资源级别隔离将磁盘标记为过时时的节点上的通信链接出现故障。 

节点级别隔离确保节点不会运行任何资源。 这可通过重置节点。 Pacemaker 支持大量防御设备。 示例包括服务器不间断电源提供或管理接口卡。

有关 STONITH 和隔离的信息，请参阅以下文章：

* [从零开始的 pacemaker 群集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [隔离和 STONITH](http://clusterlabs.org/doc/crm_fencing.html)
* [Red Hat 高可用性外的接程序与 Pacemaker： 防御](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

因为防御配置的节点级别很大程度取决于你的环境，则在本教程中 （它可以配置更高版本） 的情况下禁用它。 以下脚本可以禁用节点级别隔离：

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>禁用 STONITH 仅出于测试目的。 如果计划在生产环境中使用 Pacemaker，则应根据环境计划 STONITH 实现，并使其处于启用状态。 RHEL 不提供针对任何云环境 （包括 Azure） 或 HYPER-V 隔离代理。 因此，群集供应商未提供在这些环境中运行生产群集相关的支持。 我们正在研究解决方案弥补该漏洞，并在将来版本中推出。

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Set cluster property start-failure-is-fatal to false

`start-failure-is-fatal`指示是否无法在节点上启动资源将阻止进一步开始尝试在该节点上。 当设置为`false`，群集来决定是否要尝试恢复使用基于资源的当前故障计数和迁移阈值的同一节点上启动。 发生故障转移后，Pacemaker 重试启动可用性组主前者上资源的 SQL 实例可用后。 Pacemaker 将降级到辅助数据库副本，并自动重新加入可用性组。 

若要更新属性值设置为`false`运行：

```bash
sudo pcs property set start-failure-is-fatal=false
```

>[!WARNING]
>自动故障转移后，当`start-failure-is-fatal = true`资源管理器将尝试启动资源。 如果它在第一次尝试上失败，手动运行`pcs resource cleanup <resourceName>`来清理资源失败计数，重置配置。

Pacemaker 群集属性的信息，请参阅[Pacemaker 群集属性](http://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)。

## <a name="create-a-sql-server-login-for-pacemaker"></a>为 Pacemaker 创建 SQL Server 登录名

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>创建可用性组资源

若要创建可用性组资源，使用`pcs resource create`命令和设置资源属性。 以下命令将创建`ocf:mssql:ag`主/从具有名称的可用性组的类型资源`ag1`。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 master notify=true
```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>创建虚拟 IP 资源

若要创建虚拟 IP 地址资源，请在一个节点上运行以下命令。 使用网络中的可用静态 IP 地址。 之间的 IP 地址替换`<10.128.16.240>`带有有效的 IP 地址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker 中不存在等效的虚拟服务器名称。 若要使用指向字符串服务器的名称而不是 IP 地址的连接字符串，请在 DNS 中注册的虚拟 IP 资源地址和所需的虚拟服务器名称。 对于 DR 配置，请在主站点和 DR 站点上通过 DNS 服务器注册所需的虚拟服务器名称和 IP 地址。

## <a name="add-colocation-constraint"></a>添加主机托管约束

Pacemaker 群集中几乎所有的决定（例如，选择资源运行的位置）都靠比较分数来制定。 计算分数的每个资源。 群集资源管理器选择特定资源的最高分数的节点。 如果节点的负分数的资源，资源不能在该节点上运行。

在 pacemaker 群集上，可以操作具有约束的群集的决策。 约束具有一个分数。 如果一个约束的分数低于`INFINITY`，Pacemaker 将它看作建议。 分数为`INFINITY`是必需的。

若要确保主副本和虚拟 ip 资源的同一主机上运行，分数为无穷大将归置约束的定义。 若要添加主机托管约束，请在一个节点上运行以下命令。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>添加排序约束

主机托管约束具有隐式排序约束。 在移动可用性组资源前，它将移动虚拟 IP 资源。 默认事件序列为：

1. 用户问题`pcs resource move`到可用性组主从节点 1 到节点 2。
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
>配置群集并将可用性组添加为群集资源后，无法使用 Transact-SQL 对可用性组资源进行故障转移。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 RHEL 或 Ubuntu 使用`pcs`并且在 SLES 使用`crm`工具。 

手动故障转移的可用性组`pcs`。 请勿使用 Transact-SQL 启动故障转移。 有关说明，请参阅[故障转移](sql-server-linux-availability-group-failover-ha.md#failover)。

## <a name="next-steps"></a>后续步骤

[运行 HA 可用性组](sql-server-linux-availability-group-failover-ha.md)
