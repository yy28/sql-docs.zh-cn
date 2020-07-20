---
title: 配置多子网可用性组和 FCI (Linux)
description: 了解如何为 Linux 上的 SQL Server 配置多子网 Always On 可用性组和故障转移群集实例 (FCI)。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 3a18e668d1a62a74396530e37243d75a5a86aee2
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196962"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>配置多子网 Always On 可用性组和故障转移群集实例

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

如果 Always On 可用性组 (AG) 或故障转移群集实例 (FCI) 跨越多个站点，则通常每个站点都有其自己的网络。 这通常意味着每个站点都有其自己的 IP 地址。 例如，站点 A 的地址以 192.168.1 x 开头，站点 B 的地址以 192.168.2 x 开头，其中 x 是服务器独有的 IP 地址部分  。 如果网络层中不存在某种类型的路由，则这些服务器将无法相互通信。 处理该情况有两种方法：设置桥接两个不同子网的网络（称为 VLAN），或配置子网之间的路由。

## <a name="vlan-based-solution"></a>基于 VLAN 的解决方案
 
先决条件：对于基于 VLAN 的解决方案，每个参与 AG 或 FCI 的服务器都需要两个网卡 (NIC) 才能实现良好的可用性（双重端口 NIC 是物理服务器上的单一故障点），以便可以在其本机子网和 VLAN 中分配 IP 地址。 这是对其他网络需求的补充，如 iSCSI 需要自己的网络。

在 VLAN 上为 AG 或 FCI 创建 IP 地址。 在以下示例中，VLAN 具有 192.168.3 x 的子网，因此为 AG 或 FCI 创建的 IP 地址为 192.168.3.104。 因为 AG 或 FCI 分配有一个 IP 地址，所以无需配置其他内容。

![配置多个子网 01](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>具有 Pacemaker 的配置

在 Windows 环境中，Windows Server 故障转移群集 (WSFC) 本机支持多个子网，并通过 IP 地址上的 OR 依赖项来处理多个 IP 地址。 Linux 上没有 OR 依赖项，但有一种方法可以使用 Pacemaker 本机实现适当的多子网，如下所示。 若仅仅使用普通的 Pacemaker 命令行来修改资源，则无法做到这一点。 需要修改群集信息库 (CIB)。 CIB 是具有 Pacemaker 配置的 XML 文件。

![配置多个子网 02](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>更新 CIB

1. 导出 CIB。

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    其中文件名是要调用 CIB 的名称。

2. 编辑生成的文件。 查找 `<resources>` 部分。 你会看到为 AG 或 FCI 创建的各种资源。 查找与 IP 地址相关联的资源。 添加 `<instance attributes>` 部分，其中包含第二个 IP 地址的信息，该 IP 地址位于现有 IP 地址的上方或下方，但在 `<operations>` 前。 与以下语法类似：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    其中，NameForAttribute 是该属性的唯一名称，Score 是分配给该属性的数字（这一数字必须大于分配给主子网的数字），RuleName 是规则的名称，ExpressionName 是表达式的名称，NodeNameInSubnet2 是另一子网中节点的名称，NameForSecondIP 是与第二个 IP 地址相关联的名称，IPAddress 是第二个子网的 IP 地址，NameForSecondIPNetmask 是与网络掩码关联的名称，Netmask 是第二个子网的网络掩码        。
    
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

3. 导入修改后的 CIB，重新配置 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    其中 filename 是包含已修改的 IP 地址信息的 CIB 文件的名称。

### <a name="check-and-verify-failover"></a>检查并验证故障转移

1. CIB 成功应用更新的配置后，请在 Pacemaker 中对与 IP 地址资源关联的 DNS 名称执行 Ping 命令。 结果应反映与当前承载 AG 或 FCI 的子网关联的 IP 地址。
2. 阻止 AG 或 FCI 转移到另一个子网。
3. AG 或 FCI 完全联机后，对与 IP 地址关联的 DNS 名称执行 Ping 命令。 结果应反映第二个子网中的 IP 地址。
4. 如果需要，请阻止 AG 或 FCI 回到原始子网。
