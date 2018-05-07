---
title: SQL Server Always On 可用性组部署模式 |Microsoft 文档
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1f3b39f8c74c826a9844bb9198384056bf8614d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性组配置的高可用性和数据保护

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍了在 Linux 服务器上的 SQL Server Always On 可用性组的受支持的部署配置。 一个可用性组支持高可用性和数据保护。 自动故障检测、 自动故障转移和故障转移后的透明重新连接提供高可用性。 同步的副本提供数据保护。 

在 Windows Server 故障转移群集 (WSFC)，以实现高可用性的常见配置使用两个同步副本和第三个服务器或文件共享提供仲裁。 文件共享见证服务器验证可用性组配置的状态的同步和副本角色，例如。 此配置可确保辅助副本选择，因为故障转移目标具有的最新数据和可用性组配置更改。 

WSFC 同步可用性组副本和文件共享见证服务器之间的故障转移仲裁配置元的数据。 当可用性组不是在 WSFC 上时，SQL Server 实例的 master 数据库中存储配置元数据。

例如上的 Linux 群集的可用性组具有`CLUSTER_TYPE = EXTERNAL`。 没有任何 WSFC 仲裁故障转移。 在这种情况下配置元数据是管理和维护的 SQL Server 实例。 因为在此群集中没有见证服务器，需要第三个 SQL Server 实例来存储配置状态元数据。 所有三个 SQL Server 实例共同的群集提供分布式元数据存储。 

群集管理器可以查询可用性组中的 SQL Server 实例，并安排故障转移来维护高可用性。 在 Linux 群集中，Pacemaker 是群集管理器。 

SQL Server 自 2017 年 CU 1 使具有的可用性组的高可用性`CLUSTER_TYPE = EXTERNAL`为两个同步副本配置的唯一副本。 可以在任何版本的 SQL Server 自 2017 年 CU1 或更高版本-承载配置唯一的副本，包括 SQL Server Express 版本。 配置唯一的副本会维护有关 master 数据库中的可用性组的配置信息，但不包含可用性组中的用户数据库。 

## <a name="how-the-configuration-affects-default-resource-settings"></a>配置如何影响默认资源设置

SQL Server 2017 引入了`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`群集资源设置。 此设置可指定的数量的辅助副本写入保证要登录，之后才能提交主副本的每个事务的事务数据。 当你使用的外部群集管理器时，此设置将影响高可用性和数据保护。 设置的默认值在创建群集资源时根据的体系结构。 当你安装 SQL Server 资源代理- `mssql-server-ha` -并创建可用性组的群集资源，群集管理器检测到可用性组配置并设置`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`相应地。 

如果支持的配置，资源代理参数`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`设置为提供高可用性和数据保护的值。 有关详细信息，请参阅[pacemaker 了解 SQL Server 资源代理](#pacemakerNotify)。

以下各节介绍群集资源的默认行为。 

选择可用性组设计，以满足高可用性、 数据保护和读取缩放的特定业务要求。

以下配置描述了可用性组设计模式和每个模式的功能。 这些设计模式适用于可用性组用于`CLUSTER_TYPE = EXTERNAL`高可用性解决方案。 

- **三个同步副本**
- **两个同步副本**
- **两个同步副本和配置唯一的副本**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三个同步副本

此配置包含三个同步副本。 默认情况下，它提供高可用性和数据保护。 它还可以为读取缩放。

![三个副本][3]

读取缩放、 高可用性和数据保护，可以提供具有三个同步副本的可用性组。 下表描述可用性行为。 

| |读取扩展|高可用性 （& a) </br> 数据保护 | 数据保护
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|主要副本中断 | 手动故障转移。 可能导致数据丢失。 新的主是 R / 瓦 |自动故障转移。 新的主是 R / 瓦 |自动故障转移。 前面的主要恢复和联接可用性组作为辅助之前，新的主才可供用户事务。 
|一个次要副本中断  | 主是 R / 瓦 如果主没有自动故障转移将失败。 |主是 R / 瓦 如果主没有自动故障转移也会失败。 | 主也无法供用户事务。 
<sup>*</sup> 默认值

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>两个同步副本

此配置，实现数据保护。 如其他可用性组配置，它可以启用读取缩放。 两个同步副本配置不提供自动高可用性。 

![两个同步副本][1]

具有两个同步副本的可用性组提供读取缩放和数据保护。 下表描述可用性行为。 

| |读取扩展 |数据保护
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|主要副本中断 | 手动故障转移。 可能导致数据丢失。 新的主是 R / 瓦| 自动故障转移。 前面的主要恢复和联接可用性组作为辅助之前，新的主才可供用户事务。
|一个次要副本中断  |主是 R/W，运行公开数据丢失。 |主辅助恢复之前不可用的用户事务。
<sup>*</sup> 默认值

>[!NOTE]
>前面的方案是在 SQL Server 自 2017 年 CU 1 之前的行为。 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>两个同步副本和配置唯一的副本

具有两个 （或多个） 的同步副本和配置唯一的副本的可用性组提供数据保护，并可能还提供高可用性。 下图表示此体系结构：

![配置唯一的可用性组][2]

1. 同步用户数据复制到辅助副本。 它还包括可用性组配置元数据。
2. 可用性组配置元数据的同步复制。 它不包括用户数据。

