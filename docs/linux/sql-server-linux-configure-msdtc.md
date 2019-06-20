---
title: 如何在 Linux 上配置 MSDTC |Microsoft Docs
description: 本文提供用于在 Linux 上配置 MSDTC 的演练。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 2bcf87b91423ae7aa79ae6a5194aa8fc31ca71c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713262"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSTDC)。 在 SQL Server 2019 预览版中引入了在 Linux 上的 MSDTC 支持。

## <a name="overview"></a>概述

通过引入 MSDTC 和 RPC 终结点映射器功能在 SQL Server Linux 上的 SQL Server 上启用了分布式的事务。 默认情况下，RPC 终结点映射过程在传入 RPC 请求的端口 135 上侦听，并提供到远程请求的已注册的组件信息。 远程请求可以使用返回的终结点映射程序的信息与已注册的 RPC 组件，如 MSDTC 服务进行通信。 一个过程需要超级用户权限才能在 Linux 上，将绑定到的已知端口 （端口号小于 1024年）。 若要避免使用 root 权限的 RPC 终结点映射器进程启动 SQL Server，系统管理员必须使用 iptables 创建网络地址转换将流量路由到 SQL Server 的 RPC 终结点映射进程的端口 135 上。

SQL Server 2019 引入了 mssql-conf 实用工具的两个配置参数。

| mssql-conf 设置 | Description |
|---|---|
| **network.rpcport** | RPC 终结点映射器进程将绑定到 TCP 端口。 |
| **distributedtransaction.servertcpport** | MSDTC 服务器侦听的端口。 如果未设置，MSDTC 服务在服务重新启动时，将使用随机临时端口和防火墙例外将需要重新配置以确保 MSDTC 服务能够持续通信。 |

有关这些设置和其他相关的 MSDTC 设置的详细信息，请参阅[在 Linux 上使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#msdtc)。

## <a name="supported-msdtc-configurations"></a>支持的 MSDTC 配置

支持以下的 MSDTC 配置：

- OLE TX 为分布式事务针对 Linux 上的 SQL Server 的 ODBC 访问接口。
- 使用 JDBC 和 ODBC 提供程序在 Linux 上的 SQL Server XA 分布式事务。 若要使用 ODBC 提供程序执行 XA 事务，需要使用 Microsoft ODBC Driver for SQL Server 版本 17.3 或更高版本。
- 链接服务器上的分布式的事务。

有关限制和 msdtc 预览版中的已知的问题，请参阅[发行说明以在 Linux 上的 SQL Server 2019 预览](sql-server-linux-release-notes-2019.md#msdtc)。

## <a name="msdtc-configuration-steps"></a>MSDTC 配置步骤

有三个步骤来配置 MSDTC 通信和功能。 如果未创建必需的配置步骤，SQL Server 不会启用 MSDTC 功能。

- 配置**network.rpcport**并**distributedtransaction.servertcpport**使用 mssql-conf
- 将防火墙配置为允许上进行通信**distributedtransaction.servertcpport**和端口 135。
- 配置 Linux 服务器的路由，以便在端口 135 上的 RPC 通信重定向到 SQL Server **network.rpcport**。

以下部分提供有关每个步骤的详细的说明。

## <a name="configure-rpc-and-msdtc-ports"></a>配置 RPC 和 MSDTC 端口

首先，配置**network.rpcport**并**distributedtransaction.servertcpport**使用 mssql-conf 如果特定于 SQL Server，并且在所有受支持分发版上通用此步骤。

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

第二步是将防火墙配置为允许上进行通信**servertcpport**和端口 135。  这样，RPC 终结点映射过程和 MSDTC 过程与其他事务管理器和协调器外部通信。 具体取决于你的 Linux 分发版和防火墙，这实际步骤将有所不同。 

下面的示例演示如何在创建这些规则**Ubuntu**。

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下面的示例演示如何在完成**Red Hat Enterprise Linux (RHEL)** :

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

请务必在配置端口路由下一节中之前配置防火墙。 刷新防火墙可以清除端口路由规则在某些情况下。

## <a name="configure-port-routing"></a>配置端口路由

配置 Linux 服务器路由表，以便在端口 135 上的 RPC 通信重定向到 SQL Server **network.rpcport**。 在不同的分发上转发的端口的配置机制可能会有所不同。 以下部分提供有关 Ubuntu、 SUS Enterprise Linux (SLES) 和 Red Hat Enterprise Linux (RHEL) 的指导。

### <a name="port-routing-in-ubuntu-and-sles"></a>在 Ubuntu 和 SLES 端口路由

不使用 Ubuntu 和 SLES **firewalld**服务，这样**iptable**规则是高效机制来实现端口路由。 **Iptable**规则可能不会持续期间重启，因此，以下命令还提供用于在重新启动后还原规则的说明。

1. 创建端口 135 的路由规则。 在以下示例中，端口 135 定向到在上一节中定义的 RPC 端口 13500。 替换为`<ipaddress>`与你的服务器的 IP 地址。

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   `--comment RpcEndPointMapper`上述命令中的参数可以帮助管理这些规则在稍后的命令。

2. 查看使用以下命令创建的路由规则：

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 将路由规则保存到你的计算机上的文件。

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. 若要在重启后重新加载规则，将添加到以下命令`/etc/rc.local`（适用于 Ubuntu) 或`/etc/init.d/after.local`（适用于 SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > 必须具有超级用户 (sudo) 权限来编辑**為 rc.local**或**after.local**文件。

**Iptables 保存**并**iptables 还原**命令，以及与`rc.local` / `after.local`启动配置，提供了基本的机制来保存和还原 iptables条目。 根据 Linux 分发版，那里可能更高级的或自动完成选项可用。 例如，Ubuntu 备用方法是**iptables 持久**包让项保持不变。

> [!IMPORTANT]
> 前面的步骤假定的固定的 IP 地址。 如果您的 SQL Server 实例的 IP 地址发生更改 （由于手动干预或 DHCP），必须删除并重新创建路由规则，如果它们使用 iptables 创建。 如果需要重新创建或删除现有的路由规则，可以使用以下命令以删除旧`RpcEndPointMapper`规则：
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>RHEL 中的路由的端口

使用的分发上**firewalld**服务，如 Red Hat Enterprise Linux，同一个服务可以用于这两个打开的端口上的服务器和内部端口转发。 例如，在 Red Hat Enterprise Linux，你应使用**firewalld**服务 (通过**防火墙 cmd**配置实用程序用于`-add-forward-port`或类似的选项) 来创建和管理永久性端口而不是使用 iptables 转发规则。

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

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

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>上的 MSDTC RPC 通信配置身份验证

Linux 上的 SQL Server 的 MSDTC 不使用身份验证对 RPC 通信默认情况下中。 但是，当主机计算机加入到 Active Directory (AD) 域后，就可以配置 MSDTC 以使用已经过身份验证的 RPC 通信使用以下**mssql conf**设置：

| 设置 | Description |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | 配置安全的分布式事务的唯一 RPC 调用。 |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | 配置的安全性仅 RPC 调用的分布式事务。 |
| **distributedtransaction.turnoffrpcsecurity**               | 启用或禁用 RPC 安全性为分布式事务。 |

## <a name="next-steps"></a>后续步骤

Linux 上 SQL Server 的详细信息，请参阅[Linux 上的 SQL Server](sql-server-linux-overview.md)。
