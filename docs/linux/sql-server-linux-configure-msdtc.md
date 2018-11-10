---
title: 如何在 Linux 上配置 MSDTC |Microsoft Docs
description: 本文提供用于在 Linux 上配置 MSDTC 的演练。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a06dfa03442cfbcff2f8815f9c946afbd9ff771c
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269670"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSTDC)。 在 SQL Server 2019 预览版中引入了在 Linux 上的 MSDTC 支持。

## <a name="overview"></a>概述

通过引入 MSDTC 和 RPC 终结点映射器功能在 SQL Server Linux 上的 SQL Server 上启用了分布式的事务。 默认情况下，RPC 终结点映射过程在传入 RPC 请求的端口 135 上侦听，并将的路由到适当组件 （如 MSDTC 服务）。 过程需要超级用户特权，若要在 Linux 上，将绑定到的已知端口 （端口号小于 1024年）。 若要避免使用 root 权限的 RPC 终结点映射器进程启动 SQL Server，系统管理员必须使用 iptables 创建 NAT 转换以将流量路由到 SQL Server 的 RPC 终结点映射进程的端口 135 上。

SQL Server 2019 引入了 mssql-conf 实用工具的两个配置参数。

| mssql-conf 设置 | Description |
|---|---|
| **network.rpcport** | RPC 终结点映射器进程将绑定到 TCP 端口。 |
| **network.servertcpport** | MSDTC 服务器侦听的端口。 如果未设置，MSDTC 服务在服务重新启动时，将使用随机临时端口和防火墙例外将需要重新配置，以确保 MSDTC 服务能够持续通信。 |

有关这些设置和其他相关的 MSDTC 设置的详细信息，请参阅[在 Linux 上使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#msdtc)。

## <a name="supported-msdtc-configurations"></a>支持的 MSDTC 配置

支持以下的 MSDTC 配置：

- OLE TX 为分布式事务针对 Linux 上的 SQL Server JDBC 和 ODBC 提供程序。
- 使用 JDBC 提供程序在 Linux 上的 SQL Server XA 分布式事务。
- 链接服务器上的分布式的事务。

有关限制和 msdtc 预览版中的已知的问题，请参阅[发行说明以在 Linux 上的 SQL Server 2019 预览](sql-server-linux-release-notes-2019.md#msdtc)。

## <a name="msdtc-configuration-steps"></a>MSDTC 配置步骤

有三个步骤来配置 MSDTC 通信和功能。 如果未创建必需的配置步骤，SQL Server 不会启用 MSDTC 功能。

- 配置**network.rpcport**并**distributedtransaction.servertcpport**使用 mssql-conf
- 将防火墙配置为允许上进行通信**rpcport**， **servertcpport**，和端口 135。
- 配置 Linux 服务器的路由，以便在端口 135 上的 RPC 通信重定向到 SQL Server **network.rpcport**。

以下部分提供有关每个步骤的详细的说明。

## <a name="configure-rpc-and-msdtc-ports"></a>配置 RPC 和 MSDTC 端口

首先，配置**network.rpcport**并**distributedtransaction.servertcpport**使用 mssql-conf

1. 使用 mssql-conf 设置**network.rpcport**值。 下面的示例将其设置为 13500。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. 设置**distributedtransaction.servertcpport**值。 下面的示例将其设置为 51999。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. 请重新启动 SQL Server。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>配置防火墙

最后一步是将防火墙配置为允许上进行通信**rpcport**， **servertcpport**，和端口 135。  这样，RPC 终结点映射过程和 MSDTC 过程与其他事务管理器和协调器外部通信。 具体取决于你的 Linux 分发版和防火墙，这实际步骤将有所不同。 

下面的示例演示如何在 Ubuntu 上创建这些规则。

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下面的示例演示如何完成 Red Hat Enterprise Linux (RHEL) 上：

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

请务必在配置端口路由下一节中之前配置防火墙。 刷新防火墙可以清除端口路由规则在某些情况下。

## <a name="configure-port-routing"></a>配置端口路由

配置 Linux 服务器路由表，以便在端口 135 上的 RPC 通信重定向到 SQL Server **network.rpcport**。 Iptable 规则可能不会保留在重新启动时，因此，以下命令还提供用于在重新启动后还原规则的说明。

1. 创建端口 135 的路由规则。 在以下示例中，端口 135 定向到在上一节中定义的 RPC 端口 13500。 替换为`<ipaddress>`与你的服务器的 IP 地址。

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   `--comment RpcEndPointMapper`上述命令中的参数可以帮助管理这些规则在稍后的命令。

2. 查看使用以下命令创建的路由规则：

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 将路由规则保存到你的计算机上的文件。

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. 若要在重启后重新加载规则，将添加到以下命令`/etc/rc.local`（适用于 Ubuntu 或 RHEL） 或`/etc/init.d/after.local`（适用于 SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

**Iptables 保存**并**iptables 还原**命令提供了基本的机制来保存和还原 iptables 条目。 根据 Linux 分发版，那里可能更高级的或自动完成选项可用。 例如，Ubuntu 备用方法是**iptables 持久**包让项保持不变。 对于 Red Hat Enterprise Linux，你可能能够使用 firewalld 服务或者 (通过使用 – 防火墙 cmd 配置实用程序添加-转发的端口或类似的选项) 创建持久的端口转发规则而不是使用 iptables。

> [!IMPORTANT]
> 前面的步骤假定的固定的 IP 地址。 如果您的 SQL Server 实例的 IP 地址发生更改 （由于手动干预或 DHCP），则必须删除并重新创建路由规则。 如果需要重新创建或删除现有的路由规则，可以使用以下命令以删除旧`RpcEndPointMapper`规则：
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

## <a name="verify"></a>Verify

在此情况下，SQL Server 应能够参与分布式事务。 若要验证 SQL Server 正在侦听，请运行**netstat**命令 (如果使用 RHEL 时，可能需要首先安装**net 工具**包):

```bash
sudo netstat -tulpn | grep sqlservr
```

应看到类似于以下输出：

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

但是，重启后，SQL Server 不会启动侦听**servertcpport**直到第一个分布式事务。 在这种情况下，您不会看到 SQL Server 侦听端口 51999 在此示例中，直到第一个分布式事务。

## <a name="next-steps"></a>后续步骤

Linux 上 SQL Server 的详细信息，请参阅[Linux 上的 SQL Server](sql-server-linux-overview.md)。
