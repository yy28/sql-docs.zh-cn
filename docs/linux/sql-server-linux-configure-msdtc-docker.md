---
title: 如何使用分布式的事务和 Docker 上的 SQL Server |Microsoft Docs
description: 本文介绍如何使用 Linux 上配置 MSDTC Dprovides 演练。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3242f0d074dc3c2f33fc83de4604a20bfdcbd64a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049393"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>如何使用分布式的事务和 Docker 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何设置 Docker 上的 SQL Server 为分布式事务。

从 SQL Server 2019 preview 开始，容器映像才支持 Microsoft 分布式事务处理协调器 (MSDTC) 所需的分布式事务。 若要了解 MSDTC 的通信要求，请参阅[如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)](sql-server-linux-configure-msdtc.md)。 本文介绍的特殊要求和与 SQL Server Docker 容器相关的方案。

## <a name="configuration"></a>配置

若要启用 docker 的容器中的 MSDTC 事务，必须设置两个新的环境变量：

- **MSSQL_RPC_PORT**: RPC 终结点映射程序服务将绑定到并侦听的 TCP 端口。  
- **MSSQL_DTC_TCP_PORT**端口 MSDTC 服务配置为在其上侦听。

### <a name="pull-and-run"></a>请求和运行

下面的示例演示如何使用这些环境变量来请求和运行为 MSDTC 配置的容器。 这使得它可以与任何主机上的任何应用程序进行通信。

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=13500' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 13500:13500 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

下面的命令在 PowerShell 中的 Windows 上的 Docker 演示相同的命令：

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=13500" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 13500:13500 -p 51000:51000 `
   -d "mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu"
```

在此命令中， **RPC 端点映射程序**服务已绑定到端口 13500，并**MSDTC**服务已绑定到端口 51000 docker 虚拟网络中。 SQL Server TDS 通信时 docker 虚拟网络中的端口 1433年上使用。 这些端口都已从外部公开到 TDS 端口 51433、 RPC 终结点映射器端口 13500 和 MSDTC 端口 51000 所在的主机。

> [!NOTE]
> RPC 终结点映射器和 MSDTC 端口不需要主机和容器上都相同。 因此虽然 RPC 端点映射程序端口已配置为在容器上 13500，它无法可能映射到端口 13501 或任何其他可用的端口在主机服务器上。

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

如果在 docker 容器参与分布式事务的主机外部的服务器，主机必须配置端口路由。 有关详细信息，请参阅[配置端口路由](sql-server-linux-configure-msdtc.md#configure-port-routing)。

## <a name="next-steps"></a>后续步骤

Linux 上 MSDTC 的详细信息，请参阅[如何在 Linux 上配置 Microsoft 分布式事务处理协调器 (MSDTC)](sql-server-linux-configure-msdtc.md)。