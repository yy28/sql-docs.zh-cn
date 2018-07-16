---
title: 查看合并发布 （复制 TRANSACT-SQL 编程） 的冲突信息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
ms.openlocfilehash: 48225870d89fc6bf39355957187fac84a704093d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316097"
---
# <a name="view-conflict-information-for-merge-publications-replication-transact-sql-programming"></a>查看合并发布的冲突信息（复制 Transact-SQL 编程）
  在合并复制中解决冲突后，落选行中的数据将写入冲突表中。 这些冲突数据可以使用复制存储过程以编程方式进行查看。 有关详细信息，请参阅 [高级合并复制冲突的检测和解决](merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>查看所有类型冲突的冲突信息和落选行数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 **@conflict_logging** 的 [@conflict_logging](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 已不推荐使用 **@centralized_conflicts** 参数。  
  
     下表基于为 **@conflict_logging**。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |`publisher`|@shouldalert|0|  
    |`subscriber`|0|@shouldalert|  
    |`both`|@shouldalert|@shouldalert|  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **conflict_table** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看相关项目的冲突行。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql)。 将步骤 1 中的项目的冲突表指定给 **@conflict_table**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将会返回落选行的行数据和其他信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql)。 将步骤 1 中的项目的冲突表指定给 **@conflict_table**。 这将会返回落选行的行数据和其他信息。  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>仅查看与删除失败相关的冲突的信息  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 **@conflict_logging** 的 [@conflict_logging](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 已不推荐使用 **@centralized_conflicts** 参数。  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突表信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **source_object** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看删除冲突的冲突信息。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql)。 将步骤 1 中发生冲突的源表的名称指定给 **@source_object**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将返回发布服务器上存储的删除冲突信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql)。 将步骤 1 中发生冲突的源表的名称指定给 **@source_object**。 （可选）指定 **@publication** 的值，以便将返回的冲突信息限制为特定发布。 这将返回订阅服务器上存储的删除冲突信息。  
  
## <a name="see-also"></a>请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
