---
title: "分布式可用性组（AlwaysOn 可用性组） | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# 分布式可用性组（AlwaysOn 可用性组）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  分布式可用性组使你能够关联驻留在不同 Windows Server 故障转移群集 (WSFC) 上的两个可用性组。 分布式可用性组的主要用途之一是用于灾难恢复，在灾难恢复过程中，主站点将从地理上与 DR 站点分散。 你想让数据继续复制到 DR 站点，但不希望出现潜在的网络问题或 DR 站点出现问题，从而造成主站点崩溃。  
  
 下图对分布式可用性组的结构进行了说明。  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 在上图中，有两个单独的 Windows Server 故障转移群集（WFSC 1 和 WFSC 2）。 每个群集都有其自己的与数据库配置匹配的可用性组。 可以将分布式可用性组视作“可用性组的可用性组”。 在此示例中，AG 1 成为了主要可用性组。 所有的插入和更新操作都对主要副本 AG 1 执行，然后再复制到其次要副本。 但是也会在网络中将更改一次复制到 WSFC 2 上的次要可用性组。 AG 2 可用性组将这些更改复制到其次要副本中。  
  
> [!IMPORTANT]  
>  当在两个可用性组之间建立分布式可用性组关系时，次要可用性组将自动变为只读。 只能对主要可用性组的主要副本（在此示例中，AG 1 为主要副本）执行更新和插入操作。  
  
 在单个 Windows Server 故障转移群集上，分布式可用性组在以下方面不同于可用性组：  
  
-   每个 WSFC 维护其自己的仲裁模式和节点投票配置。 这意味着次要 WSFC 的运行状况不会影响主要 WSFC。  
  
-   在该群集内通过网络将数据一次发送到次要 WSFC，然后进行复制。 在单个 WSFC 中，数据会单独发送到每个副本。 对于地理上分散的次要站点，分布式可用性组将更有效。  
  
-   主要和次要群集上使用的操作系统版本可能会不同。 在单个 WSFC 中，所有服务器的操作系统版本都必须相同。 这有可能使用具有滚动更新/升级操作系统特性的分布式可用性组。  
  
-   主要和次要可用性组必须拥有相同的数据库配置。  
  
-   不支持自动故障转移到次要可用性组。  
  
## 创建分布式可用性组  
 若要创建分布式可用性组，必须在每个 WSFC 上创建可用性组和侦听器。 然后将这些合并到分布式可用性组中。 以下步骤提供了在 Transact-SQL 中实现此操作的基本示例。 此示例不涵盖创建可用性组和侦听器的所有详细信息，相反，它着重于突出显示关键要求。  
  
### 在第一个群集上创建主要可用性组  
 在第一个 WSFC 上创建可用性组。   在此示例中，将用于数据库 `ag1` 的可用性组命令为 `db1`。  
  
```tsql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
 请注意，本示例使用直接的种子设定，其中 **SEEDING_MODE** 设置为 **AUTOMATIC**，用于副本和分布式可用性组。 这意味着一旦建立后，次要副本和次要可用性组将自动填充，而无需手动备份和还原主要数据库。  
  
### 将次要副本联接到主要可用性组  
 任何次要副本都必须使用 **JOIN** 选项联接到具有 **ALTER AVAILABILITY GROUP** 的可用性组。 因为在此示例中使用了直接的种子设定，因此也必须调用具有  **GRANT CREATE ANY DATABASE** 选项的 **ALTER AVAILABILITY GROUP** 。 这允许可用性组创建数据库并开始从主要副本自动进行种子设定。  
  
 在此示例中，在次要副本 `server2`上运行以下命令，以联接 `ag1` 可用性组。 允许可用性组在次要副本上创建数据库。  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 为主要可用性组创建侦听器  
 接下来，在第一个 WSFC 上为主要可用性组添加侦听器。 在此示例中，侦听器名为 `ag1-listener`。 有关创建侦听程序的详细说明，请参阅[创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 在第二个群集上创建次要可用性组  
 然后，在第二个 WSFC 上创建次要可用性组 `ag2`。 在这种情况下，不会指定数据库，因为它会自动从主要可用性组进行种子设定。  
  
```tsql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
>  请注意，该次要可用性组必须使用相同的数据库镜像终结点（此示例中为端口 5022）。 否则，在本地故障转移后，副本会停止。  
  
