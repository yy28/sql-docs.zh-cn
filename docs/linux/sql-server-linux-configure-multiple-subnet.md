---
title: 配置多子网可用性组和 FCI (Linux)
description: 了解如何为 Linux 上的 SQL Server 配置多子网 Always On 可用性组和故障转移群集实例 (FCI)。
ms.custom: seo-lt-2019
author: liweiSecurity
ms.author: liweiyin
ms.reviewer: VanMSFT
ms.date: 07/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5abe1d99f753e0f41ca74a0864079293800dc1df
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362962"
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
    <instance attributes id="<NameForAttribute>">
        <nvpair id="<NameForIP>" name="ip" value="<IPAddress>"/>
    </instance attributes>
    ```
    
    其中，NameForAttribute 是此属性的唯一名称，NameForIP 是与 IP 地址关联的名称，IPAddress 是第二个子网的 IP 地址  。
    
    下面显示了一个示例。
    
    ```xml
    <instance attributes id="virtualip-instance_attributes">
        <nvpair id="virtualip-instance_attributes-ip" name="ip" value="192.168.1.102"/>
    </instance attributes>
    ```
    
    默认情况下，导出的 CIB XML 文件中只有一个 <instance/>。 假设有两个子网，你只需有两个 <instance/> 条目即可。
    下例展示了两个子网的条目
    
    ```xml
    <instance attributes id="virtualip-instance_attributes1">
        <rule id="Subnet1-IP" score="INFINITY" boolean-op="or">
            <expression id="Subnet1-Node1" attribute="#uname" operation="eq" value="Node1" />
            <expression id="Subnet1-Node2" attribute="#uname" operation="eq" value="Node2" />
        </rule>
        <nvpair id="IP-In-Subnet1" name="ip" value="192.168.1.102"/>
    </instance attributes>
    <instance attributes id="virtualip-instance_attributes2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node1" attribute="#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet2" name="ip" value="192.168.2.102"/>
    </instance attributes>
    ```
   
   如果子网具有多个服务器，将使用 'boolean-op="or"'。


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

下面的 CSS 帖子显示了如何为三个子网配置 CIB，请查看详细信息：[通过修改 CIB 配置多子网 AlwaysOn 可用性组](https://techcommunity.microsoft.com/t5/sql-server-support/configure-multiple-subnet-alwayson-availability-groups-by/ba-p/1544838)。