在可用性组图中，主副本将配置数据推送到辅助副本并配置唯一的副本。 辅助副本还会收到用户数据。 配置唯一的副本未收到用户数据。 辅助副本处于同步的可用性模式。 配置唯一的副本不包含可用性组-仅有关可用性组的元数据中的数据库。 配置唯一的副本上的配置数据是以同步方式提交。

>[!NOTE]
>与配置仅副本 availabilility 组是用于 SQL Server 自 2017 年 CU1 的新功能。 可用性组中的 SQL Server 的所有实例必须都是 SQL Server 自 2017 年 CU1 或更高版本。 

默认值为`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`为 0。 下表描述可用性行为。 

| |高可用性 （& a) </br> 数据保护 | 数据保护
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|主要副本中断 | 自动故障转移。 新的主是 R / 瓦 | 自动故障转移。 新的主数据库不可用的用户事务。 
|辅助副本中断 | 主数据库处于 R/W，运行已公开到数据丢失 （如果主失败并且无法恢复）。 如果主没有自动故障转移也会失败。 | 主也无法供用户事务。 如果主故障转移到没有副本也会失败。 
|配置仅副本中断 | 主是 R / 瓦 如果主没有自动故障转移也会失败。 | 主是 R / 瓦 如果主没有自动故障转移也会失败。 
|同步辅助 + 配置仅副本中断| 主也无法供用户事务。 自动故障转移。 | 主也无法供用户事务。 故障转移到如果没有副本以及主服务器失败。 
<sup>*</sup> 默认值

>[!NOTE]
>承载配置唯一的副本的 SQL Server 的实例还可以托管其他数据库。 此外可以参与作为多个可用性组的配置数据库。 

## <a name="requirements"></a>需求

* 可用性组中的配置仅副本的所有副本都必须都是 SQL Server 自 2017 年 CU 1 或更高版本。
* 任何版本的 SQL Server 可以承载配置仅副本，包括 SQL Server Express。 
* 可用性组都需要至少一个辅助副本-除了主副本。
* 配置仅副本不会计入每个 SQL Server 实例的副本最大数目。 SQL Server 标准版允许最多三个副本，SQL Server 企业版则允许最多 9。

## <a name="considerations"></a>注意事项

* 不能超过一个配置每个可用性组的唯一副本。 
* 配置唯一的副本不能为主副本。
* 无法修改配置唯一的副本的可用性模式。 若要从配置的唯一副本更改为同步或异步辅助副本，删除配置唯一的副本，并添加所需的可用性模式的辅助副本。 
* 配置的唯一副本是同步的与可用性组元数据。 没有用户数据。 
* 具有一个主副本和一个配置时，唯一的副本，但没有辅助副本的可用性组不是有效的。 
* SQL Server Express edition 实例上，无法创建可用性组。 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 Pacemaker 的 SQL Server 资源代理

SQL Server 自 2017 年 1 CTP 1.4 添加`sequence_number`到`sys.availability_groups`以允许 Pacemaker 来确定如何最新的辅助副本均与主副本。 `sequence_number` 是单调递增 BIGINT 的表示方式保持最新的本地可用性组副本。 Pacemaker 更新`sequence_number`与每个可用性组配置更改。 配置更改的示例包括故障转移、 副本添加或删除。 对主要主机和更新数，则将其复制到辅助副本。 因此具有最新配置的辅助副本具有相同的序列号的主数据库。 

当 Pacemaker 决定将提升为主副本时，它首先会发送*预提升*到所有副本的通知。 副本返回的序列号。 接下来，当 Pacemaker 实际尝试将提升为主副本，副本仅提升本身如果其序列号为最高的所有序列号。 如果其自己的序列号与最高序列号不匹配，副本会拒绝升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。 

此过程需要适用于具有相同的序列号的以前的主数据库的升级可用的至少一个副本。 Pacemaker 资源代理集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`以便至少一个同步的辅助副本处于最新而且可用将要默认情况下自动进行故障转移的目标。 每个监视的操作的值与`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`是计算 （和更新如有必要）。 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`值除以 2 的同步副本数。 在故障转移时，资源代理需要 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`副本) 响应预升级通知。 具有最高的副本`sequence_number`提升为主。 

例如，具有三个同步副本的一个主副本和两个同步辅助副本的可用性组。

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 为 1;(3 / 2-> 1)。

- 所需的响应来预升级操作的副本数为 2;(3-1 = 2)。 

在此方案中，两个副本必须等待故障转移触发作出响应。 主副本中断后的成功自动故障转移，这两个辅助副本需要最新和响应预升级通知。 如果它们已联机并且同步，则它们具有相同的序列号。 可用性组提升其中之一。 如果只有一个辅助副本响应预升级操作，资源代理不能保证响应辅助副本具有最高 sequence_number，因此，故障转移，则不触发。

>[!IMPORTANT]
>`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 为 0 时有数据丢失风险。 期间的主副本中断，资源代理不会自动触发故障转移。 您可以等待主若要恢复，或者手动故障转移使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

你可以选择重写默认行为，并防止设置可用性组资源`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`自动。

以下脚本集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`可用性组上的 0 到名为`<**ag1**>`。 运行前，将 `<**ag1**>` 替换为可用性组的名称。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要还原到基于运行的可用性组配置的默认值：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>运行前面的命令时，主暂时降级到了辅助站点，然后再次提升。 资源更新将导致停止并重新启动的所有副本。 新值`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`副本重新启动后，不即时的方式，才会设置。

## <a name="see-also"></a>另请参阅

[在 Linux 上的可用性组](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
