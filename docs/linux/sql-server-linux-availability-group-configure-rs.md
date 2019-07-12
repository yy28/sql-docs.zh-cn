---
title: Linux 上配置读取缩放 SQL Server 可用性组
titleSuffix: SQL Server
description: 了解如何在 Linux 上配置 SQL Server 始终在可用性组 (AG) 的读取缩放工作负荷。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 01/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4cbb11da91864716838a7fbb4be26ac2dc00614c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834287"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>Linux 上配置读取缩放 SQL Server 可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

你可以在 Linux 上配置 SQL Server 始终在可用性组 (AG) 的读取缩放工作负荷。 存在两种类型的 AG 体系结构。 为实现高可用性体系结构使用群集管理器来改善的业务连续性。 此体系结构还可以包括读取缩放副本。 若要创建高可用性体系结构，请参阅[配置 SQL Server Always On 可用性组以实现高可用性 Linux 上](sql-server-linux-availability-group-configure-ha.md)。 其他体系结构只支持读取缩放工作负载。 本文介绍如何在不使用群集管理器的情况下创建 AG，用于读取缩放工作负载。 此体系结构仅提供读取缩放。 它不提供高可用性。

> [!NOTE]
> 设置有 `CLUSTER_TYPE = NONE` 的可用性组可包括不同操作系统平台上托管的副本。 它无法支持高可用性。 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>创建 AG

创建 AG。 设置 `CLUSTER_TYPE = NONE`。 此外，使用 `FAILOVER_MODE = MANUAL` 设置每个副本。 运行分析或报告工作负载的客户端应用程序可直接连接到辅助数据库。 还可以创建一个只读路由列表。 与主要副本的连接将读取连接请求循环转发到路由列表中的每个次要副本。

以下 Transact-SQL 脚本创建名为 `ag1` 的 AG。 脚本使用 `SEEDING_MODE = AUTOMATIC` 配置 AG 副本。 此设置会导致 SQL Server 在数据库添加到 AG 后自动在每个辅助服务器上创建数据库。 为环境更新以下脚本。 将 `<node1>` 和 `<node2>` 值替换为托管副本的 SQL Server 实例的名称。 使用为终结点设置的端口替换 `<5022>` 值。 在主 SQL Server 副本上运行以下 Transact-SQL 脚本：

```SQL
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

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

此 AG 不是高可用性配置。 如果需要高可用性，请按照的说明[Linux 上的 SQL Server 配置 Alwayson 可用性组](sql-server-linux-availability-group-configure-ha.md)。 具体而言，创建具有 AG `CLUSTER_TYPE=WSFC` （在 Windows) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux 中)。 通过使用 Windows 或 Linux 上的 Pacemaker 群集是 Windows Server 故障转移，然后与群集管理器。

## <a name="connect-to-read-only-secondary-replicas"></a>连接到只读次要副本

连接只读次要副本有两种方法。 应用程序可直接连接到托管次要副本的 SQL Server 实例并查询数据库。 它们还可以使用只读路由，这需要一个侦听器。

* [可读次要副本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [只读路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>故障转移读取缩放可用性组上的主要副本

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>后续步骤

* [配置分布式可用性组](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)
* [了解有关可用性组的详细信息](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
* [执行强制的手动故障转移](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
