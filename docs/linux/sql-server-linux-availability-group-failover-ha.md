---
title: "运行可用性组在 Linux 上的 SQL Server |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 6f060f110121bc744687b09a15e142112f48c86c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---

# <a name="operate-ha-availability-group-for-sql-server-on-linux"></a>对 Linux 上的 SQL Server 运行 HA 可用性组

## <a name="failover"></a>可用性组故障转移

使用群集管理工具管理的外部群集管理器的可用性组故障转移。 例如，如果解决方案使用 Pacemaker 管理的 Linux 群集，则使用`pcs`在 RHEL 或 Ubuntu 上执行手动故障转移。 在 SLES 上使用`crm`。 

> [!IMPORTANT]
> 在正常操作中，请勿使用 Transact-SQL 或 SQL Server 管理工具（如 SSMS 或 PowerShell）进行故障转移。 当`CLUSTER_TYPE = EXTERNAL`，仅可接受的值`FAILOVER_MODE`是`EXTERNAL`。 借助这些设置，所有手动或自动故障转移操作都由外部群集管理器执行。 

### <a name="manual-failover-examples"></a>手动故障转移示例

借助外部群集管理工具手动故障转移可用性组。 在正常操作中，请勿使用 Transact-SQL 启动故障转移。 如果未响应的外部群集管理工具，你可以强制可用性组进行故障转移。 若要强制手动故障转移的说明，请参阅[手动移动没有响应群集工具时](#forceManual)。

两步完成手动故障转移。 

1. 将资源组资源从拥有资源的群集节点移动到新节点。

   群集管理器移动可用组资源并添加位置约束。 此约束配置要在新节点上运行的资源。 为了移动是手动或自动故障转移在将来，你必须删除此约束。

2. 删除位置约束。

#### <a name="1-manually-fail-over"></a>1.手动故障转移

若要手动故障转移可用性组资源名为*ag_cluster*到名为的群集节点*nodeName2*，运行适合于你的分发的命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES 示例**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>手动故障转移资源后，你需要删除自动添加在移动期间的位置约束。

#### <a name="2-remove-the-location-constraint"></a>2.删除位置约束

在手动移动，`pcs`命令`move`或`crm`命令`migrate`添加针对要放置在新的目标节点上的资源的位置约束。 若要查看新约束，请在手动移动资源后运行以下命令：

- **RHEL/Ubuntu 示例**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES 示例**

   ```bash
   crm config show
   ```

需要删除位置约束，以便将来移动（包括自动故障转移）成功。 

若要删除约束，请运行以下命令。 

- **RHEL/Ubuntu 示例**

   在此示例中`ag_cluster-master`是已移动的资源的名称。 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES 示例**

   在此示例中`ag_cluster`是已移动的资源的名称。 

   ```bash
   crm resource clear ag_cluster
   ```

或者，可以运行以下命令删除位置约束。  

- **RHEL/Ubuntu 示例**

   在以下命令中，`cli-prefer-ag_cluster-master` 是需要删除的约束的 ID。 `sudo pcs constraint --full` 会返回此 ID。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **SLES 示例**

   在下面的命令`cli-prefer-ms-ag_cluster`是约束的 ID。 `crm config show` 会返回此 ID。 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>自动故障转移不会添加位置约束，因此不需要进行清除。 

详细信息：
- [Red Hat - 管理群集资源](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker-手动移动资源](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES 管理指南-资源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 

### <a name="forceManual"></a>手动移动没有响应群集工具时 

在极端情况下，如果用户不能使用的交互与群集的群集管理工具 （即群集无响应，群集管理工具具有错误的行为），用户可能需要手动的故障转移而跳过的外部群集管理器。 不建议用于常规操作，并且应在群集无法使用群集管理工具执行故障转移操作的情况下使用。

如果无法故障转移群集管理工具的可用性组，请按照以下步骤来从 SQL Server 工具故障转移操作：

1. 验证可用性组资源是否不再由群集管理。 

      - 尝试将资源设置为非托管模式。 这会指示资源代理停止监视和管理资源。 例如： 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - 如果未能将资源模式设置为非托管模式，请删除该资源。 例如：

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >删除某个资源时，还将删除所有关联的约束。 

1. 手动设置会话上下文变量`external_cluster`。

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. 使用 Transact-SQL 对可用性组进行故障转移。 在替换下面的示例`<**MyAg**>`替换为你的可用性组的名称。 连接到托管目标次要副本的 SQL Server 实例，并运行以下命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. 重新启动群集资源监视和管理。 运行以下命令：

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>数据库级别监视和故障转移触发器

有关`CLUSTER_TYPE=EXTERNAL`，故障转移触发器语义是不同相比 WSFC。 在 WSFC 中的 SQL Server 实例上可用性组时，转换外`ONLINE`状态的数据库会导致可用性组运行状况报告错误。 这将指示群集管理器触发故障转移操作。 在 Linux 上，SQL Server 实例不能与群集通信。 “由外而内”监视数据库运行状况。 如果用户选择用于监视数据库级别的故障转移和故障转移 (通过设置选项`DB_FAILOVER=ON`创建可用性组时)，群集将检查数据库状态是否为`ONLINE`每次运行监视的操作时。 群集查询中的状态`sys.databases`。 不同于任何状态`ONLINE`，自动 （如果满足自动故障转移条件），它将触发故障转移。 故障转移的实际时间取决于监视操作的频率以及 sys.databases 中正在更新的数据库状态。

## <a name="upgrade-availability-group"></a>升级的可用性组

在升级某一可用性组之前，审阅的最佳实践在[升级可用性组副本实例](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。

以下各节说明如何使用可用性组在 Linux 上执行滚动升级 SQL Server 实例。 

>[!WARNING]
>在 Linux 上，滚动升级到 SQL Server 自 2017 年 1 RC2 不支持。 升级辅助副本之后，它将断开连接从主副本中，直至升级主要副本。 Microsoft 规划以解决此问题在未来版本。 

### <a name="upgrade-steps-on-linux"></a>在 Linux 上的升级步骤

在 Linux 中的 SQL Server 实例上可用性组副本时，可用性组的群集类型是`EXTERNAL`或`NONE`。 除了 Windows Server 故障转移群集 (WSFC) 是之外，由群集管理器管理的可用性组`EXTERNAL`。 Pacemaker 使用 Corosync 是外部的群集管理器的示例。 具有未群集管理器的可用性组具有群集类型`NONE`此处所述的升级步骤是特定于可用性组的群集类型`EXTERNAL`或`NONE`。

1. 在开始之前，备份每个数据库。
2. 升级该主机辅助副本的 SQL Server 实例。

    a. 首先升级异步辅助副本。

    b. 升级同步辅助副本。

   >[!NOTE]
   >如果某一可用性组仅有异步副本-为了避免丢失任何数据更改为同步的一个副本，并等待，直到它已同步。 然后升级此副本。

   下面的示例将升级`mssql-server`和`mssql-server-ha`包。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

1. 升级所有辅助副本后，手动故障转移到其中一个同步的辅助副本。

   具有的可用性组`EXTERNAL`群集类型，请使用群集管理工具进行故障转移; 与可用性组`NONE`群集类型应使用 TRANSACT-SQL 来故障转移。 

   下面的示例故障转移群集管理工具具有的可用性组。 替换`<targetReplicaName>`替换将变为主数据库的同步辅助副本的名称：

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >以下步骤仅适用于不具有群集管理器的可用性组。  

   可用性组群集类型是否为`NONE`、 手动故障转移。 请按顺序完成下列步骤：

      a. 下面的命令设置到了辅助站点的主副本。 替换`AG1`替换为你的可用性组的名称。 在承载主副本的 SQL Server 的实例上运行 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. 下面的命令设置为主同步的辅助副本。 在 SQL Server-承载同步辅助副本的实例的目标实例上运行以下 TRANSACT-SQL 命令。

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. 故障转移后，旧的主副本上升级 SQL Server。 

   下面的示例将升级`mssql-server`和`mssql-server-ha`包。

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

1. 对于可用性组使用的外部群集管理器-群集在其中键入是外部，清理而引起的手动故障转移的位置约束。 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. 恢复新升级的辅助副本-以前的主副本的数据移动。 SQL Server 的更高版本实例将日志块传输到可用性组中的较低版本实例时，这是必需的。 在新的辅助副本 （以前的主副本） 上运行以下命令。

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

升级后的所有服务器，你可以故障回复的故障转移回原始主副本的如有必要。 

## <a name="drop-an-availability-group"></a>删除可用性组

若要删除某一可用性组，运行[DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md)。 群集类型是否为`EXTERNAL`或`NONE`承载副本的 SQL Server 的每个实例上运行命令。 例如，若要删除某一可用性组名为`group_name`运行以下命令：

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>后续步骤

[配置 SQL Server 可用性组群集资源的 Red Hat Enterprise Linux 群集](sql-server-linux-availability-group-cluster-rhel.md)

[为 SQL Server 可用性组群集资源配置 SUSE Linux Enterprise Server 群集](sql-server-linux-availability-group-cluster-sles.md)

[配置 SQL Server 可用性组群集资源的 Ubuntu 群集](sql-server-linux-availability-group-cluster-ubuntu.md)

