---
title: 在 Linux 上配置多子网 Alwayson 可用性组和故障转移群集实例 |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 595add5d077136c4093776fae8e3a2f7ab04bb26
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396170"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>配置多子网 Alwayson 可用性组和故障转移群集实例

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

当 Always On 可用性组 (AG) 或故障转移群集实例 (FCI) 跨多个站点，每个站点通常具有其自己的网络。 这通常意味着，每个站点都有其自己的 IP 地址。 例如，站点 A 的地址以 192.168.1 开头。*x*和站点 B 的地址开头 192.168.2。*x*，其中*x*是仅适用于服务器的 IP 地址的一部分。 而无需某种形式的路由已到位在网络层，这些服务器将不能相互通信。 有两种方法来处理这种情况： 设置网络，用于桥接两个不同子网，名为 VLAN，或配置子网之间路由。

## <a name="vlan-based-solution"></a>基于 VLAN 的解决方案
 
**先决条件**:对于基于 VLAN 的解决方案，参与可用性组或 FCI 的每台服务器需要两个网卡 (Nic) 以正确的可用性 （双端口 NIC 是单一物理服务器上的故障点），，，以便可以将有关其本机的子网，以及一个 IP 地址分配在 VLAN。 其中不包括任何其他网络需要，如 iSCSI，还需要其自身的网络。

AG 或 FCI 的 IP 地址创建 VLAN 上完成。 在以下示例中，VLAN 具有 192.168.3 的子网。*x*，因此创建 AG 或 FCI 的 IP 地址是 192.168.3.104。 任何其他需要配置，因为没有分配到 AG 或 FCI 的单个 IP 地址。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>配置与 Pacemaker

在 Windows 世界中，Windows Server 故障转移群集 (WSFC) 以本机方式支持多个子网和多个 IP 地址通过 IP 地址上的或依赖关系的处理。 在 Linux 上，没有任何 OR 依赖关系，但没有本机实现正确的多子网与 Pacemaker，一种方法按以下所示。 不能只需使用普通的 Pacemaker 命令行来修改的资源来执行此操作。 您需要修改群集信息基础 （上）。 上为 Pacemaker 配置具有的 XML 文件。

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>更新上

1.  导出。

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    其中*文件名*是你想要调用上的名称。

2.  编辑已生成的文件。 查找`<resources>`部分。 你将看到为 AG 或 FCI 创建的各种资源。 查找与 IP 地址相关联。 添加`<instance attributes>`节替换高于或低于现有，第二个 IP 地址的信息之前`<operations>`。 它是类似于以下语法：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    其中*NameForAttribute*是此属性的唯一名称*分数*是分配给该属性，必须高于主要子网，数字*RuleName*是规则的名称*表达式名称*是该表达式的名称*NodeNameInSubnet2*的其他子网中的节点名称*NameForSecondIP*是第二个 IP 地址，与关联的名称*IPAddress*是第二个子网的 IP 地址*NameForSecondIPNetmask*是子网掩码，与关联的名称和*子网掩码*是第二个子网的网络掩码。
    
    下面显示了一个示例。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  导入已修改的上并重新配置 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    其中*文件名*是使用修改后的 IP 地址信息的上文件的名称。

### <a name="check-and-verify-failover"></a>检查并验证故障转移

1.  使用更新的配置已成功应用上之后，ping 与 Pacemaker 中的 IP 地址资源关联的 DNS 名称。 它应反映与当前正在承载可用性组或 FCI 的子网关联的 IP 地址。
2.  故障到另一个子网的 AG 或 FCI。
3.  AG 或 FCI 完全处于联机状态后，执行 ping 操作相关联的 IP 地址的 DNS 名称。 它应反映中第二个子网的 IP 地址。
4.  如果需要，故障回复到原始子网可用性组或 FCI。
