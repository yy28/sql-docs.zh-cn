## <a name="managing-synchronous-commit-mode"></a>管理同步提交模式

>[!WARNING]
>在某些情况下，Linux 上采用同步提交模式的 SQL Server 可用性组很容易发生数据丢失。 请参阅以下有关根本原因和解决方法的详细信息，确保避免数据丢失。 此问题将在以后的版本中解决。

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>有关可用性组资源升级的 Pacemaker 通知

在 CTP 1.4 版本推出之前，可用性组的 Pacemaker 资源代理不知道某个标记为 `SYNCHRONOUS_COMMIT` 的副本是否确实是最新的。 该副本有可能已停止与主副本同步，但资源代理并不知道这种情况。 因此，代理可能会将过时的副本升级为主副本 - 如果升级成功，将导致数据丢失。 

SQL Server 自 2017 年 1 CTP 1.4 添加`sequence_number`到`sys.availability_groups`若要解决此问题。 `sequence_number` 是一个单调递增的 BIGINT，表示本地 AG 副本相对于系统中其余副本的新旧程度。 执行故障转移、添加/删除副本和其他 AG 操作会更新此数字。 该数字将在主副本上更新，然后推送到辅助副本。 因此，处于最新状态的辅助副本上的数字与主副本相同。

当 Pacemaker 决定将某个副本升级为主副本时，首先会向所有副本发送通知，以提取并存储序列号。 接下来，当 Pacemaker 实际尝试将某个副本升级为主副本时，如果该副本的序列号在所有序列号中是最高的，则该副本只会提升自身，并拒绝其他升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。

请注意，仅当至少有一个可用于升级的副本的序列号与以前的主副本相同时，才能保证这种结果。 由于资源代理需要 Pacemaker 将通知发送到所有副本，因此需要使用 `notify=true` 配置可用性资源。 对于现有的每个 `ocf:mssql:ag` 资源，用户需要在将 `mssql-server-ha` 包更新到 CTP 1.4 之前使用 `notify=true` 更新资源配置，否则该资源将进入错误状态。 

### <a name="how-to-avoid-potential-for-data-loss"></a>如何避免数据丢失的可能性 

在以下情况下，可用性组仍可能容易发生数据丢失。 在包含五个节点的群集中，如果某个可用性组的副本位于 SQL Server 的三个实例上，则主副本和一个辅助副本可能会出现在其他辅助副本的前面。 如果是这样，`sys.availability_groups` 中的 `sequence_number` 将高于其他副本。 在此情况下，如果两个副本与群集中的其余节点断开连接，Pacemaker 可以看到仲裁形式的剩余三个节点，并允许落后的副本将其自身升级为主副本。 在这种情况下，有可能会丢失数据。

sql2017 引入了用于强制一定数量的辅助副本可用之后, 才能任何事务可以提交在主计算机上的新功能。 使用 `REQUIRED_COPIES_TO_COMMIT` 可以设置在继续事务之前，必须提交到辅助副本数据库事务日志的副本数。 可以结合 `CREATE AVAILABILITY GROUP` 或 `ALTER AVAILABILITY GROUP` 使用此选项。 请参阅 [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx)。

若要避免上面所述的数据丢失的可能性，请将 `REQUIRED_COPIES_TO_COMMIT` 设置为已同步副本的最大数目。 以后的版本将采用内置逻辑来自动处理 `REQUIRED_COPIES_TO_COMMIT` 的设置。
设置 `REQUIRED_COPIES_TO_COMMIT` 后，主副本数据库中的事务将等待在所需数目的同步辅助副本数据库事务日志中提交事务。 如果足够数目的同步辅助副本未联机，事务将会停止，直到与足够数目的辅助副本的通信恢复。

以下示例将可用性组名称 [ag1] 设置为 `REQUIRED_COPIES_TO_COMMIT = 2`。 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

在上面的示例中，如果可用性组包含两个辅助副本，它将等待两个辅助副本确认提交。 如果其中一个副本无响应，事务将被阻塞。
