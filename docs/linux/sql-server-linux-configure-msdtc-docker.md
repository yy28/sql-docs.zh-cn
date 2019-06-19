---
title: 如何使用分布式的事务和 Docker 上的 SQL Server |Microsoft Docs
description: 本文介绍如何使用 Linux 上配置 MSDTC Dprovides 演练。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/25/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 71392b2d5de785df22ec1cf758a12675a0058e45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705581"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>如何使用分布式的事务和 Docker 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何设置 SQL Server Linux 容器在 Docker 上的分布式事务。

从 SQL Server 2019 preview 开始，容器映像才支持 Microsoft 分布式事务处理协调器 (MSDTC) 所需的分布式事务。 若要了解 MSDTC 的通信要求，请参阅[如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)](sql-server-linux-configure-msdtc.md)。 本文介绍的特殊要求和与 SQL Server Docker 容器相关的方案。

## <a name="configuration"></a>配置

若要启用 docker 的容器中的 MSDTC 事务，必须设置两个新的环境变量：

- **MSSQL_RPC_PORT**: RPC 终结点映射程序服务将绑定到并侦听的 TCP 端口。  
- **MSSQL_DTC_TCP_PORT**: 端口 MSDTC 服务配置为在其上侦听。

### <a name="pull-and-run"></a>请求和运行

下面的示例演示如何使用这些环境变量来请求和运行为 MSDTC 配置单个 SQL Server 容器。 这使得它可以与任何主机上的任何应用程序进行通信。

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

> [!IMPORTANT]
> 前一个命令仅适用于 Linux 上运行的 Docker。 适用于 Windows 的 Docker，Windows 主机已在上侦听端口 135。 您可以删除`-p 135:135`Docker 上 Windows，但它的参数有一些限制。 生成的容器可以然后不用于分布式事务涉及的进程内主机。仅在主机上的 docker 容器之间的分布式事务可以参与。

在此命令中， **RPC 端点映射程序**服务已绑定到端口 135，并**MSDTC**服务已绑定到端口 51000 docker 虚拟网络中。 SQL Server TDS 通信时 docker 虚拟网络中的端口 1433年上使用。 这些端口都已从外部公开到 TDS 端口 51433、 RPC 终结点映射器端口 135 和 MSDTC 端口 51000 所在的主机。

> [!NOTE]
> RPC 终结点映射器和 MSDTC 端口不需要在主机和容器上相同。 因此虽然 RPC 端点映射程序端口已配置为在容器上 135，它无法可能映射到端口 13501 或任何其他可用的端口在主机服务器上。

## <a name="configure-the-firewall"></a>配置防火墙

为了与和通过主机通信，还必须在用于容器的主机服务器上配置防火墙。 打开防火墙以允许所有端口 docker 容器公开为外部通信。 在上一示例中，这将是端口 135、 51433 和 51000。 这些是主机本身上的端口和不它们将映射到容器中的端口。 因此，如果 RPC 终结点映射器端口 51000 的容器已映射到主机端口 51001，然后端口应与主机的通信在防火墙中打开 51001 (不 51000)。  

下面的示例演示如何在 Ubuntu 上创建这些规则。

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下面的示例演示如何完成 Red Hat Enterprise Linux (RHEL) 上：

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>配置端口在主机上的路由

在上一示例中，因为单个 Docker 容器将 RPC 端口 135 映射到端口 135 的主机上，分布式的事务的主机应现在适用于无需进一步配置。 请注意，它能直接使用端口 135 的容器中，因为 SQL Server 在使用提升的权限，在容器中运行。 对于 SQL Server 容器外，必须使用一个不同的临时端口，然后必须到该端口路由流量发往端口 135。

但是，如果您未决定将容器的端口 135 给不同的端口在主机上，如 13500 映射，然后必须配置端口在主机上的路由。 这样，要参与分布式事务与主机和与其他外部服务器的 docker 容器。 有关详细信息，请参阅[配置端口路由](sql-server-linux-configure-msdtc.md#configure-port-routing)。

## <a name="next-steps"></a>后续步骤

Linux 上 MSDTC 的详细信息，请参阅[如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)](sql-server-linux-configure-msdtc.md)。
