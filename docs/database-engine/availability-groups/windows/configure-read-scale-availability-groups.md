---
title: 在 Windows 上配置 SQL Server 可用性组用于读取缩放 | Microsoft Docs
description: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: conceptual
ms.prod: sql
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.openlocfilehash: de62bd96371e93e9491b9c781da3b41f7086dc75
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34768343"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-windows"></a>在 Windows 上配置 SQL Server 可用性组用于读取缩放

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

可在 Windows 上配置 SQL Server AlwaysOn 可用性组 (AG) 用于读取缩放工作负载。 存在两种类型的 AG 体系结构。 高可用性体系结构使用群集管理器提供改善的业务连续性，并且可包含可读次要副本。 若要创建此高可用性体系结构，请参阅[在 Windows 上创建和配置可用性组](creation-and-configuration-of-availability-groups-sql-server.md)。 其他体系结构只支持读取缩放工作负载。 本文介绍如何在不使用群集管理器的情况下创建 AG，用于读取缩放工作负载。 此体系结构仅提供读取缩放。 它不提供高可用性。

>[!NOTE]
>设置有 `CLUSTER_TYPE = NONE` 的可用性组可包括不同操作系统平台上托管的副本。 它无法支持高可用性。 有关 Linux 操作系统，请参阅[在 Linux 上配置 SQL Server 可用性组用于读取缩放](../../../linux/sql-server-linux-availability-group-configure-rs.md)

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-the-ag"></a>创建 AG

创建 AG。 设置 `CLUSTER_TYPE = NONE`。 此外，使用 `FAILOVER_MODE = NONE` 设置每个副本。 运行分析或报告工作负载的客户端应用程序可直接连接到辅助数据库。 还可以创建一个只读路由列表。 与主要副本的连接将读取连接请求循环转发到路由列表中的每个次要副本。

以下 Transact-SQL 脚本创建名为 `ag1` 的 AG。 脚本使用 `SEEDING_MODE = AUTOMATIC` 配置 AG 副本。 此设置会导致 SQL Server 在数据库添加到 AG 后自动在每个辅助服务器上创建数据库。 为环境更新以下脚本。 将 `<node1>` 和 `<node2>` 值替换为托管副本的 SQL Server 实例的名称。 使用为终结点设置的端口替换 `<5022>` 值。 在主 SQL Server 副本上运行以下 Transact-SQL 脚本：

```sql
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH (
            ENDPOINT_URL = N'tcp://<node2>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-ag"></a>将辅助 SQL Server 加入 AG

以下 Transact-SQL 脚本将服务器加入名为 `ag1` 的 AG。 为环境更新脚本。 在每个辅助 SQL Server 副本上运行以下 Transact-SQL 脚本，从而加入 AG：

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

此 AG 不是高可用性配置。 如果需要高可用性，请遵循[为 Linux 上的 SQL Server 配置 Alwayson 可用性组](../../../linux/sql-server-linux-availability-group-configure-ha.md)或[在 Windows 上创建和配置可用性组](creation-and-configuration-of-availability-groups-sql-server.md)中的说明。

## <a name="connect-to-read-only-secondary-replicas"></a>连接到只读次要副本

连接只读次要副本有两种方法。 应用程序可直接连接到托管次要副本的 SQL Server 实例并查询数据库。 它们还可以使用只读路由，这需要一个侦听器。

* [可读次要副本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [只读路由](listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>故障转移读取缩放可用性组上的主要副本

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>后续步骤

* [配置分布式可用性组](distributed-availability-groups-always-on-availability-groups.md)
* [了解有关可用性组的详细信息](overview-of-always-on-availability-groups-sql-server.md)
* [执行强制的手动故障转移](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
