---
title: 查看合并发布的冲突信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a87f0391580dd8f577abf94997fd1448ae5bf198
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="view-conflict-information-for-merge-publications"></a>查看合并发布的冲突信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在合并复制中解决冲突后，落选行中的数据将写入冲突表中。 这些冲突数据可以使用复制存储过程以编程方式进行查看。 有关详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>查看所有类型冲突的冲突信息和落选行数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 **@conflict_logging** 的 [@conflict_logging](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 已不推荐使用 **@centralized_conflicts** 参数。  
  
     下表基于为 **@conflict_logging**。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**发布服务器**|@shouldalert|0|  
    |**订阅服务器**|0|@shouldalert|  
    |**两者**|@shouldalert|@shouldalert|  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **conflict_table** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看相关项目的冲突行。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 将步骤 1 中的项目的冲突表指定给 **@conflict_table**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将会返回落选行的行数据和其他信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 将步骤 1 中的项目的冲突表指定给 **@conflict_table**。 这将会返回落选行的行数据和其他信息。  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>仅查看与删除失败相关的冲突的信息  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 **@conflict_logging** 的 [@conflict_logging](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 已不推荐使用 **@centralized_conflicts** 参数。  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突表信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **source_object** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看删除冲突的冲突信息。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 将步骤 1 中发生冲突的源表的名称指定给 **@source_object**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将返回发布服务器上存储的删除冲突信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 将步骤 1 中发生冲突的源表的名称指定给 **@source_object**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将返回订阅服务器上存储的删除冲突信息。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
