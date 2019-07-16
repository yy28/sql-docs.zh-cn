---
title: SQL Server Always On 可用性组的部署模式
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 637d67767e17344d63498f8cb6a141fa78b11ecb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996426"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性组配置的高可用性和数据保护

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍在 Linux 服务器上的 SQL Server Always On 可用性组的受支持的部署配置。 一个可用性组支持高可用性和数据保护。 自动故障检测、 自动故障转移和故障转移后的透明重新连接提供高可用性。 已同步的副本提供数据保护。 

在 Windows Server 故障转移群集 (WSFC)，以实现高可用性的常见配置使用两个同步副本和第三个服务器或文件共享提供仲裁。 文件共享见证例如验证可用性组配置的同步的状态和副本的角色。 此配置可确保辅助副本选择作为故障转移目标具有的最新的数据和可用性组配置更改。 

WSFC 中同步故障转移可用性组副本和文件共享见证服务器之间的仲裁配置元的数据。 如果某一可用性组不在 WSFC 上，SQL Server 实例的 master 数据库中存储配置元数据。

例如，Linux 群集上的可用性组具有`CLUSTER_TYPE = EXTERNAL`。 没有任何 WSFC 仲裁故障转移。 在这种情况下配置元数据是管理和维护通过 SQL Server 实例。 由于在此群集中没有见证服务器，因此第三个 SQL Server 实例需要存储配置状态的元数据。 所有三个 SQL Server 实例一起为群集提供分布式元数据存储。 

群集管理器可以查询的 SQL Server 实例，该可用性组，并协调故障转移来维持高可用性。 在 Linux 群集中，Pacemaker 是群集管理器。 

SQL Server 2017 CU 1 启用高可用性的可用性组`CLUSTER_TYPE = EXTERNAL`加两个同步副本上仅配置副本。 可以在任何版本的 SQL Server 2017 CU1 或更高版本-上承载仅配置副本，包括 SQL Server Express edition。 仅配置副本维护有关 master 数据库中的可用性组的配置信息，但不包含可用性组中的用户数据库。 

## <a name="how-the-configuration-affects-default-resource-settings"></a>配置如何影响默认资源设置

SQL Server 2017 引入了`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`群集资源设置。 此设置可确保指定的数目的辅助副本写入记录之前提交主副本的每个事务的事务数据。 当您使用外部群集管理器时，此设置影响的高可用性和数据保护。 在创建群集资源依赖于体系结构中设置的默认值。 当你安装 SQL Server 资源代理- `mssql-server-ha` -并创建可用性组的群集资源，群集管理器检测到可用性组配置和设置`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`相应地。 

如果支持的配置，则资源代理参数`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`设置为提供高可用性和数据保护的值。 有关详细信息，请参阅[pacemaker 的了解 SQL Server 资源代理](#pacemakerNotify)。

以下部分介绍群集资源的默认的行为。 

选择以满足特定业务要求的高可用性、 数据保护和读取缩放可用性组设计。

以下配置介绍了可用性组设计模式，以及每个模式的功能。 这些设计模式适用于可用性组与`CLUSTER_TYPE = EXTERNAL`的高可用性解决方案。 

- **三个同步副本**
- **两个同步副本**
- **两个同步副本和仅配置副本**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三个同步副本

此配置包含三个同步副本。 默认情况下，它提供高可用性和数据保护。 它还可以提供读取缩放。

![三个副本][3]

读取缩放、 高可用性和数据保护，可以提供具有三个同步副本的可用性组。 下表介绍可用性行为。 

| |读取缩放|高可用性 （& a) </br> 数据保护 | 数据保护|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|主要副本中断 |自动故障转移。 新的主副本是 R / w。 |自动故障转移。 新的主副本是 R / w。 |自动故障转移。 新的主数据库不可用的用户事务，直到在先前的主要副本恢复并加入可用性组作为辅助。 |
|一个次要副本中断  | 主要是 R / w。 如果主没有自动故障转移会失败。 |主要是 R / w。 如果主没有自动故障转移也会失败。 | 主数据库不可用的用户事务。 |

<sup>\*</sup> 默认值

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>两个同步副本

此配置使数据保护。 像其他可用性组配置，它可以实现读取缩放。 两个同步副本配置不提供自动高可用性。 两个副本配置为仅适用于 SQL Server 2017 RTM 和更高版本不再支持使用 (CU1 及更高版本) 的 SQL Server 2017 版本...

![两个同步副本][1]

具有两个同步副本的可用性组提供读取缩放和数据保护。 下表介绍可用性行为。 

| |读取缩放 |数据保护|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要副本中断 | 手动故障转移。 可能导致数据丢失。 新的主副本是 R / w。| 自动故障转移。 新的主数据库不可用的用户事务，直到在先前的主要副本恢复并加入可用性组作为辅助。|
|一个次要副本中断  |主要是 R/W，运行可能导致数据丢失。 |主次要副本恢复之前不可用的用户事务。|

<sup>\*</sup> 默认值

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>两个同步副本和仅配置副本

具有两个 （或多个） 的同步副本和仅配置副本的可用性组提供数据保护，而且还可能提供高可用性。 下图显示此体系结构：

![配置唯一的可用性组][2]

1. 同步用户数据复制到辅助副本。 它还包括可用性组配置元数据。
2. 同步的可用性组配置元数据的复制。 它不包括用户数据。

