---
title: "在 Linux 上配置多子网 Alwayson 可用性组和故障转移群集实例 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 84195d2451664b2bee81ebbb1dc3b7d9d89060d5
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>配置多子网 Alwayson 可用性组和故障转移群集实例

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

当始终在可用性组 (AG) 或故障转移群集实例 (FCI) 跨多个站点，每个站点通常都有其自己网络。 这通常意味着每个站点有其自己的 IP 寻址。 例如，站点 A 的地址使用 192.168.1 启动。*x*和站点 B 地址开头 192.168.2。*x*，其中*x*是唯一的服务器的 IP 地址的一部分。 而无需某种形式的路由已到位在网络层，这些服务器将不能相互之间进行通信。 有两种方法来处理这种情况下： 设置的网络的桥接两个不同子网，名为 VLAN，或配置子网之间路由。

## <a name="vlan-based-solution"></a>基于 VLAN 的解决方案
 
**先决条件**： 基于为 VLAN 的解决方案，每台服务器参与可用性组或 FCI 需要两个网卡 (Nic) 为正确的可用性 （单一物理服务器上的故障点是双端口 NIC），以便它能够上分配 IP 地址其本机的子网，以及一个与 VLAN 上。 这是除了任何其他网络需要，如 iSCSI，还需要其自己的网络。

可用性组或 FCI 的 IP 地址创建可与 VLAN 上。 在以下示例中，VLAN 都有 192.168.3 的子网。*x*，因此创建可用性组或 FCI 的 IP 地址是 192.168.3.104。 任何其他需要配置，因为没有单个 IP 地址分配给可用性组或 FCI。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>配置 Pacemaker

在 Windows 世界中，Windows Server 故障转移群集 (WSFC) 以本机方式支持多个子网，并处理通过 IP 地址上的或依赖关系的多个 IP 地址。 在 Linux 上，不存在或依赖，但没有本机实现正确的多子网与 Pacemaker，一种方法按以下所示。 不能只需使用正常的 Pacemaker 命令行修改资源来执行此操作。 你需要修改群集信息基础 （兴业）。 兴业是 Pacemaker 配置 XML 文件。

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>更新兴业

1.  导出兴业。

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    其中*filename*是你想要调用兴业的名称。

2.  编辑生成的文件。 查找`<resources>`部分。 你将看到已创建的可用性组或 FCI 的各种资源。 找到一个与 IP 地址相关联。 添加`<instance attributes>`之前部分的上方或下方的现有版本，第二个 IP 地址的信息`<operations>`。 它是类似于以下语法：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    其中*NameForAttribute*是此特性的唯一名称*分数*是对属性必须高于主子网的分配的编号*RuleName*是规则的名称，*表达式名称*是表达式的名称*NodeNameInSubnet2*是其他子网中的节点的名称*NameForSecondIP*是第二个 IP 地址，与关联的名称*IPAddress*是第二个子网的 IP 地址*NameForSecondIPNetmask*是子网掩码，与关联的名称和*子网掩码*是第二个子网的网络掩码。
    
    下面显示一个示例。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  导入已修改的兴业和重新配置 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    其中*filename*是包含已修改的 IP 地址信息的兴业文件的名称。

### <a name="check-and-verify-failover"></a>检查并验证故障转移

1.  兴业成功应用了更新的配置后，ping 与 Pacemaker 中的 IP 地址资源关联的 DNS 名称。 它应反映与当前正在承载可用性组或 FCI 的子网关联的 IP 地址。
2.  到其他子网中失败的可用性组或 FCI。
3.  可用性组或 FCI 处于完全联机状态后，执行 ping 操作相关联的 IP 地址的 DNS 名称。 它应反映中第二个子网的 IP 地址。
4.  如果需要，故障回复到原始的子网的可用性组或 FCI。
