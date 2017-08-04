---
title: "SQL Server Always On 可用性组部署模式 |Microsoft 文档"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e2d26fd9ce79fc8c47c7499313648d565ae1b97
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---

# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性组配置的高可用性和数据保护

本文介绍了在 Linux 服务器上的 SQL Server Always On 可用性组的受支持的部署配置。 一个可用性组支持高可用性和数据保护。 自动故障检测、 自动故障转移和故障转移后的透明重新连接提供高可用性。 同步的副本提供数据保护。 

>[!NOTE]
>除了高可用性和数据保护，可用性组可以提供灾难恢复、 跨平台迁移和读取横向扩展。 本文主要讨论了实现高可用性和数据保护。 

使用 Windows Server 故障转移群集，常见的配置高可用性使用两个同步副本和[文件共享见证服务器](http://technet.microsoft.com/library/cc731739.aspx)。 文件共享见证服务器验证可用性组配置的状态的同步和副本角色，例如。 此配置可确保辅助副本选择，因为故障转移目标具有的最新数据和可用性组配置更改。 

适用于 Linux 当前的高可用性解决方案不适应外部的见证服务器，如 Windows Server 故障转移群集中的文件共享见证服务器。 当没有 Windows Server 故障转移群集时，参与的 SQL Server 实例上的 master 数据库中存储的可用性组配置。 因此，该可用性组实现高可用性和数据保护要求至少三个同步副本。 在 Linux 服务器上创建可用性组后，创建群集资源。 群集资源设置确定以实现高可用性配置。

选择可用性组设计，以满足特定业务要求，以实现高可用性，数据保护，并读取横向扩展。

>[!IMPORTANT]
>以下配置描述了可用性组设计模式和每个模式的功能。 这些设计模式适用于可用性组用于`CLUSTER_TYPE = EXTERNAL`高可用性解决方案。 

设计模式是两个可用性组配置。 配置包括：

- **三个同步副本**

- **两个同步副本**

## <a name="how-the-configuration-affects-default-resource-settings"></a>配置如何影响默认资源设置

群集资源设置`required_synchronized_secondaries_to_commit`可保证在提交事务在主副本上的之前每个事务写入到最小辅助副本日志数。 高可用性和数据保护，具体取决于配置，则可能会影响此设置。 当你安装 SQL Server 资源代理- `mssql-server-ha` -并创建可用性组的群集资源，群集管理器检测到可用性组配置并设置`required_synchronized_secondaries_to_commit`相应地。 

如果支持的配置，资源代理参数`required_synchronized_secondaries_to_commit`设置为提供高可用性和数据保护的值。 有关详细信息，请参阅[pacemaker 了解 SQL Server 资源代理](#pacemakerNotify)。

以下各节介绍群集资源的默认行为。 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三个同步副本

此配置包含三个同步副本。 默认情况下，它提供高可用性和数据保护。 它还可以为读取的横向扩展。

![三个副本][3]

下表介绍基于具有三个同步副本的可用性组的设置的高可用性和数据保护行为： 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|自动故障转移后主副本中断| |✔| 
|一个辅助副本中断后可用的主副本|✔|✔| 
|两个辅助副本停机后可用的主副本|✔| |
|主副本中断-可能造成数据丢失后的手动故障转移|✔| | 

\*默认设置可用性组添加为群集中的资源时。

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>两个同步副本

此配置，实现数据保护。 如其他可用性组配置，它可以启用读取的横向扩展。 两个同步副本配置不提供自动高可用性。 

![两个同步副本][1]

此配置需要两台服务器。 这些服务器充当主副本和辅助副本的角色。 

两个同步副本配置进行了优化的数据保护和分发数据库的读取工作负载。 默认情况下，该资源的数据保护配置。 此配置不提供高可用性，因为如果 SQL Server 的任一实例失败，数据库完全不可用或没有数据丢失的风险。 

下表介绍根据具有两个同步副本的可用性组的可能值的数据保护行为： 

|`required_synchronized_secondaries_to_commit`|0 \*|1 
| --- |:---|:---
|自动故障转移后主副本中断| |✔ \*\* | 
|辅助副本中断后可用的主副本|✔| |

\*默认设置可用性组添加为群集中的资源时。

\*\*在此配置中，主副本中断发生可用性组自动后进行故障转移。 应用程序无法连接到可用性组主副本之前重新打开行-现在作为辅助副本。 

两个同步副本配置可能是最经济，因为它只要求 SQL Server 的两台服务器上的两个实例。

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 Pacemaker 的 SQL Server 资源代理

SQL Server 自 2017 年 1 CTP 1.4 添加`sequence_number`到`sys.availability_groups`以允许 Pacemaker 来确定如何最新的辅助副本均与主副本。 `sequence_number`是单调递增 BIGINT 的表示方式保持最新的本地可用性组副本。 Pacemaker 更新`sequence_number`与每个可用性组配置更改。 配置更改的示例包括故障转移、 副本添加或删除。 对主要主机和更新数，则将其复制到辅助副本。 因此具有最新配置的辅助副本具有相同的序列号的主数据库。 

当 Pacemaker 决定将提升为主副本时，它首先会发送*预提升*到所有副本的通知。 副本返回的序列号。 接下来，当 Pacemaker 实际尝试将提升为主副本，副本仅提升本身如果其序列号为最高的所有序列号。 如果其自己的序列号与最高序列号不匹配，副本会拒绝升级操作。 这样，就只有序列号最高的副本才会升级为主副本，确保不会丢失数据。 

此过程需要适用于具有相同的序列号的以前的主数据库的升级可用的至少一个副本。 Pacemaker 资源代理集`required_synchronized_secondaries_to_commit`以便至少一个同步的辅助副本处于最新而且可用将要默认情况下自动进行故障转移的目标。 每个监视的操作的值与`required_synchronized_secondaries_to_commit`是计算 （和更新如有必要）。 `required_synchronized_secondaries_to_commit`值除以 2 的同步副本数。 在故障转移时，资源代理需要 (`total number of replicas`  -  `required_synchronized_secondaries_to_commit`副本) 响应预升级通知。 具有最高的副本`sequence_number`提升为主。 

例如，具有三个同步副本的一个主副本和两个同步辅助副本的可用性组。

- `required_synchronized_secondaries_to_commit`为 1;(3 / 2-> 1)。

- 所需的响应来预升级操作的副本数为 2;(3-1 = 2)。 

在此方案中，两个副本必须等待故障转移触发作出响应。 主副本中断后的成功自动故障转移，这两个辅助副本需要最新和响应预升级通知。 如果它们已联机并且同步，则它们具有相同的序列号。 可用性组提升其中之一。 如果只有一个辅助副本响应预升级操作，资源代理不能保证响应辅助副本具有最高 sequence_number，因此，故障转移，则不触发。

>[!IMPORTANT]
>当`required_synchronized_secondaries_to_commit`是 0 没有数据丢失的风险。 期间的主副本中断，资源代理不会自动触发故障转移。 您可以等待主若要恢复，或者手动故障转移使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

你可以选择重写默认行为，并防止设置可用性组资源`required_synchronized_secondaries_to_commit`自动。

以下脚本集`required_synchronized_secondaries_to_commit`可用性组上的 0 到名为`<**ag1**>`。 在运行替换之前`<**ag1**>`替换为你的可用性组的名称。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要还原到基于运行的可用性组配置的默认值：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>运行前面的命令时，主暂时降级到了辅助站点，然后再次提升。 资源更新将导致停止并重新启动的所有副本。 新值`required_synchronized_secondaries_to_commit`副本重新启动后，不即时的方式，才会设置。

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
