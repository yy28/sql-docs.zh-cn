---
title: 在现有发布中添加和删除项目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 411a97c4e143ea06ee5bd00dc9a357c4c2c7e1ff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187257"
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>在现有发布中添加和删除项目
  在创建发布后，可以添加和删除项目。 可以随时添加项目，但删除项目所需的操作取决于复制的类型和删除项目的时间。  
  
## <a name="adding-articles"></a>添加项目  
 添加项目涉及的操作有：将项目添加到发布、为发布创建新的快照、同步订阅以应用新项目的架构和数据。  
  
> [!NOTE]  
>  如果向合并发布中添加一个项目和一个依赖于此新项目的现有项目，则必须使用 **@processing_order** 和 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 的 [@processing_order](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)参数指定两个项目的处理顺序。 请考虑以下情况：您要发布一个表，但不发布该表引用的函数。 如果不发布该函数，则无法在订阅服务器中创建相应的表。 将此函数添加到发布时：为 **sp_addmergearticle** 的 **@processing_order** 的 **sp_changemergearticle**；为 **sp_changemergearticle** 的 **@processing_order** 的 **@processing_order**，为参数 **@article**。 此处理顺序可确保在创建依赖于某函数的表之前在订阅服务器上创建该函数。 每个项目可以使用不同的数字，只要函数的数字小于表的数字即可。  
  
1.  用以下方法之一添加一个或多个项目：  
  
    -   [在发布中添加和删除项目 &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [定义项目](define-an-article.md)  
  
2.  将项目添加到发布后，必须为发布（和所有分区，如果发布是带有参数化筛选器的合并发布）创建新的快照。 然后，分发代理或合并代理将新项目的架构和数据复制到订阅服务器（并不重新初始化整个发布）。  
  
    -   若要创建新快照，请参阅 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
    -   若要为包含参数化筛选器的合并发布创建新快照，请参阅[为包含参数化筛选器的合并发布创建快照](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
3.  创建快照后，同步订阅以复制新项目的架构和数据。  
  
    -   若要同步推送订阅，请参阅[同步推送订阅](../synchronize-a-push-subscription.md)。  
  
    -   若要同步请求订阅，请参阅[同步请求订阅](../synchronize-a-pull-subscription.md)。  
  
## <a name="dropping-articles"></a>删除项目  
 可以随时从发布中删除项目，但必须考虑以下行为：  
  
-   从发布中删除项目并不会将对象从发布数据库中删除，也不会将相应对象从订阅数据库中删除。 必要时，使用 DROP \<Object> 删除这些对象。 在删除通过外键约束与其他已发布项目相关的项目时，建议手动或使用按需脚本执行在订阅服务器上删除表：指定包含相应 DROP \<Object> 语句的脚本。 有关详细信息，请参阅[在同步期间执行脚本（复制 Transact-SQL 编程）](../execute-scripts-during-synchronization-replication-transact-sql-programming.md)。  
  
-   对于兼容级别为 90RTM 或更高的合并发布，可以随时删除项目，但需要创建一个新的快照。 此外：  
  
    -   如果项目在联接筛选器或逻辑记录关系中是父项目，就必须先删除关系，这需要重新初始化。  
  
    -   如果项目具有发布中的最后一个参数化筛选器，就必须重新初始化订阅。  
  
-   对于兼容级别低于 90RTM 的合并发布，可以在初始同步订阅之前删除项目，而无需特别考虑。 如果在同步一个或多个订阅之后删除项目，则必须删除、重新创建和同步订阅。  
  
-   对于快照发布或事务发布，可以在创建订阅之前删除项目，而无需特别考虑。 如果在创建一个或多个订阅之后删除项目，则必须删除、重新创建和同步订阅。 有关删除订阅的详细信息，请参阅[订阅发布](../subscribe-to-publications.md)和 [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)。 使用**sp_dropsubscription** 可以删除订阅中的单个项目，而不是删除整个订阅。  
  
1.  从发布中删除项目涉及的操作有：删除项目并为发布创建新的快照。 删除项目会使当前快照失效，因此必须创建新的快照。  
  
    -   若要从发布中删除项目，请参阅[在发布中添加和删除项目 &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md) 或[删除项目](delete-an-article.md)。  
  
2.  从发布中删除项目后，必须为发布（和所有分区，如果发布是带有参数化筛选器的合并发布）创建新的快照。  
  
    -   若要创建新快照，请参阅 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
    -   若要为包含参数化筛选器的合并发布创建新快照，请参阅[为包含参数化筛选器的合并发布创建快照](../create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 如上所述，在某些情况下删除项目需要删除、重新创建及同步订阅。 有关详细信息，请参阅[订阅发布](../subscribe-to-publications.md)和[同步数据](../synchronize-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [发布数据和数据库对象](publish-data-and-database-objects.md)   
 [重新初始化订阅](../reinitialize-subscriptions.md)   
 [对发布数据库进行架构更改](make-schema-changes-on-publication-databases.md)  
  
  
