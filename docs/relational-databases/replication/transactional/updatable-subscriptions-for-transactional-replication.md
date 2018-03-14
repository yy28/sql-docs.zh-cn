---
title: "事务复制的可更新订阅 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c4922de0c287e5263163f56d151455fea9a836f9
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="updatable-subscriptions---for-transactional-replication"></a>事务复制的可更新订阅
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  此功能在从 2012 到 2016 的 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 版本中仍然受支持。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 事务复制支持在订阅服务器中通过可更新订阅和对等复制来进行更新。 下面介绍两种可更新订阅：  
  
-   立即更新。 必须连接发布服务器和订阅服务器才能在订阅服务器中更新数据。  
  
-   排队更新。不必连接发布服务器和订阅服务器即可在订阅服务器中更新数据。 可以在订阅服务器或发布服务器脱机时进行更新。  
  
 在订阅服务器中更新数据时，首先将数据传播到发布服务器，然后再传播到其他订阅服务器。 如果使用立即更新，将使用两阶段提交协议立即传播更改。 如果使用排队更新，更改将存储在队列中；当网络连接可用时，再在发布服务器中异步应用排队事务。 由于更新异步传播至发布服务器，所以发布服务器或另一台订阅服务器有可能更新同一数据，而在应用更新时会发生冲突。 将根据创建发布时设置的冲突解决策略检测和解决冲突。  
  
 如果在新建发布向导中创建具有可更新订阅的事务发布，将同时启用立即更新和排队更新。 如果使用存储过程创建发布，则可以启用一个或两个选项。 创建发布的订阅时，可以指定要使用的更新模式。 如有必要，以后可以在两种更新模式之间切换。 有关详细信息，请参阅下面的“在更新模式之间切换”部分。  
  
 若要启用事务发布的可更新订阅，请参阅 [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)。  
  
 若要创建事务发布的可更新订阅，请参阅[创建事务发布的可更新订阅 (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)。 
  
## <a name="switching-between-update-modes"></a>在更新模式之间切换  
 使用可更新订阅时，可以指定订阅使用一种更新模式，然后在应用程序需要时再切换到另一种更新模式。 例如，可以指定订阅使用立即更新，但如果因系统故障而导致网络连接断开，则切换到排队更新。  
  
> [!NOTE]  
>  复制不会自动切换更新模式。 必须通过 SQL Server Management Studio 设置更新模式，否则你的应用程序必须调用 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md) 来切换更新模式。  
  
 如果从立即更新切换到排队更新，只有在连接了订阅服务器和发布服务器，且队列读取器代理已将队列中所有挂起消息应用到发布服务器后，才能切换回立即更新。  
  
 **切换更新模式**  
  
 若要切换更新模式，必须为这两种更新模式都启用发布和订阅，然后再根据需要进行切换。 有关详细信息，请参阅  
[Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)。  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>使用可更新订阅的注意事项  
  
-   为更新订阅或排队更新订阅启用发布后，不能再为发布禁用该选项（即使订阅不需要使用它）。 若要禁用该选项，必须删除发布并创建一个新发布。  
  
-   不支持重新发布数据。  
  
-   出于跟踪的目的，复制将在已发布的表中添加 **msrepl_tran_version** 列。 由于添加的这个列，所有 **INSERT** 语句都应包括一个列列表。  
  
