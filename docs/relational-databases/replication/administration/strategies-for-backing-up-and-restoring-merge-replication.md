---
title: 备份和还原策略（合并）
description: 介绍合并复制中使用的数据备份和还原策略。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e61dd8343e95ca5b5322235fb431f3dc5a5624cc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900825"
---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>合并复制的备份和还原策略
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  对于合并复制，请定期备份下列数据库：  
  
-   发布服务器上的发布数据库  
  
-   分发服务器上的分发数据库  
  
-   各个订阅服务器上的订阅数据库  
  
-   发布服务器、分发服务器和所有订阅服务器上的 **master** 和 **msdb** 系统数据库。 当备份这些数据库中的一个数据库或相关的复制数据库时，应同时备份这些数据库。 例如，应在备份发布数据库的同时备份发布服务器上的 **master** 和 **msdb** 数据库。 如果还原发布数据库，请确保 **master** 和 **msdb** 数据库在复制配置和设置方面与发布数据库保持一致。  
  
 如果执行定期日志备份，则在日志备份中应捕获所有与复制相关的更改。 如果不执行日志备份，则当与复制相关的设置发生更改时，应执行备份。 有关详细信息，请参阅 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)。  
  
 选择以下一种方法来备份和还原发布数据库，然后遵循针对分发数据库和订阅数据库列出的建议。  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>备份和还原发布数据库  
 有两种方法可以还原合并发布数据库。 从备份中还原发布数据库后，应进行以下两项操作之一：  
  
-   使发布数据库和订阅数据库同步。  
  
-   重新初始化对发布数据库中发布的所有订阅。  
  
 使用这两种方法中的任何一种都可确保发布服务器和所有订阅服务器在执行还原后同步。  
  
> [!NOTE]  
>  如果某些表包含标识列，则必须确保还原后分配正确的标识范围。 有关详细信息，请参阅[复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
### <a name="synchronizing-the-publication-database"></a>同步发布数据库  
 使发布数据库与订阅数据库同步使用户可从一个或多个订阅数据库中上载先前在发布数据库中所做的但未在还原备份中实现的更改。 可以上载的数据取决于筛选发布的方法：  
  
-   如果发布未经筛选，则应能通过与最新订阅服务器同步来更新发布数据库。  
  
-   如果发布经过筛选，则可能无法更新发布数据库。 假设有一个按如下方式分区的表：每个订阅仅收到一个区域（北部、东部、南部和西部）的客户数据。 如果每个数据分区至少有一个订阅服务器，那么使每个分区与订阅服务器同步会更新发布数据库。 但是，以西分区为例，如果其中的数据未复制到任何订阅服务器，那么发布服务器上的此数据就无法更新。  
  
> [!IMPORTANT]  
>  使发布数据库与订阅数据库同步可使已发布的表还原到一个时间点，该时间点比从备份还原的其他未发布表的时间点更近。  
  
 如果与运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本的订阅服务器同步，则订阅无法匿名；它必须是客户端订阅或服务器订阅（在早期版本中称为本地订阅和全局订阅）。  
  
 若要同步订阅，请参阅 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
### <a name="reinitializing-all-subscriptions"></a>重新初始化所有订阅  
 重新初始化所有订阅可确保所有订阅服务器都处于与已还原发布数据库一致的状态。 若要将完整的拓扑返回到给定发布数据库备份表示的先前状态，应使用此方法。 例如，如果作为从错误执行的批处理操作中还原的一种机制将发布数据库还原到某个较早的时间点，就可能需要重新初始化所有订阅。  
  
 如果选择此选项，请生成一个新的快照，用以在还原发布数据库后立即向重新初始化的订阅服务器传递。  
  
 若要重新初始化订阅，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-a-subscription.md)。  
  
 若要创建并应用快照，请参阅 [创建并应用初始快照](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) 和 [为包含参数化筛选器的合并发布创建快照](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>备份和还原分发数据库  
 对于合并复制，应定期备份分发数据库，而且，只要所用备份的时间不超过使用分发服务器的所有发布的最短保持期，则无须考虑任何特殊事项即可还原分发数据库。 例如，如果三个发布的保持期分别为 10 天、20 天和 30 天，则用于还原数据库的备份的保持时间不应超过 10 天。 分发数据库在合并复制中的作用有限：它不存储更改跟踪中使用的任何数据，也不对将要转发到订阅数据库的合并复制更改提供临时存储（而事务复制中提供）。  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>备份和还原订阅数据库  
 为了确保成功恢复订阅数据库，订阅服务器应在备份订阅数据库前与发布服务器同步；还原订阅数据库后它们还要进行同步：  
  
-   备份订阅数据库前与发布服务器同步有助于确保在从备份中还原订阅服务器的情况下，订阅可以仍处于发布保持期内。 例如，请假设有一个保持期为 10 天的发布。 上次同步是在 8 天前，现在执行备份。 如果 4 天后还原备份，那么上次同步就已经是 12 天前的事了，这已经过了保持期。 这种情况下，必须重新初始化订阅服务器。 如果订阅服务器在备份之前进行了同步，则订阅数据库将在保持期之内。  
  
     该备份的保持时间应不超过订阅服务器订阅的所有发布的保持期的最小值。 例如，如果订阅服务器订阅了三个保持期分别为 10 天、20 天和 30 天的发布，则用于还原数据库的备份的保持时间不应超过 10 天。  
  
-   还原后使订阅数据库与其每个发布同步可确保订阅服务器与发布服务器上的所有更改同步更新。  
  
 若要设置发布保持期，请参阅[设置订阅的过期期限](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)。  
  
 若要同步订阅，请参阅 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>备份和还原重新发布的数据库  
 如果某个数据库从发布服务器订阅数据，并依次将同样的数据发布给其他订阅数据库，则称该数据库为重新发布数据库。 还原重新发布数据库时，请遵从此主题中“备份和还原发布数据库”和“备份和还原订阅数据库”两节所介绍的准则。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据库的备份和还原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [备份和还原复制的数据库](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
