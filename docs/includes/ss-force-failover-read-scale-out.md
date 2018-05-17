---
title: 用于可用性组的 SQL Server 强制故障转移
description: 对群集类型为 NONE 的可用性组强制进行故障转移
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: f5655e73481d830c848aea34c4a4f49613be0913
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
每个 AG 仅有一个主要副本。 主要副本允许读取和写入操作。 若要更改哪个副本为主要副本，可进行故障转移。 在高可用性的 AG 中，群集管理器自动执行故障转移过程。 在群集类型为 NONE 的可用性组中，需手动执行故障转移过程。 

故障转移群集类型为 NONE 的可用性组中的主要副本有两种方法：

- 强制手动故障转移（会丢失数据）
- 手动故障转移（无数据丢失）

### <a name="forced-manual-failover-with-data-loss"></a>强制手动故障转移（会丢失数据）

当主要副本不可用且无法恢复时，请使用此方法。 

若要强制执行会丢失数据的故障转移，请连接托管目标次要副本的 SQL Server 实例并运行：

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>手动故障转移（无数据丢失）

主要副本可用时使用此方法，但需要暂时或永久更改配置，并更改托管主要副本的 SQL Server 实例。 发出手动故障转移前，确保目标次要副本为最新版本，避免潜在的数据丢失。 

手动故障转移（无数据丢失）：

1. 使目标次要副本 `SYNCHRONOUS_COMMIT`。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 运行以下查询，确定已将活动事务提交到主要副本和至少一个同步次要副本： 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   当 `synchronization_state_desc` 为 `SYNCHRONIZED` 时，会同步次要副本。

3. 将 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 更新为 1。

   以下脚本在名为 `ag1` 的 AG 上将 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 设置为 1。 运行以下脚本前，将 `ag1` 替换为 AG 的名称：

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   此设置可确保将每个活动事务提交到主要副本和至少一个同步次要副本。 

4. 将主要副本降级为次要副本。 将主要副本降级后，该副本为只读。 在托管主要副本的 SQL Server 实例上运行此命令，以将角色更新为 `SECONDARY`：

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. 将目标次要副本升级为主要副本。 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 若要删除 AG，请使用[删除可用性组](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)。 对于使用群集类型 NONE 或 EXTERNAL 创建的 AG，必须对属于该 AG 的所有副本执行该命令。