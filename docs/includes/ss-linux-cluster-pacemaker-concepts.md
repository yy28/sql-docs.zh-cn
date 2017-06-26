## <a name="pacemakerNotify"></a>了解 Pacemaker 的 SQL Server 资源代理

在 CTP 1.4 版本中之前, 的 Pacemaker 资源代理的可用性组无法不知道是否副本标记为`SYNCHRONOUS_COMMIT`或不是真正最新。 该副本有可能已停止与主副本同步，但资源代理并不知道这种情况。 因此，代理可能会将过时的副本升级为主要副本 - 如果升级成功，将导致数据丢失。 

SQL Server 自 2017 年 1 CTP 1.4 添加`sequence_number`到`sys.availability_groups`若要解决此问题。 `sequence_number`是表示本地可用性组副本针对可用性组中的副本的其余部分的最新程度如何单调递增 BIGINT。 执行故障转移、添加或删除副本和其他可用性组操作会更新此数字。 该数字将在主要副本上更新，然后推送到次要副本。 因此，处于最新状态的次要副本的 sequence_number 与主要副本相同。 

当 Pacemaker 决定将某个副本升级为主要副本时，首先会向所有副本发送通知，以提取并存储序列号（我们将其称为预升级通知）。 接下来，当 Pacemaker 实际尝试将某个副本升级为主要副本时，如果该副本的序列号在所有副本的序列号中是最高的，则该副本只会升级自身，并拒绝其他升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。 

请注意，仅当至少有一个可用于升级的副本的序列号与以前的主副本相同时，才能保证这种结果。 若要确保这一点，Pacemaker 资源代理将自动设置的默认行为是`REQUIRED_COPIES_TO_COMMIT`，以便至少一个同步提交辅助副本是最新，并可用于自动故障转移的目标。 每个监视的操作的值与`REQUIRED_COPIES_TO_COMMIT`是计算 （和更新如有必要） 作为 (的同步提交副本数 / 2)。 然后，在故障转移时，资源代理将需要 (`total number of replicas`  -  `required_copies_to_commit`副本) 响应预升级通知才能进行提升为主其中之一。 具有最高的副本`sequence_number`将被提升到主副本。 

例如，假设一个可用性组具有三个同步副本：一个主要副本和两个同步提交次要副本。

- `REQUIRED_COPIES_TO_COMMIT`为 3 / 2 = 1

- 响应预升级操作所需的副本数为 3 - 1 = 2。 因此需准备 2 个副本来触发故障转移。 这意味着，主要副本服务中断的情况下，如果其中一个次要副本无响应，仅另一个次要副本响应预升级操作，则资源代理无法确保进行响应的次要副本具有最高的 sequence_number，从而不会触发故障转移。

用户可以选择重写默认行为，并配置可用性组资源，以不设置`REQUIRED_COPIES_TO_COMMIT`自动如上所述。

>[!IMPORTANT]
>当`REQUIRED_COPIES_TO_COMMIT`是 0 没有数据丢失的风险。 在主要副本中断的情况下，资源代理不会自动触发故障转移。 用户必须决定是等待主要副本恢复还是手动执行故障转移。

若要设置`REQUIRED_COPIES_TO_COMMIT`为 0，运行：

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

上述默认行为也适用于具有 2 个同步副本（主要副本 + 次要副本）的情况。 将默认 pacemaker`REQUIRED_COPIES_TO_COMMIT = 1`若要确保辅助副本始终是最新的最大的数据保护。  

>[!WARNING]
>由于次要副本发生计划内或计划外中断，该操作会增加主要副本不可用的风险。 用户可以选择更改资源代理的默认行为，并重写`REQUIRED_COPIES_TO_COMMIT`为 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

资源代理后重写，将使用的新设置`REQUIRED_COPIES_TO_COMMIT`和停止计算它。 这意味着用户必须相应进行手动更新（例如，如果副本数增加）。

下表描述了在不同可用性组资源配置中，主要副本或次要副本发生中断时的后果：

### <a name="availability-group---2-sync-replicas"></a>可用性组 -2 个同步副本

| |主要副本中断 |一个次要副本中断
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|用户需要发出手动故障转移。 <br>可能导致数据丢失。<br> 新的主要副本是 R/W |主要副本为 R/W，运行可能导致数据丢失
|`REQUIRED_COPIES_TO_COMMIT=1` * |群集自动发出故障转移 <br>无数据丢失。 <br> 新的主副本将拒绝所有连接，直到前面的主要恢复和联接可用性组作为辅助数据库。 |辅助恢复之前，主将拒绝所有连接。

\*SQL Server 资源代理对于 Pacemaker 默认行为。

### <a name="availability-group---3-sync-replicas"></a>可用性组 -3 个同步副本

| |主要副本中断 |一个次要副本中断
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|用户需要发出手动故障转移。 <br>可能导致数据丢失。 <br>新的主要副本是 R/W |主要副本是 R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |群集自动发出故障转移。 <br>无数据丢失。 <br>新的主要副本是 RW |主要副本是 R/W 

\*SQL Server 资源代理对于 Pacemaker 默认行为。