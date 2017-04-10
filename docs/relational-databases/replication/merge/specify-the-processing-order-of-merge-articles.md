---
title: "指定合并项目的处理顺序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "项目 [SQL Server 复制], 处理顺序"
  - "合并复制 [SQL Server 复制], 项目处理顺序"
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 指定合并项目的处理顺序
  从 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]开始，可以覆盖合并发布的项目默认处理顺序。 例如，如果通过触发器定义引用完整性而这些触发器又必须按某顺序激发，以上操作就会很有用。  
  
 **指定项目的处理顺序**  
  
-   复制 TRANSACT-SQL 编程︰ [指定处理顺序的合并表项目 & #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/specify the processing order of merge table articles.md)  
  
## 如何确定处理顺序  
 合并同步过程中，项目在默认情况下按照对象间相关性要求的顺序处理，包括基表中定义的声明性引用完整性 (DRI) 约束。 处理涉及将更改枚举到表，然后应用这些更改。 若不存在 DRI，但在表项目之间存在联接筛选器或逻辑记录，则就以筛选器和逻辑记录要求的顺序处理项目。 不相关的文章任何其他项目通过 DRI、 联接筛选器、 逻辑记录或其他依赖关系处理中项目别名根据 [sysmergearticles & #40;Transact SQL & #41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 系统表中。  
  
 考虑一个包含 **SalesOrderHeader** 表和 **SalesOrderDetail** 表的发布，并且 **SalesOrderHeader** 表中具有主键列 **SalesOrderID** 而 **SalesOrderDetail** 表中具有对应的外键列 **SalesOrderID** 。 同步过程中，合并复制通过在 **SalesOrderDetail** 中插入相关行之前先在 **SalesOrderHeader**中插入某些新行的方式来防止违反外键。 同样，要先从 **SalesOrderDetail** 中删除行，然后才从 **SalesOrderHeader**中删除相关行。  
  
 但是，在某些应用程序中，通过数据库触发器（或者在应用程序级，而不是通过 DRI）强制引用完整性。 考虑上述具有引用完整性的发布（而不是 DRI）， **SalesOrderDetail** 表可能会有一个插入触发器以确保在允许插入之前 **SalesOrderHeader** 表中存在相关行。 **SalesOrderHeader** 可能有一个删除触发器以确保在允许删除之前 **SalesOrderDetail** 中没有相关行。 由于合并复制无法在激发触发器之前确定触发器的结果，所以在确定项目的处理顺序时，合并复制不会考虑触发器。 同样，复制也不会考虑在应用程序级定义的约束。  
  
 通过触发器或在应用程序级维护引用完整性时，您应该指定项目应处理的顺序。 在有关触发器的示例中，需要指定在处理 **SalesOrderDetail** 之前先处理 **SalesOrderHeader**表，因为项目排序是根据插入顺序进行的。 合并复制会自动反转删除顺序。 不进行项目排序也不会导致合并复制失败，因为即使违反约束，合并代理也会继续处理项目；然后它会在处理完其他项目后重试所有过去失败的操作。 指定项目顺序仅避免重试以及其他与其相关联的处理。 如果指定了错误顺序（比如，导致详细记录在标题记录前处理的顺序），合并复制会重试处理直到成功。  
  
## 另请参阅  
 [合并复制的项目选项](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [通过逻辑记录对相关行的更改进行分组](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [联接筛选器](../../../relational-databases/replication/merge/join-filters.md)  
  
  