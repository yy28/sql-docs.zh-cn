---
title: "次要副本的自动种子设定 (SQL Server) | Microsoft Docs"
description: "使用自动种子设定初始化次要副本。"
services: data-lake-analytics
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Automatic seeding [SQL Server], secondary replica
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1b72f9f5bf58f72bb4284b1a6cc8d0af7a722aed
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="automatic-seeding-for-secondary-replicas"></a>次要副本的自动种子设定

[!INCLUDE [tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2012 和 2014 中，初始化可用性组中的次要副本的唯一方法是使用备份、复制和还原。 SQL Server 2016 引入了用于初始化次要副本的新功能 - 自动种子设定。 自动种子设定使用日志流传输将使用 VDI 的备份流式传输到使用所配置终结点的可用性组的每个数据库的次要副本。 最初创建可用性组或将数据库添加到可用性组时，可以使用此新功能。 支持 AlwaysOn 可用性组的所有 SQL Server 版本都支持自动种子设定，并可与传统可用性组和[分布式可用性组](distributed-availability-groups.md)一起使用。

## <a name="considerations"></a>注意事项

使用自动种子设定的注意事项包括：

* [对主要副本的性能和事务日志影响](#performance-and-transaction-log-impact-on-the-primary-replica)
* [磁盘布局](#disk-layout)
* [安全性](#security)


### <a name="performance-and-transaction-log-impact-on-the-primary-replica"></a>对主要副本的性能和事务日志影响

自动种子设定是否可用于初始化次要副本具体取决于数据库大小、网络速度，以及主要副本和次要副本之间的距离。 例如，假定：

* 数据库大小为 5 TB
* 网络速度为 1 Gb/秒
* 两个站点之间的距离为 1000 英里

全带宽可用时，1 Gb/s 的网络可以提供 125 MB/s 的持续吞吐量。 在上述条件下，自动种子设定需要超过 11 个小时的时间。 在实践中，自动种子设定进程要稍慢一些，因为网络信号随着距离的增加而降低，并且通常会与网络上的其他资源共享链路。 在种子设定过程中，主要副本上的数据库事务日志将继续增大，并且在该数据库的自动种子设定完成之前无法截断。  然后，可以使用事务日志备份截断事务日志。

自动种子设定是一种可处理最多五个数据库的单线程进程。 这可能会影响性能，尤其是在可用性组具有多个数据库的情况下。

自动种子设定可以使用压缩，但它默认处于禁用状态。 启用压缩可减少网络带宽并可能加快进程速度，但代价是增加处理器开销。 若要在自动种子设定过程中使用压缩，请启用跟踪标志 9567 - 请参阅[调整可用性组的压缩](tune-compression-for-availability-group.md)。

### <a name="disk-layout"></a>磁盘布局

自动种子设定将在其中创建数据库的文件夹必须已经存在，并且与主要副本上的路径相同。

### <a name="security"></a>安全性

安全性权限根据要初始化的副本类型而有所不同：

* 对于传统可用性组，必须向次要副本上的可用性组授予权限，因为它已联接到可用性组。 在 Transact-SQL 中，使用命令 ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE。
* 对于分布式可用性组（其中正在创建的副本的数据库位于第二个可用性组的主要副本上），无需额外的权限，因为它已是主要副本。
* 对于分布式可用性组的第二个可用性组上的次要副本，必须使用命令 ALTER AVAILABILITY GROUP [2ndAGName] GRANT CREATE ANY DATABASE。 将从第二个可用性组的主要副本对此次要副本进行种子设定。

## <a name="create-an-availability-group-with-automatic-seeding"></a>使用自动种子设定创建可用性组

使用自动种子设定通过 Transact-SQL 或 SQL Server Management Studio（SSMS，版本 17 或更高版本）创建可用性组。 若要使用 SSMS 中的可用性组向导，请遵循[这些说明](use-the-availability-group-wizard-sql-server-management-studio.md) - 进行到步骤 9 时，你将看到自动种子设定为第一个和默认选项。

![选择初始数据同步][1]

以下示例使用 Transact-SQL 创建可用性组。 另请参阅主题[创建可用性组 (Transact-SQL)](create-an-availability-group-transact-sql.md)。 通过将 SEEDING_MODE 选项设置为 AUTOMATIC，在次要副本上启用种子设定。 默认行为是 MANUAL，这是 SQL Server 2016 之前的行为，需要在主要副本上进行数据库备份、将备份文件复制到次要副本并通过 WITH NORECOVERY 还原备份。

```
CREATE AVAILABILITY GROUP [AGName]
  FOR DATABASE db1
  REPLICA ON N'Primary_Replica'
WITH (
  ENDPOINT_URL = N'TCP://Primary_Replica.Contoso.com:5022', 
  FAILOVER_MODE = AUTOMATIC, 
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
),
  N'Secondary_Replica' WITH (
    ENDPOINT_URL = N'TCP://Secondary_Replica.Contoso.com :5022', 
    FAILOVER_MODE = AUTOMATIC, 
    SEEDING_MODE = AUTOMATIC);
 GO
```

在执行 CREATE AVAILABILITY GROUP 语句期间在主要副本上设置 SEEDING_MODE 不起作用，因为主要副本已包含数据库的主要读/写副本。 仅当另一个副本被设为主要副本并添加数据库时，才应用 SEEDING_MODE。 稍后可更改种子设定模式 - 请参阅[更改副本的种子设定模式](#change-the-seeding-mode-of-a-replica)。

在成为次要副本的实例上，一旦联接实例，SQL Server 日志中将添加以下消息：

可用性组“AGName”的本地可用性副本无权创建数据库，但 SEEDING_MODE 为 AUTOMATIC。 使用 ALTER AVAILABILITY GROUP… GRANT CREATE ANY DATABASE 命令，以允许创建由主要可用性副本进行种子设定的数据库。

联接后，发出以下语句：

```
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE
 GO
````

> [!NOTE] 
> 从 SQL Server 2016 SP1 CU2 开始，当前存在一个已知问题，即次要副本必须等待三分钟以允许可用性组对数据库进行种子设定，然后才能执行 ALTER AVAILABILITY GROUP... 语句。 在该时间过去之前，该语句不会返回错误，而是指示成功。 这也是一个已知问题。 这些问题将在 SQL Server 将来的更新中修复。 其中一种解决方法是插入 WAITFOR 语句：

```
WAITFOR DELAY '00:03:15';
ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE;
GO
```

如果成功，则将在次要副本上自动创建具有下列任一状态的数据库：

* 已同步（如果次要副本配置为同步，且数据已完成同步）。
* 正在同步（如果通过异步数据移动配置次要副本，或通过同步进行配置但尚未与主要副本进行同步）。

<a name="sql-server-log"></a>除了如下所述的[动态管理视图](#dynamic-management-views)，还可在 SQL Server 日志中看到开始和完成自动种子设定：

![SQL Server 日志][2]

## <a name="combine-backup-and-restore-with-automatic-seeding"></a>使用自动种子设定合并备份和还原

可使用自动种子设定合并传统的备份、复制和还原。 在这种情况下，首先还原次要副本上的数据库，包括所有可用的事务日志。 接下来，在创建可用性组以“捕获”次要副本的数据库时启用自动种子设定，就像已还原结尾日志备份一样（请参阅[结尾日志备份 (SQL Server)](../../../relational-databases/backup-restore/tail-log-backups-sql-server.md)）。

## <a name="add-a-database-to-an-availability-group-with-automatic-seeding"></a>使用自动种子设定将数据库添加到可用性组

可以使用自动种子设定通过 Transact-SQL 或 SQL Server Management Studio（SSMS，版本 17 或更高版本）将数据库添加到可用性组。
如果在将次要副本添加到可用性组时，次要副本使用了自动种子设定，则无需进行任何其他操作。 如果使用了备份、复制和还原，请首先更改种子设定模式（请参阅下一节），然后使用 GRANT 语句添加数据库 - 请参阅[可用性组 - 添加数据库](availability-group-add-a-database.md)。

## <a name="change-the-seeding-mode-of-a-replica"></a>更改副本的种子设定模式

创建可用性组后，可以更改副本的种子设定模式，因此可以启用或禁用自动种子设定。 在创建可用性组后启用自动种子设定可实现使用自动种子设定将数据库添加到可用性组，前提是该数据库通过备份、复制和还原创建。 例如：

```
ALTER AVAILABILITY GROUP [AGName]
  MODIFY REPLICA ON 'Replica_Name'
  WITH (SEEDING_MODE = AUTOMATIC)
```

若要禁用自动种子设定，请使用值 MANUAL。

## <a name="prevent-automatic-seeding-after-an-availability-group-is-created"></a>创建可用性组后阻止自动种子设定

如果不希望对次要副本完全禁用自动种子设定，但想要暂时防止次要副本自动创建数据库，请拒绝可用性组 CREATE 权限。 这种情况即，已向可用性组添加新数据库，但不允许可用性组在次要副本上创建数据库。

```
ALTER AVAILABILITY GROUP [AGName] DENY CREATE ANY DATABASE
GO
```

## <a name="monitor-automatic-seeding"></a>监视自动种子设定

监视自动种子设定并对其进行故障排除的方法有四种：

* [SQL Server 日志](#sql-server-log)（之前已介绍）
* [动态管理视图](#dynamic-management-views)
* [备份历史记录表](#backup-history-tables)
* [扩展事件](#extended-events)

### <a name="dynamic-management-views"></a>动态管理视图

有两个动态管理视图 (DMV) 可用于监视种子设定：sys.dm_hadr_automatic_seeding 和 sys.dm_hadr_physical_seeding_stats。

* sys.dm_hadr_automatic_seeding 包含自动种子设定的常规状态，并保留了每次执行（无论成功与否）的历史记录。 列 current_state 将具有值 COMPLETED 或 FAILED。 如果值为 FAILED，请使用 failure_state_desc 中的值以帮助诊断问题。 可能需要将其与 [SQL Server 日志](#sql-server-log)中的内容相结合，以确定问题所在。 此 DMV 填充在主要副本和所有次要副本上。

* sys.dm_hadr_physical_seeding_stats 显示在执行自动种子设定操作时自动种子设定操作的状态。 与 sys.dm_hadr_automatic_seeding 一样，这将在主要副本和次要副本上显示值，但不会存储此历史记录。 这些值仅针对当前执行，且不会保留。 相关的列包括 start_time_utc、end_time_utc、estimate_time_complete_utc、total_disk_io_wait_time_ms、total_network_wait_time_ms，如果种子设定操作失败，则还包括 failure_message。

### <a name="backup-history-tables"></a>备份历史记录表

自动种子设定还会将条目放入 `msdb` 表中，该表存储用于备份和还原的历史记录。 在接收自动种子设定的次要副本上，`backupmediafamily` 表的 physical_device_name 列的值为 GUID，`backupset` 中的相应条目为 server_name 和 machine_name 的主要副本的名称。

### <a name="extended-events"></a>扩展事件

自动种子设定添加了新的扩展事件，用于在初始化过程中跟踪状态更改、故障和性能统计信息。
例如，以下脚本会创建用于捕获自动种子设定相关事件的扩展事件会话。

```
CREATE EVENT SESSION [AG_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(SET filename=N’autoseed.xel’,max_file_size=(5),max_rollover_files=(4))
  WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO
```

下表列出了与自动种子设定相关的扩展事件。

|Name|说明|
|----|-----------|
|hadr_db_manager_seeding_request_msg|种子设定请求消息。|
|hadr_physical_seeding_backup_state_change|物理种子设定备份端状态更改。|
|hadr_physical_seeding_restore_state_change|物理种子设定还原端状态更改。|
|hadr_physical_seeding_forwarder_state_change|物理种子设定转发器端状态更改。|
|hadr_physical_seeding_forwarder_target_state_change|物理种子设定转发器目标端状态更改。|
|hadr_physical_seeding_submit_callback|物理种子设定提交回调事件。|
|hadr_physical_seeding_failure|物理种子设定失败事件。|
|hadr_physical_seeding_progress|物理种子设定进度事件。|
|hadr_physical_seeding_schedule_long_task_failure|物理种子设定计划长任务失败事件。|
|hadr_automatic_seeding_start|在提交自动种子设定操作时发生。|
|hadr_automatic_seeding_state_transition|在自动种子设定操作更改状态时发生。|
|hadr_automatic_seeding_success|在自动种子设定操作成功时发生。|
|hadr_automatic_seeding_failure|在自动种子设定操作失败时发生。|
|hadr_automatic_seeding_timeout|在自动种子设定操作超时时发生。|

## <a name="see-also"></a>另请参阅

[更改可用性组 (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)

[CREATE AVAILABILITY GROUP (Transact-SQL)](https://msdn.microsoft.com/library/ff878399.aspx)（创建可用性组 (Transact-SQL)）

[AlwaysOn 可用性组故障排除和监视指南](http://technet.microsoft.com/library/dn135328.aspx)

> 本文内容由 Microsoft 最有价值专家 [Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20Hirt) 编写。

<!--Image references-->
[1]: ./media/auto-seed-new-availability-group.png
[2]: ./media/auto-seed-sql-server-log.png

