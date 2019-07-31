---
title: 配置分布式可用性组
description: '介绍如何创建和配置分布式 Always On 可用性组。 '
ms.custom: seodec18
ms.date: 08/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a90f9b303fa285c5fc826aab232abe3e07166992
ms.sourcegitcommit: 67261229b93f54f9b3096890b200d1aa0cc884ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68354600"
---
# <a name="configure-a-distributed-always-on-availability-group"></a>配置分布式 Always On 可用性组  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

若要创建分布式可用性组，必须拥有两个各自具有其侦听器的可用性组。 然后将这些可用性组合并到分布式可用性组中。 以下步骤提供了在 Transact-SQL 中实现此操作的基本示例。 此示例不涵盖创建可用性组和侦听器的所有详细信息，相反，它着重于突出显示关键要求。

有关分布式可用性组的技术概述，请参阅[分布式可用性组](distributed-availability-groups.md)。

## <a name="prerequisites"></a>必备条件

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>设置终结点侦听程序以侦听所有 IP 地址

确保终结点可在分布式可用性组中的不同可用性组之间进行通信。 如果将一个可用性组设置为终结点上的特定网络，分布式可用性组将无法正常工作。 在分布式可用性组中承载副本的每台服务器上，将侦听器设置为侦听所有 IP 地址 (`LISTENER_IP = ALL`)。

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>创建侦听程序以侦听所有 IP 地址

例如，以下脚本可在 TCP 端口 5022 上创建侦听所有 IP 地址的侦听程序终结点。  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>更改侦听程序以侦听所有 IP 地址

例如，以下脚本可更改侦听程序终结点以侦听所有 IP 地址。  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>创建第一个可用性组

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>在第一个群集上创建主要可用性组  
在第一个 Windows Server 故障转移群集 (WSFC) 上创建可用性组。   在此示例中，将用于数据库 `ag1` 的可用性组命令为 `db1`。 主可用性组的主要副本在分布式可用性组中称为全局主要副本  。 Server1 是此示例中的全局主要副本。        
  
