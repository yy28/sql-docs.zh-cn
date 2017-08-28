## <a name="pacemakerNotify"></a>了解 Pacemaker 的 SQL Server 资源代理

在 CTP 1.4 版本推出之前，可用性组的 Pacemaker 资源代理无法确定某个标记为 `SYNCHRONOUS_COMMIT` 的副本是否确实是最新的。 该副本有可能已停止与主副本同步，但资源代理并不知道这种情况。 因此，代理可能会将过时的副本升级为主要副本 - 如果升级成功，将导致数据丢失。 

SQL Server 2017 CTP 1.4 在 `sys.availability_groups` 中添加了 `sequence_number`，从而解决了此问题。 `sequence_number` 是一个单调递增的 BIGINT，表示本地可用性组副本相对于可用性组中其余副本的新旧程度。 执行故障转移、添加或删除副本和其他可用性组操作会更新此数字。 该数字将在主要副本上更新，然后推送到次要副本。 因此，处于最新状态的次要副本的 sequence_number 与主要副本相同。 

当 Pacemaker 决定将某个副本升级为主要副本时，首先会向所有副本发送通知，以提取并存储序列号（我们将其称为预升级通知）。 接下来，当 Pacemaker 实际尝试将某个副本升级为主要副本时，如果该副本的序列号在所有副本的序列号中是最高的，则该副本只会升级自身，并拒绝其他升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。 

请注意，仅当至少有一个可用于升级的副本的序列号与以前的主副本相同时，才能保证这种结果。 为确保这一点，默认行为是，Pacemaker 资源代理自动设置 `REQUIRED_COPIES_TO_COMMIT`，从而使至少一个同步提交次要副本处于最新状态且可用作自动故障转移的目标。 对于每个监视操作，`REQUIRED_COPIES_TO_COMMIT` 的值按“同步提交副本数/2”的方式进行计算（如果需要，也将进行更新）。 然后，在故障转移时，此资源代理需要一定数量的副本（`total number of replicas` - `required_copies_to_commit` 个副本）响应预升级通知，从而能够将其中一个副本升级为主要副本。 `sequence_number` 最高的副本将升级为主要副本。 

例如，假设一个可用性组具有三个同步副本：一个主要副本和两个同步提交次要副本。

- `REQUIRED_COPIES_TO_COMMIT` 为 3 / 2 = 1

- 响应预升级操作所需的副本数为 3 - 1 = 2。 因此需准备 2 个副本来触发故障转移。 这意味着，主要副本服务中断的情况下，如果其中一个次要副本无响应，仅另一个次要副本响应预升级操作，则资源代理无法确保进行响应的次要副本具有最高的 sequence_number，从而不会触发故障转移。

用户可选择替代默认行为，不采用上述设置，而将可用性组资源配置为不自动设置 `REQUIRED_COPIES_TO_COMMIT`。

>[!IMPORTANT]
>`REQUIRED_COPIES_TO_COMMIT` 为 0 时有数据丢失风险。 在主要副本中断的情况下，资源代理不会自动触发故障转移。 用户必须决定是等待主要副本恢复还是手动执行故障转移。

若要将 `REQUIRED_COPIES_TO_COMMIT` 设置为 0，请运行：

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

（SLES 上）使用 crm 的等效命令为：

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

若要还原为默认计算值，请运行：

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>更新资源属性会导致所有副本停止并重新启动。 这意味着主要副本会首先暂时降级为次要副本，然后再次进行升级，从而导致写入操作暂不可用。 REQUIRED_COPIES_TO_COMMIT 的新值仅在副本重新启动后进行设置，因此不会与运行 pcs 命令同时进行。

## <a name="balancing-high-availability-and-data-protection"></a>平衡高可用性和数据保护 

上述默认行为也适用于具有 2 个同步副本（主要副本 + 次要副本）的情况。 Pacemaker 默认 `REQUIRED_COPIES_TO_COMMIT = 1`，从而确保次要副本始终处于最新状态，实现最大程度的数据保护。  

>[!WARNING]
>由于次要副本发生计划内或计划外中断，该操作会增加主要副本不可用的风险。 用户可选择更改资源代理的默认行为，并将 `REQUIRED_COPIES_TO_COMMIT` 替换为 0：

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

替换后，资源代理将新设置用于 `REQUIRED_COPIES_TO_COMMIT`，并对其停止计算。 这意味着用户必须相应进行手动更新（例如，如果副本数增加）。

下表描述了在不同可用性组资源配置中，主要副本或次要副本发生中断时的后果：

### <a name="availability-group---2-sync-replicas"></a>可用性组 -2 个同步副本

| |主要副本中断 |一个次要副本中断
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|用户需要发出手动故障转移。 <br>可能导致数据丢失。<br> 新的主要副本是 R/W |主要副本为 R/W，运行可能导致数据丢失
|`REQUIRED_COPIES_TO_COMMIT=1` * |群集自动发出故障转移 <br>无数据丢失。 <br> 在先前的主要副本恢复并加入可用性组作为次要副本之前，新的主要副本将拒绝所有连接。 |次要副本恢复之前，主要副本将拒绝所有连接。

\* Pacemaker 的 SQL Server 资源代理默认行为。

### <a name="availability-group---3-sync-replicas"></a>可用性组 -3 个同步副本

| |主要副本中断 |一个次要副本中断
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|用户需要发出手动故障转移。 <br>可能导致数据丢失。 <br>新的主要副本是 R/W |主要副本是 R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |群集自动发出故障转移。 <br>无数据丢失。 <br>新的主要副本是 RW |主要副本是 R/W 

\* Pacemaker 的 SQL Server 资源代理默认行为。