在可用性组图中，主副本将配置数据推送到辅助副本和仅配置副本。 辅助副本还会收到用户数据。 仅配置副本不会接收用户数据。 辅助副本处于同步可用性模式。 仅配置副本不包含可用性组-仅有关可用性组的元数据中的数据库。 仅配置副本上的配置数据是以同步方式提交。

> [!NOTE]
> 仅配置副本的 availabilility 组是用于 SQL Server 2017 CU1 的新功能。 SQL Server 可用性组中的所有实例必须都是 SQL Server 2017 CU1 或更高版本。 

默认值为`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`为 0。 下表介绍可用性行为。 

| |高可用性 （& a) </br> 数据保护 | 数据保护|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要副本中断 | 自动故障转移。 新的主副本是 R / w。 | 自动故障转移。 新的主数据库不可用的用户事务。 |
|次要副本中断 | 主要副本是 R/W，运行可能导致数据丢失 （如果主数据库将失败并且无法恢复）。 如果主没有自动故障转移也会失败。 | 主数据库不可用的用户事务。 如果主故障转移到没有副本也会失败。 |
|配置仅副本中断 | 主要是 R / w。 如果主没有自动故障转移也会失败。 | 主要是 R / w。 如果主没有自动故障转移也会失败。 |
|同步辅助 + 配置仅副本中断| 主数据库不可用的用户事务。 无自动故障转移。 | 主数据库不可用的用户事务。 故障转移到如果没有副本以及主服务器失败。 |

<sup>\*</sup> 默认值

> [!NOTE]
> 承载仅配置副本的 SQL Server 的实例还可以托管其他数据库。 它还可加入作为多个可用性组的配置数据库。 

## <a name="requirements"></a>要求

- 可用性组中包含仅配置副本的所有副本都必须都是 SQL Server 2017 CU 1 或更高版本。
- 任何版本的 SQL Server 可以托管仅配置副本，包括 SQL Server Express。 
- 可用性组需要至少一个辅助副本-除了主副本。
- 仅配置副本不会计入每个 SQL Server 实例的副本的最大数目。 SQL Server 标准版，最多三个副本，SQL Server Enterprise Edition 支持最多 9。

## <a name="considerations"></a>注意事项

- 不能超过一个配置每个可用性组的唯一副本。 
- 仅配置副本不能为主要副本。
- 不能修改仅配置副本的可用性模式。 若要从仅配置副本更改为同步或异步辅助副本，删除仅配置副本，并添加所需的可用性模式的辅助副本。 
- 仅配置副本是同步的与可用性组元数据。 没有任何用户数据。 
- 具有一个主副本和一个配置唯一的副本，但没有任何辅助副本的可用性组不是有效的。 
- 您不能在 SQL Server Express 版本的实例上创建可用性组。 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 Pacemaker 的 SQL Server 资源代理

添加 SQL Server 2017 CTP 1.4`sequence_number`到`sys.availability_groups`以便 Pacemaker 来标识如何保持最新的辅助副本均与主副本。 `sequence_number` 是一个单调递增的 BIGINT，表示如何保持最新的本地可用性组副本。 Pacemaker 更新`sequence_number`每个可用性组的配置更改。 配置更改的示例包括故障转移、 副本添加或删除。 更新到主副本，该数字，然后将其复制到辅助副本。 因此具有最新配置的辅助副本具有与主数据库相同的序列号。 

当 Pacemaker 决定将升级为主要副本时，它首先会发送*预升级*到所有副本的通知。 副本返回的序列号。 接下来，当 Pacemaker 实际尝试将某个副本升级为主要副本，副本仅升级自身，如果其序列号最高的所有序列号。 如果其自己的序列号与最高序列号不匹配，该副本将拒绝此升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。 

此过程要求使用相同的序列号与以前的主升级可用的至少一个副本。 Pacemaker 资源代理集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`，以便在至少一个同步次要副本是最新程序并且可用于在默认情况下自动故障转移目标。 对于每个监视的操作的值`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`进行计算 （进行更新，如有必要）。 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`值是同步副本数除以 2。 在故障转移时，资源代理需要 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`副本) 响应预升级通知。 具有最高的副本`sequence_number`升级为主要。 

例如，具有三个同步副本： 一个主副本和两个同步辅助副本的可用性组。

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 为 1;(3 / 2-> 1)。

- 所需的数量的副本响应预升级操作为 2;(3-1 = 2)。 

在此方案中，两个副本必须响应的触发故障转移。 主要副本中断后的成功自动故障转移，这两个辅助副本需要最新状态和响应预升级通知。 如果它们处于联机状态且同步，它们具有相同的序列号。 可用性组升级其中之一。 如果只有一个辅助副本响应预升级操作，则资源代理不能确保的辅助数据库的响应具有最高的 sequence_number，和不触发故障转移。

> [!IMPORTANT]
> `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 为 0 时有数据丢失风险。 主副本在中断期间，资源代理不会自动触发故障转移。 可以等待主要副本恢复，也可以手动故障转移使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

可以选择重写默认行为，并防止可用性组资源设置`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`自动。

下面的脚本集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`对可用性组的 0 到名为`<**ag1**>`。 运行前，将 `<**ag1**>` 替换为可用性组的名称。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要还原为默认值，基于运行的可用性组配置：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> 运行上述命令时，主要是暂时降级为次要副本，然后再次进行升级。 资源更新将导致所有副本停止并重新启动。 新值`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`仅在副本重新启动，不在瞬间完成后设置。

## <a name="see-also"></a>请参阅

[Linux 上的可用性组](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