```sql  
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
  
>[!NOTE]
>上述示例使用自动种子设定，其中 SEEDING_MODE 设置为 AUTOMATIC，用于副本和分布式可用性组   。 此配置将设置次要副本和次要可用性组自动填充，而无需手动备份和还原主要数据库。  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>将次要副本联接到主要可用性组  
任何次要副本都必须使用 **JOIN** 选项联接到具有 **ALTER AVAILABILITY GROUP** 的可用性组。 由于在此示例中使用了自动种子设定，因此也必须调用具有 GRANT CREATE ANY DATABASE 选项的 ALTER AVAILABILITY GROUP   。 此设置允许可用性组创建数据库并开始从主要副本自动进行种子设定。  
  
在此示例中，在次要副本 `server2`上运行以下命令，以联接 `ag1` 可用性组。 允许可用性组在次要副本上创建数据库。  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>当可用性组在辅助副本上创建数据库时，它将数据库所有者设置为运行 `ALTER AVAILABILITY GROUP` 语句的帐户以授予创建任意数据库的权限。 有关详细信息，请参阅[授予可用性组在复制副本上创建数据库的权限](automatic-seeding-secondary-replicas.md#grantCreate)。
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>为主要可用性组创建侦听程序  

接下来，在第一个 WSFC 上为主要可用性组添加侦听器。 在此示例中，侦听器名为 `ag1-listener`。 有关创建侦听程序的详细说明，请参阅[创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>创建第二个可用性组  
 然后，在第二个 WSFC 上创建次要可用性组 `ag2`。 在这种情况下，不会指定数据库，因为它会自动从主要可用性组进行种子设定。  辅助可用性组的主要副本在分布式可用性组中称为转发器  。 在此示例中，server3 是转发器。 
  
```sql  
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
> 该次要可用性组必须使用相同的数据库镜像终结点（此示例中为端口 5022）。 否则，在本地故障转移后，副本会停止。  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>将次要副本联接到次要可用性组  
 在此示例中，在次要副本 `server4`上运行以下命令，以联接 `ag2` 可用性组。 允许可用性组在次要副本上创建数据库以支持自动种子设定。  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>为次要可用性组创建侦听器  
 接下来，在第二个 WSFC 上添加次要可用性组的侦听器。 在此示例中，侦听器名为 `ag2-listener`。 有关创建侦听程序的详细说明，请参阅[创建或配置可用性组侦听程序 (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>在第一个群集上创建分布式可用性组  
 在第一个 WSFC 上创建分布式可用性组（此示例中命名为 `distributedag` ）。 使用具有 **DISTRIBUTED** 选项的 **CREATE AVAILABILITY GROUP** 命令。 AVAILABILITY GROUP ON 参数指定了成员可用性组、`ag1` 和 `ag2`  。  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** 为每个可用性组指定了侦听程序与可用性组的数据库镜像端点。 在此示例中，为端口 `5022` （不是用于创建侦听程序的端口 `60173` ）。 如果使用的是负载均衡器，对于 Azure 中的实例，请[向分布式可用性组端口添加负载均衡规则](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group)。 向侦听器端口添加规则，除了 SQL Server 实例端口。 
  
## <a name="join-distributed-availability-group-on-second-cluster"></a>在第二个群集上联接分布式可用性组  
 然后，在第二个 WSFC 上联接分布式可用性组。  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="failover"></a> 联接第二个可用性组的辅助数据库
当第二个可用性组的次要副本上的数据库处于正在还原状态后，必须手动将它联接到可用性组。

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="failover"></a>故障转移到次要可用性组  

此时仅支持手动故障转移。 手动故障转移分布式可用性组：

1. 若要确保不会丢失任何数据，请将分布式可用性组设置为同步提交。
1. 等待分布式可用性组完成同步。
1. 在全局主要副本上，将分布式可用性组角色设置为 `SECONDARY`。
1. 测试故障转移就绪情况。
1. 故障转移主要可用性组。

以下 Transact-SQL 示例演示了对名为 `distributedag` 的分布式可用性组进行故障转移的详细步骤：

1. 通过在全局主要副本和转发器上同时  运行以下代码，将分布式可用性组设置为同步提交。   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   >[!NOTE]
   >在分布式可用性组中，两个可用性组之间的同步状态取决于两个副本的可用性模式。 对于同步提交模式，当前的主要可用性组和当前的次要可用性组必须具有 `SYNCHRONOUS_COMMIT` 可用性模式。 因此，必须在全局主要副本和转发器上运行上述脚本。

1. 等分布式可用性组的状态变为 `SYNCHRONIZED`。 对全局主要副本（主要可用性组的主要副本）运行以下查询。 
    
      ```sql  
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

    在可用性组 **synchronization_state_desc** 变为 `SYNCHRONIZED`后继续。 如果 **synchronization_state_desc** 不为 `SYNCHRONIZED`，请每隔五秒运行一次命令，直到变为该状态为止。 在 **synchronization_state_desc** = `SYNCHRONIZED`之前，不要继续操作。 

1. 在全局主要副本上，将分布式可用性组角色设置为 `SECONDARY`。 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    此时，分布式可用性组不可用。

1. 测试故障转移就绪。 运行以下查询：

    ```sql
    SELECT ag.name, 
        drs.database_id, 
        drs.group_id, 
        drs.replica_id, 
        drs.synchronization_state_desc, 
        drs.end_of_log_lsn 
    FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
    WHERE drs.group_id = ag.group_id; 
    ```  
    当 synchronization_state_desc 为 `SYNCHRONIZED` 且两个可用性组的 **end_of_log_lsn** 相同时，可用性组即可进行故障转移  。 

1. 从主要可用性组故障转移到次要可用性组。 在托管次要可用性组的主要副本的 SQL Server 上运行以下命令。 

    ```sql
    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    执行此步骤后，分布式可用性组将变为可用。
      
完成上述步骤后，分布式可用性组将进行故障转移，且不会丢失任何数据。 如果可用性组位于不同的地理位置，导致延迟，请将可用性模式改回为 ASYNCHRONOUS_COMMIT。 
  
## <a name="remove-a-distributed-availability-group"></a>删除分布式可用性组  
 以下 Transact-SQL 语句删除了名为 `distributedag`的分布式可用性组：  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>在故障转移群集实例上创建分布式可用性组

你可以使用故障转移群集实例 (FCI) 上的可用性组来创建分布式可用性组。 在此情况下，无需任何可用性组侦听器。 为 FCI 实例的主要副本使用虚拟网络名称 (VNN)。 以下示例演示了一个名为 SQLFCIDAG 的分布式可用性组。 一个可用性组为 SQLFCIAG。 SQLFCIAG 有 2 个 FCI 副本。 FCI 主要副本的 VNN 为 SQLFCIAG-1，FCI 次要副本的 VNN 为 SQLFCIAG-2。 该分布式可用性组还包含用于灾难恢复的 SQLAG-DR。

![AlwaysOn 分布式可用性组](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 以下 DDL 将创建此分布式可用性组。 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

侦听程序 URL 是主要 FCI 实例的 VNN。

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>在分布式可用性组中手动故障转移 FCI

若要手动故障转移 FCI 可用性组，请更新分布式可用性组，以反映侦听程序 URL 的更改。 例如，在 SQLFCIAG 的主要可用性组和次要可用性组上运行以下 DDL：

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>后续步骤

 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
