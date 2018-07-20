---
title: 运行可用性组在 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 8f2978533bb1e4006db9ebf2d2ed97a242a6f603
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086319"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>始终对 Linux 上的可用性组

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>可用性组升级

在升级某一可用性组之前，请查看模式和实践[升级可用性组副本实例](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。

以下各节说明如何使用可用性组在 Linux 上执行滚动升级 SQL Server 实例。 

### <a name="upgrade-steps-on-linux"></a>Linux 上的升级步骤

在 Linux 中的 SQL Server 实例上可用性组副本时，可用性组的群集类型为`EXTERNAL`或`NONE`。 除了 Windows Server 故障转移群集 (WSFC) 是由群集管理器管理的可用性组`EXTERNAL`。 与 Corosync pacemaker 是外部群集管理器的示例。 没有群集管理器与可用性组具有群集类型`NONE`此处所述的升级步骤将为可用性组群集类型的特定`EXTERNAL`或`NONE`。

实例的升级的顺序取决于其角色是否为辅助数据库并且它们承载同步或异步副本。 第一次承载异步辅助副本的 SQL Server 实例进行升级。 然后，升级承载同步辅助副本的实例。 

   >[!NOTE]
   >如果可用性组仅具有异步副本，以避免任何数据丢失一个副本更改为同步，并等到它完成同步。 然后，升级此副本。
   
在开始之前，备份每个数据库。

1. 在承载辅助副本要升级的节点上停止资源。
   
   运行升级命令之前，停止资源，因此群集将不监视它并不必要地失败。 下面的示例资源以停止添加位置约束会导致在节点上。 更新`ag_cluster-master`在资源名称和`nodeName1`与托管升级的目标副本的节点。

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. 升级辅助副本上的 SQL Server。

   以下示例将升级`mssql-server`和`mssql-server-ha`包。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. 删除位置约束。

   运行升级命令之前，停止资源，因此群集将不监视它并不必要地失败。 下面的示例资源以停止添加位置约束会导致在节点上。 更新`ag_cluster-master`在资源名称和`nodeName1`与托管升级的目标副本的节点。

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   最佳做法是确保启动资源 (使用`pcs status`命令) 和辅助副本已连接，并且升级后同步状态。

1. 升级所有辅助副本后，手动故障转移到其中一个同步次要副本。

   为使用可用性组`EXTERNAL`群集类型，请使用群集管理工具进行故障转移; 可用性组与`NONE`应使用 TRANSACT-SQL 进行故障转移群集类型。 
   下面的示例将故障转移群集管理工具的可用性组。 替换为`<targetReplicaName>`将变为主数据库的同步辅助副本的名称：

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >以下步骤仅适用于没有群集管理器的可用性组。

   如果可用性组群集类型为`NONE`、 手动故障转移。 请按顺序完成下列步骤：

      A. 以下命令设置到辅助站点的主副本。 替换为`AG1`与可用性组的名称。 承载主副本的 SQL Server 实例上运行 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. 以下命令设置为主要副本同步的辅助副本。 SQL Server-承载同步辅助副本的实例的目标实例上运行以下 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 故障转移后，SQL Server 升级旧的主副本上通过重复前面的过程。

   以下示例将升级`mssql-server`和`mssql-server-ha`包。

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. 对于可用性组与外部群集管理器-的群集类型为 EXTERNAL，清理位置约束而引起的手动故障转移。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 恢复新升级的辅助副本-以前的主副本的数据移动。 SQL Server 的更高版本实例将日志块传输到可用性组中的较低版本实例时，此步骤是必需的。 在新的辅助副本 （以前的主副本） 上运行以下命令。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

升级后的所有服务器，则可以故障回复。 如有必要，则故障转移回原始的主要副本。 

## <a name="drop-an-availability-group"></a>删除可用性组

若要删除某一可用性组，请运行[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)。 如果群集类型为`EXTERNAL`或`NONE`承载副本的 SQL Server 的每个实例上运行命令。 例如，若要删除某一可用性组名为`group_name`运行以下命令：

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>后续步骤

[配置 SQL Server 可用性组群集资源的 Red Hat Enterprise Linux 群集](sql-server-linux-availability-group-cluster-rhel.md)

[为 SQL Server 可用性组群集资源配置 SUSE Linux Enterprise Server 群集](sql-server-linux-availability-group-cluster-sles.md)

[配置 Ubuntu 群集 SQL Server 可用性组群集资源](sql-server-linux-availability-group-cluster-ubuntu.md)
