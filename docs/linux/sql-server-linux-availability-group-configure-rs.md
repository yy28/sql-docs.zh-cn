---
title: "在 Linux 上配置 SQL Server 可用性组进行读取横向 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 9d8528d227f45e212141e97308718082d6c59cea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>在 Linux 上配置读取缩放 SQL Server 可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

你可以在 Linux 上配置 SQL Server 始终在可用性组 (AG) 读取规模工作负荷。 有两种类型的承载个可用性组的体系结构。 高可用性的体系结构使用群集管理器提供改进的业务连续性。 此体系结构还可以包括读取缩放副本。 若要创建的高可用性体系结构，请参阅[配置 SQL Server Always On 可用性组以在 Linux 上实现高可用性](sql-server-linux-availability-group-configure-ha.md)。 其他体系结构支持仅读取规模工作负荷。 此文章介绍了如何创建可用性组，而无需读取规模工作负荷的群集管理器。 此体系结构提供仅读取缩放。 它不提供高可用性。

>[!NOTE]
>可用性组与`CLUSTER_TYPE = NONE`可以包括不同的操作系统平台上托管的副本。 它无法支持高可用性。 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>创建可用性组

创建可用性组。 Set `CLUSTER_TYPE = NONE`. 此外，设置与每个副本`FAILOVER_MODE = NONE`。 客户端应用程序运行分析或报告工作负荷可以直接连接到辅助数据库。 您还可以创建一个只读路由列表。 连接到主副本转发连接到读取请求，每个辅助副本从一种轮循机制的方式中的路由列表。

下面的 TRANSACT-SQL 脚本将创建名为可用性组`ag1`。 脚本将与可用性组副本`SEEDING_MODE = AUTOMATIC`。 此设置会导致它被添加到可用性组之后，自动在每个辅助服务器上创建数据库的 SQL Server。 为环境更新以下脚本。 替换`<node1>`和`<node2>`具有承载副本的 SQL Server 实例的名称的值。 替换`<5022>`与终结点设置的端口的值。 在主 SQL Server 副本上运行以下 TRANSACT-SQL 脚本：

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

### <a name="join-secondary-sql-servers-to-the-ag"></a>将辅助 SQL 服务器联接到可用性组

下面的 TRANSACT-SQL 脚本将服务器加入到名为可用性组`ag1`。 为环境更新脚本。 在每个辅助 SQL Server 副本上，运行以下的 Transact SQL 脚本，以加入可用性组：

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

此可用性组不是高可用性配置。 如果你需要高可用性，请遵循的说明[为在 Linux 上的 SQL Server 中配置 Alwayson 可用性组](sql-server-linux-availability-group-configure-ha.md)。 具体而言，创建可用性组与`CLUSTER_TYPE=WSFC`（在 Windows 中) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux 中)。 然后与集成群集管理器通过使用在 Windows 或 Linux 上的 Pacemaker 上群集任一 Windows Server 故障转移。

## <a name="connect-to-read-only-secondary-replicas"></a>连接到只读的辅助副本

有两种方法来连接到只读的辅助副本。 应用程序可以直接连接到承载辅助副本的 SQL Server 实例，并查询数据库。 他们还可以使用只读路由，这需要一个侦听器。

* [可读辅助副本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [只读路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>故障转移上读取缩放可用性组的主副本

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>后续步骤

* [配置分布式的可用性组](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [了解有关可用性组的详细信息](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [执行强制的手动故障转移](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

