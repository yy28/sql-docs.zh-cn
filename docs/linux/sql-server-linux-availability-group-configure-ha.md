---
title: "配置 SQL Server Always On 可用性组以在 Linux 上实现高可用性 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: c1d84ae8ac797775759bc53a29cc55acd1323f32
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>配置 SQL Server Always On 可用性组以在 Linux 上实现高可用性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上创建 SQL 服务器始终在可用性组 (AG) 以实现高可用性。 有两种配置类型为承载个可用性组。 A*高可用性*配置使用群集管理器提供业务连续性。 此配置还可以包括读取缩放副本。 本文档说明如何创建可用性组以实现高可用性。

你还可以创建可用性组，而无需群集管理器*读取缩放*。 为读取横向可用性组仅提供性能向外扩展的只读副本。它不提供高可用性。 若要创建为读取横向可用性组，请参阅[在 Linux 上配置 SQL Server 可用性组进行读取横向](sql-server-linux-availability-group-configure-rs.md)。

保证高可用性和数据保护的配置需要两个或三个同步提交副本。 具有三个同步副本，即使一个服务器不可用，可以自动将恢复可用性组。 有关详细信息，请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。 

所有服务器必须都是物理还是虚拟的并且虚拟服务器必须都是相同的虚拟化平台上。 此要求是因为隔离代理是特定于平台。 请参阅[来宾群集的策略](https://access.redhat.com/articles/29440#guest_policies)。

## <a name="roadmap"></a>路线图

在以实现高可用性的 Linux 服务器上创建可用性组的步骤是不同于 Windows Server 故障转移群集上的步骤。 以下列表描述的高级步骤： 

1. [三个群集服务器上配置 SQL Server](sql-server-linux-setup.md)。

   >[!IMPORTANT]
   >可用性组中的所有三个服务器需要位于相同的平台的物理或虚拟的因为 Linux 高可用性使用隔离代理来隔离服务器上的资源。 隔离代理是特定于每个平台。

2. 创建可用性组。 本文介绍了此步骤。 

3. 配置 Pacemaker 之类的群集资源管理器。
   
   配置群集资源管理器的方式取决于特定的 Linux 分发版。 请参阅以下链接了解分发具体说明： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >生产环境需要 STONITH 之类的隔离代理，以获得高可用性。 本文档中的演示不使用隔离代理。 演示仅用于测试和验证目的。 
   
   >Linux 群集使用隔离将群集返回到已知状态。 配置隔离的方式取决于分发和环境。 目前，隔离不是在某些云环境中可用的。 有关详细信息，请参阅[RHEL 高可用性群集的虚拟化平台的支持策略](https://access.redhat.com/articles/29440)。
   
   >SLES，请参阅[SUSE Linux Enterprise 高可用性扩展](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. 将可用性组添加为群集中的资源。  

   若要将可用性组添加为群集中的资源的方式取决于在 Linux 分发。 请参阅以下链接了解分发具体说明： 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>创建可用性组

对于高可用性配置，以确保自动故障转移，可用性组要求至少三个副本。 采用以下配置可支持高可用性：

- [三个同步副本](sql-server-linux-availability-group-ha.md#threeSynch)

- [两个同步副本加上配置副本](sql-server-linux-availability-group-ha.md#twoSynch)

有关信息，请参阅[可用性组配置的高可用性和数据保护](sql-server-linux-availability-group-ha.md)。

>[!NOTE]
>可用性组可以包括其他同步或异步副本。 

在 Linux 上创建可用性组以实现高可用性。 使用[创建可用性组](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql)与`CLUSTER_TYPE = EXTERNAL`。 

* 可用性组-`CLUSTER_TYPE = EXTERNAL`指定外部群集实体管理可用性组。 Pacemaker 是外部群集实体的示例。 当可用性组群集类型是外部， 

* 设置主要和辅助副本`FAILOVER_MODE = EXTERNAL`。 
   指定与外部群集管理器，如 Pacemaker 交互副本。 

下面的 TRANSACT-SQL 脚本创建名为的高可用性 AG `ag1`。 脚本将与可用性组副本`SEEDING_MODE = AUTOMATIC`。 此设置会导致 SQL Server 在每个辅助服务器上自动创建数据库。 为环境更新以下脚本。 替换`<node1>`， `<node2>`，或`<node3>`具有承载副本的 SQL Server 实例的名称的值。 替换`<5022>`端口你设置镜像终结点的数据。 若要创建可用性组，请在承载主副本的 SQL Server 实例上运行以下 TRANSACT-SQL。

运行**只有一个**的以下脚本： 

- [创建具有三个同步副本的可用性组](#threeSynch)。
- [创建具有两个同步副本和配置副本的可用性组](#configOnly)
- [创建具有两个同步副本的可用性组](#readScale)。

<a name="threeSynch"></a>

- 创建具有三个同步副本的可用性组

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >运行上述脚本创建具有三个同步副本的可用性组后，不运行以下脚本：

- 创建具有两个同步副本和配置副本的可用性组：

   >[!IMPORTANT]
   >此体系结构允许任何版本的 SQL Server 以承载第三个副本。 例如，可以在 SQL Server Enterprise Edition 上承载的第三个副本。 在 Enterprise Edition 上是唯一有效的终结点类型`WITNESS`。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- 创建具有两个同步副本的可用性组

   包括与同步的可用性模式的两个副本。 例如，以下脚本创建调用 AG `ag1`。 `node1` 和`node2`驻留在同步模式下，使用自动种子设定和自动故障转移的副本。

   >[!IMPORTANT]
   >仅运行以下脚本来创建具有两个同步副本的可用性组。 如果在运行前面编写的脚本，则不运行以下脚本。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


你还可以配置与 AG`CLUSTER_TYPE=EXTERNAL`使用 SQL Server Management Studio 或 PowerShell。 

### <a name="join-secondary-replicas-to-the-ag"></a>将辅助副本联接到可用性组

下面的 TRANSACT-SQL 脚本将 SQL Server 实例联接到可用性组名为`ag1`。 为环境更新脚本。 在每个承载辅助副本的 SQL Server 实例，运行以下 TRANSACT-SQL 加入可用性组。

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>创建可用性组后，你必须使用群集技术，如 Pacemaker 以实现高可用性配置集成。 有关使用承载个可用性组，从开始读取扩展配置[!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)]，不需要设置群集。

如果你遵循本文档中的步骤，则必须尚未群集可用性组。 下一步是添加该群集。 此配置可用于读取-缩放/负载平衡方案，它并不完整的高可用性。 对于高可用性，你需要将可用性组添加为群集资源。 请参阅[下一步行动](#next-steps)有关的说明。 

## <a name="notes"></a>说明

>[!IMPORTANT]
>配置群集和可用性组添加为群集资源后，不能使用 Transact SQL 故障转移的可用性组资源。 Linux 上的 SQL Server 群集资源与此操作系统的耦合性不及 Windows Server 故障转移群集 (WSFC) 上的高。 SQL Server 服务不知道此群集的存在。 所有业务流程都通过群集管理工具完成。 在 RHEL 或 Ubuntu 使用`pcs`。 在 SLES 使用`crm`。 

>[!IMPORTANT]
>如果可用性组是群集资源，其中强制故障转移到异步副本的数据丢失不起作用的当前版本没有已知的问题。 此问题将在即将发布的版本中得到解决。 手动或自动故障转移到同步副本成功。 


## <a name="next-steps"></a>后续步骤

[配置 SQL Server 可用性组群集资源的 Red Hat Enterprise Linux 群集](sql-server-linux-availability-group-cluster-rhel.md)

[为 SQL Server 可用性组群集资源配置 SUSE Linux Enterprise Server 群集](sql-server-linux-availability-group-cluster-sles.md)

[配置 SQL Server 可用性组群集资源的 Ubuntu 群集](sql-server-linux-availability-group-cluster-ubuntu.md)
