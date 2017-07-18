---
title: "排队更新冲突的检测和解决 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 666ad0200e8429c470772fc68110d14a7809d12a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/18/2017

---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>可更新订阅 - 排队更新冲突的解决
  由于排队更新订阅允许对多个位置上的相同数据进行修改，因此，在发布服务器中同步数据时可能会发生冲突。 复制在将更改与发布服务器同步时检测冲突，并使用在创建发布时所选择的解决策略来解决那些冲突。 可能会发生下列冲突：  
  
-   更新和插入冲突。 在两个位置更改相同的数据时会发生此冲突。 一个更改入选，而另一个更改落选。  
  
-   删除冲突。 当在一个位置删除某行而在另一个位置更改同一行时，则会发生此冲突。  
  
 冲突检测和解决可能是十分耗时并占用大量资源的过程，因此，减少应用程序中的冲突的最好方法是：创建数据分区以便不同的订阅服务器修改不同的数据子集。  
  
## <a name="detecting-conflicts"></a>检测冲突  
 创建发布并启用排队更新时，复制将向基础表添加一个带有默认值 **newid()** 的**uniqueidentifier**列 ( **msrepl_tran_version** )。 在发布服务器或订阅服务器中更改已发布的数据后，行将收到一个新的全局唯一标识符 (GUID)，指示存在新的行版本。 队列读取器代理在同步过程中用此列来确定是否存在冲突。  
  
 队列中的事务将保留新旧两个行版本值。 在发布服务器中应用事务时，该事务的 GUID 将与发布中的 GUID 进行比较。 如果事务中存储的旧 GUID 与发布中的 GUID 相匹配，则将更新发布并将订阅服务器生成的新 GUID 分配给行。 通过用事务的 GUID 更新发布，可以使发布与事务中的行版本相匹配。  
  
 如果事务中存储的旧 GUID 与发布中的 GUID 不匹配，便检测到了冲突。 发布中的新 GUID 指示存在两个不同的行版本：一个版本位于订阅服务器正在提交的事务中，较新版本位于发布服务器中。 在这种情况下，在本订阅服务器事务同步之前，另一个订阅服务器或发布服务器更新了发布中的同一行。  
  
 与合并复制不同，使用 GUID 列的目的不是标识行本身，而是检查行是否已更改。  
  
## <a name="resolving-conflicts"></a>解决冲突  
 使用排队更新创建发布时，请选择在检测到任何冲突时要使用的冲突解决程序。 冲突解决程序控制队列读取器代理如何处理在同步过程中遇到的相同行的不同版本。 创建发布后，只要该发布未被订阅，就可以更改冲突解决策略。 可以选择下列冲突解决程序：  
  
-   发布服务器入选（默认）  
  
-   发布服务器入选并且重新初始化订阅  
  
-   订阅服务器入选  
  
 将记录冲突并可使用冲突查看器进行查看。  
  
 **设置排队更新冲突解决策略**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[设置排队更新冲突解决选项 (SQL Server Management Studio)](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   复制 Transact-SQL 编程： [允许更新事务发布的订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)。  
  
 **查看数据冲突**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[查看事务发布的数据冲突 (SQL Server Management Studio)](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>发布服务器入选  
 如果将冲突解决设置为服务器入选，将根据发布服务器中的数据保持事务的一致性。 冲突的事务将回滚到启动该事务的订阅服务器。  
  
 队列读取器代理检测冲突，生成补偿命令并通过在分发数据库中发布这些命令来将其传播到订阅服务器。 然后，分发代理将补偿命令应用到引起冲突事务的订阅服务器。 补偿操作更新订阅服务器中的行，使其与发布服务器中的行相匹配。  
  
 在应用补偿命令之前，可以读取最终将回滚到订阅服务器的事务结果。 这相当于脏读（未提交读隔离级别）。 可能发生的后续相关事务无补偿。 但是，事务边界将得到遵守，并且事务中的所有操作都将提交，或者在发生冲突时回滚。  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>发布服务器入选并且重新初始化订阅  
 通过重新初始化订阅服务器来解决冲突可以保持订阅服务器中严格的事务一致性，但如果发布包含大量数据，则这一操作会十分耗时。  
  
 如果队列读取器代理检测到冲突，将拒绝队列中所有剩余的事务（包括冲突中的事务），并将订阅服务器标记为要重新初始化。 为发布生成的下一个快照将由分发代理应用到订阅服务器。  
  
### <a name="subscriber-wins"></a>订阅服务器入选  
 使用订阅服务器入选策略下的冲突检测意味着要更新发布服务器的最后一项订阅服务器事务入选。 在这种情况下，如果检测到冲突，将仍使用订阅服务器发送的事务，并更新发布服务器。 此策略适用于此类更改不会危及数据完整性的应用程序。  
  
## <a name="see-also"></a>另请参阅  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
