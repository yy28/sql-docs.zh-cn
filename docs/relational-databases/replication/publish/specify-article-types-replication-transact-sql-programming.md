---
title: "指定项目类型（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
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
  - "发布 [SQL Server 复制], 存储过程执行"
  - "项目 [SQL Server 复制], 事务复制选项"
  - "项目 [SQL Server 复制], 合并复制选项"
  - "存储过程 [SQL Server 复制], 发布"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 指定项目类型（复制 Transact-SQL 编程）
  复制的默认项目类型为表项目，但可以将其他数据库对象发布为项目，这些项目包括视图、存储过程、用户定义函数以及存储过程执行。 定义项目时，您可以使用复制存储过程以编程方式指定项目类型。 您要使用的具体过程取决于复制的类型和项目的类型。  
  
> [!NOTE]  
>  定义表、视图和存储过程项目时采用仅限架构的设计表示只复制对象定义。  
  
### 在事务发布或快照发布中发布表项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 将 **@type** 指定为以下值之一以定义项目类型：  
  
    -   **logbased** -基于日志的表项目，这是默认值为事务复制和快照复制。 复制会自动生成用于水平筛选的存储过程和定义垂直筛选项目的视图。  
  
    -   **logbased manualfilter** -基于日志的水平筛选项目，其中用于水平筛选的存储的过程是手动创建用户定义的为指定 **@filter**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **logbased manualview** -基于日志的垂直筛选项目，其中定义垂直筛选的项目的视图是创建用户定义的为指定 **@sync_object**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **logbased manualboth** --基于日志的水平和垂直筛选的项目，其中用于水平筛选和定义垂直筛选的项目的视图的存储的过程创建，并由用户定义并且指定 **@filter** 和 **@sync_object**, 分别。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  有关 **logbased manualboth** 和 **logbased manualfilter** 项目，请执行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 来生成用于水平筛选项目的筛选存储的过程。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  有关 **logbased manualboth**, ，**logbased manualview**, ，和 **logbased manualfilter** 项目，请执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 来生成用于定义垂直筛选的项目的视图。 有关详细信息，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### 在事务发布或快照发布中发布视图项目或索引视图项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 将 **@type** 指定为以下值之一以定义项目类型：  
  
    -   **索引视图 logbased** -基于日志的索引的视图项目。 复制会自动生成用于水平筛选的存储过程和定义垂直筛选项目的视图。  
  
    -   **仅限视图架构** -仅限架构的视图项目。 还必须复制基表。  
  
    -   **仅限索引的视图架构** -仅限架构的索引的视图项目。 还必须复制基表。  
  
    -   **索引视图 logbased manualfilter** -基于日志的水平筛选索引的视图项目，其中用于水平筛选的存储的过程是手动创建用户定义的为指定 **@filter**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **索引视图 logbased manualview** -基于日志的筛选索引的视图项目，其中定义垂直筛选的项目的视图是创建用户定义的为指定 **@sync_object**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **索引视图 logbased manualboth** -基于日志的、 经过筛选的索引的视图项目创建和用户定义的以及为指定的存储的过程用于水平筛选和定义垂直筛选的项目的视图 **@filter** 和 **@sync_object**, 分别。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  有关 **logbased manualboth** 和 **logbased manualfilter** 项目，请执行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 来生成用于水平筛选项目的筛选存储的过程。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  有关 **logbased manualboth**, ，**logbased manualview**, ，和 **logbased manualfilter** 项目，请执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 来生成用于定义垂直筛选的项目的视图。 有关详细信息，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### 在事务发布或快照发布中发布存储过程、存储过程执行或用户定义函数项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 将 **@type** 指定为以下值之一以定义项目类型：  
  
    -   **仅限 proc 架构** -仅限架构的存储的过程项目。  
  
    -   **proc exec** -将存储过程的执行复制到的项目的所有订阅服务器。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **serializable proc exec** -仅当它可序列化事务的上下文中执行复制存储过程的执行。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **仅限 func 架构** -仅限架构的用户定义函数项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### 在合并发布中发布表或视图项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 将 **@type** 指定为以下值之一以定义项目类型：  
  
    -   **表** -表项目。  
  
    -   **仅限索引的视图架构** -仅限架构的索引的视图项目。  
  
    -   **仅限视图架构** -仅限架构的视图项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### 在合并发布中发布存储过程或用户定义函数项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 将 **@type** 指定为以下值之一以定义项目类型：  
  
    -   **仅限 func 架构** -仅限架构的用户定义函数项目。  
  
    -   **仅限 proc 架构** -仅限架构的存储的过程项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 另请参阅  
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  