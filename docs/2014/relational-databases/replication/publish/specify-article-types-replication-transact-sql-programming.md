---
title: 指定项目类型（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bcd980bb7fe77e2d207e568802dfd7e69e9a1484
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882119"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>指定项目类型（复制 Transact-SQL 编程）
  复制的默认项目类型为表项目，但可以将其他数据库对象发布为项目，这些项目包括视图、存储过程、用户定义函数以及存储过程执行。 定义项目时，您可以使用复制存储过程以编程方式指定项目类型。 您要使用的具体过程取决于复制的类型和项目的类型。  
  
> [!NOTE]  
>  定义表、视图和存储过程项目时采用仅限架构的设计表示只复制对象定义。  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>在事务发布或快照发布中发布表项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 为 **\@类型**指定以下值之一以定义项目类型：  
  
    -   **logbased** - 基于日志的表项目，是事务复制和快照复制的默认值。 复制会自动生成用于水平筛选的存储过程和定义垂直筛选项目的视图。  
  
    -   **logbased manualfilter** -基于日志的水平筛选项目，其中用于水平筛选的存储过程由用户手动创建和定义，并指定 **\@筛选器**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
    -   **logbased manualview** -基于日志的垂直筛选项目，其中定义垂直筛选项目的视图由用户创建和定义，并为 **\@sync_object**指定。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
    -   **logbased manualboth** -基于日志的水平和垂直筛选项目，其中用于水平筛选的存储过程和定义垂直筛选项目的视图由用户创建和定义，并分别指定给 **\@筛选器**和 **\@sync_object**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](define-an-article.md)。  
  
2.  对于 **logbased manualboth** 和 **logbased manualfilter** 项目，请执行 [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) 生成用于水平筛选项目的筛选存储过程。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
3.  对于 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 项目，请执行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) 生成用于定义垂直筛选项目的视图。 有关详细信息，请参阅 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>在事务发布或快照发布中发布视图项目或索引视图项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 为 **\@类型**指定以下值之一以定义项目类型：  
  
    -   **indexed view logbased** - 基于日志的索引视图项目 复制会自动生成用于水平筛选的存储过程和定义垂直筛选项目的视图。  
  
    -   **view schema only** - 仅限架构的视图项目。 还必须复制基表。  
  
    -   **indexed view schema only** - 仅限架构的索引视图项目。 还必须复制基表。  
  
    -   **indexed view logbased manualfilter** -基于日志的水平筛选索引视图项目，其中用于水平筛选的存储过程由用户手动创建和定义，并指定给 **\@筛选器**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
    -   **indexed view logbased manualview** -基于日志的筛选索引视图项目，其中定义垂直筛选项目的视图由用户创建和定义，并为 **\@sync_object**指定。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
    -   **indexed view logbased manualboth** -基于日志的筛选索引视图项目，其中用于水平筛选的存储过程和定义垂直筛选项目的视图均由用户创建和定义，并分别指定给 **\@筛选器**和 **\@sync_object**。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md) 和 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](define-an-article.md)。  
  
2.  对于 **logbased manualboth** 和 **logbased manualfilter** 项目，请执行 [sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql) 生成用于水平筛选项目的筛选存储过程。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md)。  
  
3.  对于 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 项目，请执行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql) 生成用于定义垂直筛选项目的视图。 有关详细信息，请参阅 [Define and Modify a Column Filter](define-and-modify-a-column-filter.md)。  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>在事务发布或快照发布中发布存储过程、存储过程执行或用户定义函数项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 为 **\@类型**指定以下值之一以定义项目类型：  
  
    -   **proc schema only** - 仅限架构的存储过程项目。  
  
    -   **proc exec** - 将存储过程的执行复制到项目的所有订阅服务器。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **serializable proc exec** - 仅当存储过程是在可序列化事务的上下文中执行时才复制存储过程的执行。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **func schema only** - 仅限架构的用户定义函数项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](define-an-article.md)。  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>在合并发布中发布表或视图项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 为 **\@类型**指定以下值之一以定义项目类型：  
  
    -   **table** - 表项目。  
  
    -   **indexed view schema only** - 仅限架构的索引视图项目。  
  
    -   **view schema only** - 仅限架构的视图项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](define-an-article.md)。  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>在合并发布中发布存储过程或用户定义函数项目  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 为 **\@类型**指定以下值之一以定义项目类型：  
  
    -   **func schema only** - 仅限架构的用户定义函数项目。  
  
    -   **proc schema only** - 仅限架构的存储过程项目。  
  
     这样便为发布定义了一个新项目。 有关详细信息，请参阅 [Define an Article](define-an-article.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复制系统存储过程概念](../concepts/replication-system-stored-procedures-concepts.md)   
 [发布数据和数据库对象](publish-data-and-database-objects.md)  
  
  
