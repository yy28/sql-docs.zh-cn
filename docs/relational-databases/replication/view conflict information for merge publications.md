---
title: "查看合并发布的冲突信息（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "合并复制冲突解决 [SQL Server 复制], 查看冲突"
  - "sp_helpmergeconflictrows"
  - "查看冲突信息"
  - "冲突解决 [SQL Server 复制], 合并复制"
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 查看合并发布的冲突信息（复制 Transact-SQL 编程）
  在合并复制中解决冲突后，落选行中的数据将写入冲突表中。 这些冲突数据可以使用复制存储过程以编程方式进行查看。 有关详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### 查看所有类型冲突的冲突信息和落选行数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** -1 指示冲突行存储在发布服务器中，0 指示冲突行未存储在发布服务器。  
  
    -   **decentralized_conflicts** -1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为通过设置 **@conflict_logging** 参数 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 利用 **@centralized_conflicts** 参数已被否决。  
  
     下表描述在为指定的值基于这些列的值 **@conflict_logging**。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  在发布服务器的发布数据库上或在订阅服务器上的订阅数据库上，执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突信息。 这将返回具有冲突的项目的冲突表信息。 记下的值 **conflict_table** 感兴趣的任何项目。 如果值 **conflict_table** 一篇文章为 NULL，在这篇文章中发生了只有删除冲突。  
  
3.  （可选）查看相关项目的冲突行。 根据值 **centralized_conflicts** 和 **decentralized_conflicts** 从步骤 1 中，执行下列操作之一︰  
  
    -   在发布服务器上对发布数据库中，执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 指定的文章 （来自步骤 1） 一个冲突表 **@conflict_table**。 （可选）将值指定为 **@publication** 来限制对特定发布返回的冲突信息。 这将会返回落选行的行数据和其他信息。  
  
    -   在订阅服务器上的订阅数据库上，执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 指定的文章 （来自步骤 1） 一个冲突表 **@conflict_table**。 这将会返回落选行的行数据和其他信息。  
  
### 仅查看与删除失败相关的冲突的信息  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** -1 指示冲突行存储在发布服务器中，0 指示冲突行未存储在发布服务器。  
  
    -   **decentralized_conflicts** -1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器。  
  
        > [!NOTE]  
        >  使用设置合并发布的冲突日志记录行为 **@conflict_logging** 参数 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 利用 **@centralized_conflicts** 参数已被否决。  
  
2.  在发布服务器的发布数据库上或在订阅服务器上的订阅数据库上，执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 **@publication** 指定值，以便只返回属于特定发布的项目的冲突表信息。 这将返回具有冲突的项目的冲突表信息。 记下的值 **source_object** 感兴趣的任何项目。 如果值 **conflict_table** 一篇文章为 NULL，在这篇文章中发生了只有删除冲突。  
  
3.  （可选）查看删除冲突的冲突信息。 根据值 **centralized_conflicts** 和 **decentralized_conflicts** 从步骤 1 中，执行下列操作之一︰  
  
    -   在发布服务器上对发布数据库中，执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 指定的源表 （来自步骤 1） 在其发生冲突的名称 **@source_object**。 （可选）将值指定为 **@publication** 来限制对特定发布返回的冲突信息。 这将返回发布服务器上存储的删除冲突信息。  
  
    -   在订阅服务器上的订阅数据库上，执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 指定的源表 （来自步骤 1） 在其发生冲突的名称 **@source_object**。 （可选）将值指定为 **@publication** 来限制对特定发布返回的冲突信息。 这将返回订阅服务器上存储的删除冲突信息。  
  
## 另请参阅  
 [高级合并复制冲突的检测和解决](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  