-   若要在支持更新订阅的发布中的表上进行架构更改，必须在发布服务器和订阅服务器中停止该表上的所有活动，还必须将挂起的数据更改传播到所有节点，然后才能进行架构更改。 这可以确保未完成的事务不会与挂起的架构更改发生冲突。 架构更改传播到所有节点后，可以在已发布的表上恢复活动。 有关详细信息，请参阅[停止复制拓扑（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
-   如果计划切换更新模式，则在初始化订阅后，队列读取器代理必须至少运行一次（默认情况下，队列读取器代理连续运行）。  
  
-   如果订阅服务器数据库进行了水平分区，且分区中有在订阅服务器上存在而在发布服务器中不存在的行，那么订阅服务器将无法更新这些预先存在的行。 试图更新这些行将返回错误。 应先从表中删除这些行，然后再在发布服务器中添加这些行。  

-   当使用了唯一的经筛选索引时，具有排队的可更新订阅服务器的事务复制可能会遭遇性能降低。 如果具有唯一的经筛选索引的项目上发生冲突，则解决冲突将导致在订阅服务器上额外针对唯一的经筛选索引未涵盖的行进行删除和插入。
  
### <a name="updates-at-the-subscriber"></a>订阅服务器中的更新  
  
-   即使订阅过期或处于不活动状态，订阅服务器中的更新仍会传播到发布服务器中。 请确保删除或重新初始化此类订阅。  
  
-   如果使用 **TIMESTAMP** 或 **IDENTITY** 列，且将这些列按其基本数据类型进行复制，则不应在订阅服务器中更新这些列中的值。  
  
-   订阅服务器不能更新或插入 **text**、 **ntext** 或 **image** 值，因为不能在复制更改跟踪触发器中从插入或删除的表中读取数据。 同样，订阅服务器不能使用 **WRITETEXT** 或 **UPDATETEXT** 更新或插入 **text** 或 **image** 值，因为这些数据会被发布服务器覆盖。 但可以将 **text** 和 **image** 列分区到单独的表中，并在一个事务中修改这两个表。  
  
     若要更新订阅服务器上的大型对象，请分别使用数据类型 **varchar(max)**、 **nvarchar(max)**、 **varbinary(max)** ，而不要使用 **text**、 **ntext**和 **image** 数据类型。  
  
-   不允许对唯一键（包括主键）进行生成重复项的更新（例如，格式为 `UPDATE <column> SET <column> =<column>+1` 的更新），这些更新将因为违反唯一性而被拒绝。 这是因为复制会将订阅服务器中所做的设置更新作为单独的 **UPDATE** 语句为每个受影响的行进行传播。  
  
-   如果订阅服务器数据库进行了水平分区，且分区中有在订阅服务器上存在而在发布服务器中不存在的行，那么订阅服务器将无法更新这些预先存在的行。 试图更新这些行将返回错误。 应当先从表中删除这些行，然后再插入这些行。  
  
### <a name="user-defined-triggers"></a>用户定义的触发器  
  
-   如果应用程序需要在订阅服务器中使用触发器，则应在发布服务器和订阅服务器中使用 `NOT FOR REPLICATION` 选项来定义触发器。 这可以确保触发器只在原始数据更改时激发，而在复制更改时不激发。  
  
     确保复制触发器更新表时不会激发用户定义的触发器。 这可以通过在用户定义的触发器的正文中调用 **sp_check_for_sync_trigger** 过程来实现。 有关详细信息，请参阅 [sp_check_for_sync_trigger &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md)。  
  
### <a name="immediate-updating"></a>立即更新  
  
-   对于立即更新订阅，订阅服务器中的更改是使用 Microsoft 分布式事务处理协调器 (MS DTC) 传播到订阅服务器上并进行应用的。 请确保发布服务器和订阅服务器中安装并配置了 MS DTC。 有关详细信息，请参阅 Windows 文档。  
  
-   立即更新订阅使用的触发器需要连接到发布服务器才能复制更改。  
  
-   如果发布允许立即更新订阅，且发布中的项目具有列筛选器，则无法筛选出无默认值的不可为 Null 的列。  
  
### <a name="queued-updating"></a>排队更新  
  
-   合并发布中包含的表也不能作为允许排队更新订阅的事务发布的一部分进行发布。  
  
-   使用排队更新时，建议不要对主键列进行更新，因为主键被用作所有查询的记录定位器。 当冲突解决策略设置为“订阅服务器入选”时，更新主键时应小心。 如果同时在发布服务器和订阅服务器中更新主键，将获得具有不同主键的两行。  
  
-   对于 **SQL_VARIANT**数据类型的列：在订阅服务器中插入或更新数据时，队列读取器代理在将数据从订阅服务器复制到队列时，将按下列方式映射数据：  
  
    -   将**BIGINT**, **DECIMAL**, **NUMERIC**, **MONEY**和 **SMALLMONEY** 映射到 **NUMERIC**。  
  
    -   将**BINARY** 和 **VARBINARY** 映射到 **VARBINARY** 数据。  
  
### <a name="conflict-detection-and-resolution"></a>冲突检测和解决  
  
-   对于“订阅服务器入选”冲突策略：不支持对主键列的更新应用冲突解决。  
  
-   复制并不会解决由于外键约束失败而引起的冲突。  
  
    -   如果出现意外冲突，而数据又分区良好（订阅服务器不更新相同的列），则可以在发布服务器和订阅服务器中使用外键约束。  
  
    -   如果出现预料中的冲突：如果使用“订阅服务器入选”冲突解决，则不应在发布服务器或订阅服务器中使用外键约束；如果使用“发布服务器入选”冲突解决，则不应在订阅服务器中使用外键约束。  
  
## <a name="see-also"></a>另请参阅  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [事务复制的发布类型](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [订阅发布](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