### 将次要副本联接到次要可用性组  
 在此示例中，在次要副本 `server4`上运行以下命令，以联接 `ag2` 可用性组。 允许可用性组在次要副本上创建数据库以支持直接的种子设定。  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 为次要可用性组创建侦听器  
 接下来，在第二个 WSFC 上添加次要可用性组的侦听器。 在此示例中，侦听器名为 `ag2-listener`。 有关创建侦听程序的详细说明，请参阅[创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 在第一个群集上创建分布式可用性组  
 在第一个 WSFC 上创建分布式可用性组（此示例中命名为 `distributedag`）。 使用具有 **DISTRIBUTED** 选项的 **CREATE AVAILABILITY GROUP** 命令。 **AVAILABILITY GROUP ON** 参数指定了成员可用性组、`ag1` 和 `ag2`。  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** 为每个可用性组指定了侦听程序与可用性组的数据库镜像端点。 在此示例中，为端口 `5022`（不是用于创建侦听程序的端口 `60173`）。  
  
### 在第二个群集上联接分布式可用性组  
 然后，在第二个 WSFC 上联接分布式可用性组。  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## 故障转移到次要可用性组  
 此时仅支持手动故障转移。 以下 Transact-SQL 语句在名为 `distributedag` 的分布式可用性组上强制执行故障转移：  


1. 将次要可用性组的可用性模式设置为同步提交。 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. 等分布式可用性组的状态变为 `SYNCHRONIZED`。 在托管主要可用性组的主要副本的 SQL Server 上运行以下查询。 
    
      ```tsql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    在可用性组 **synchronization_state_desc** 变为 `SYNCHRONIZED` 后继续。 如果 **synchronization_state_desc** 不为 `SYNCHRONIZED`，请每隔五秒运行一次命令，直到变为该状态为止。 在 **synchronization_state_desc** = `SYNCHRONIZED` 之前，不要继续操作。 

1. 在托管主要可用性组的主要副本的 SQL Server 上，将分布式可用性组角色设置为 `SECONDARY`。 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    注意：此时，分布式可用性组不可用。

1. 测试故障转移就绪。 运行以下查询：

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    当 **synchronization_state_desc** 为 `SYNCHRONIZED` 且两个可用性组的 **end_of_log_lsn** 相同时，可用性组即可进行故障转移。 

1. 从主要可用性组故障转移到次要可用性组。 在托管次要可用性组的主要副本的 SQL Server 上运行以下命令。 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      注意：执行此步骤后，分布式可用性组将变为可用。
      
完成上述步骤后，分布式可用性组将进行故障转移，且不会丢失任何数据。 如果可用性组位于不同的地理位置，导致延迟，Microsoft 建议将可用性模式改回为 ASYNCHRONOUS_COMMIT。 
  
## 删除分布式可用性组  
 以下 Transact-SQL 语句删除了名为 `distributedag` 的分布式可用性组：  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## 使用故障转移群集实例创建分布式可用性组

你可以使用故障转移群集实例 (FCI) 上的可用性组来创建分布式可用性组。 在此情况下，无需任何可用性组侦听器。 为 FCI 实例的主要副本使用虚拟网络名称 (VNN)。 以下示例演示了一个名为 SQLFCIDAG 的分布式可用性组。 一个可用性组为 SQLFCIAG。 SQLFCIAG 有 2 个 FCI 副本。 FCI 主要副本的 VNN 为 SQLFCIAG-1，FCI 次要副本的 VNN 为 SQLFCIAG-2。 该分布式可用性组还包含用于灾难恢复的 SQLAG-DR。

![AlwaysOn 分布式可用性组](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 以下 DDL 将创建此分布式可用性组。 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

请注意，侦听器 URL 是主要 FCI 实例的 VNN。

## 在分布式可用性组中手动故障转移 FCI

若要手动故障转移 FCI 可用性组，请更新分布式可用性组，以反映侦听器 URL 的更改。 例如，在 SQLFCIAG 的主要可用性组和次要可用性组上运行以下 DDL：

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## 另请参阅  
 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  