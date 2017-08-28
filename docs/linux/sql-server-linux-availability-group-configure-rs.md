---
title: "在 Linux 上的 SQL Server 配置读取的横向扩展可用性组 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 配置读取的横向扩展可用性组

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

你可以在 Linux 上的 SQL server 配置读取的横向扩展可用性组。 可用性组有两种体系结构。 A*高可用性*体系结构使用群集管理器提供改进的业务连续性。 此体系结构还可以包括读取的横向扩展副本。 若要创建的高可用性体系结构，请参阅[配置 Alwayson 可用性组在 Linux 上的 SQL Server 的](sql-server-linux-availability-group-configure-ha.md)。

本文档介绍如何创建*读取的横向扩展*不带群集管理器的可用性组。 此体系结构只提供读取的横向扩展仅。 它不提供高可用性。

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>创建可用性组

创建可用性组。 Set `CLUSTER_TYPE = NONE`. 此外，设置与每个副本`FAILOVER_MODE = NONE`。 客户端应用程序运行分析或报告工作负荷可以直接连接到辅助数据库。 你还可以创建一个只读路由列表。 连接到主副本转发连接到读取请求，每个辅助副本从轮循机制方式中的路由列表。

以下 TRANSACT-SQL 脚本创建可用性组名称`ag1`。 脚本将与可用性组副本`SEEDING_MODE = AUTOMATIC`。 此设置会导致 SQL Server 在数据库添加到可用性组后自动在每个辅助服务器上创建数据库。 为环境更新以下脚本。 替换`**<node1>**`和`**<node2>**`具有承载副本的 SQL Server 实例的名称的值。 替换`**<5022>**`与终结点设置的端口。 在主 SQL Server 副本上运行以下 TRANSACT-SQL:

```Transact-SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>将辅助 SQL Server 加入可用性组

下面的 TRANSACT-SQL 脚本将服务器加入到可用性组名为`ag1`。 为环境更新脚本。 在每个辅助 SQL Server 副本上运行以下 Transact-SQL，以加入可用性组。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

这不是高可用性配置，如果你需要高可用性，请遵循的说明[配置 Alwayson 可用性组在 Linux 上的 SQL Server 的](sql-server-linux-availability-group-configure-ha.md)。 具体而言，创建可用性组与`CLUSTER_TYPE=WSFC`（在 Windows 中) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux 中) 以及与群集管理器的 Windows 上的 WSFC，或者在 Linux 上的 Pacemaker 集成。

## <a name="connect-to-read-only-secondary-replicas"></a>连接到只读的辅助副本

有两种方法来连接到只读的辅助副本。 应用程序可直接连接到托管次要副本的 SQL Server 实例并查询数据库，也可使用只读路由。 只读路由需要一个侦听器。

[可读辅助副本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[只读路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>故障转移上读取的横向扩展可用性组的主副本

每个可用性组仅有一个主要副本。 主要副本允许读取和写入操作。 若要更改哪些副本是主，可以故障转移。 在可用性组中以实现高可用性，群集管理器在故障转移过程中自动执行。 在读取的横向扩展可用性组中，故障转移过程为手动。 有两种方法进行故障转移中读取的缩放可用性组的主副本。

- 强制手动故障转移设置的数据丢失

- 手动故障转移而不丢失数据

### <a name="forced-fail-over-with-data-loss"></a>强制的故障转移造成数据丢失

当主要副本不可用且无法恢复时，请使用此方法。 你可以找到有关强制故障转移在数据丢失的详细信息[执行强制手动故障转移](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)。

若要强制故障转移造成数据丢失中，连接到承载目标辅助副本的 SQL 实例，并运行：
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>手动故障转移而不丢失数据

使用此方法时主副本可用，但你需要暂时或永久更改的配置和更改的 SQL Server 实例承载主副本。 在颁发之前手动故障转移，请确保目标辅助副本是最新的因此就不可能会丢失数据。 

以下步骤描述如何手动故障转移而不丢失数据：

1. 使目标次要副本同步提交。

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. 更新`required_synchronized_secondaries_to_commit`为 1。

   此设置可以确保每个活动的事务是提交到主副本和至少一个同步的辅助数据库。 可用性组已准备好进行故障转移在同步 synchronization_state_desc 时并且 sequence_number 是相同的两个主站点和目标辅助副本。 运行此查询以检查：

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. 将主要副本降级为次要副本。 降级的主副本后，它是只读的。 在承载主副本以使更新角色到辅助数据库的 SQL 实例上运行此命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. 将目标次要副本升级为主要副本。 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 若要删除可用性组使用[DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)。 对于使用 CLUSTER_TYPE NONE 或外部创建可用性组，该命令无需执行的可用性组的所有副本部分。

## <a name="next-steps"></a>后续步骤

[配置分布式的可用性组](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[了解有关可用性组的详细信息](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)


