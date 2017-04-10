---
title: "为合并项目指定不应跟踪删除（复制 Transact-SQL 编程） | Microsoft Docs"
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
  - "条件性删除跟踪 [SQL Server 复制]"
  - "合并复制 [SQL Server 复制], 条件性删除跟踪"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 为合并项目指定不应跟踪删除（复制 Transact-SQL 编程）
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 默认情况下，合并复制同步发布服务器和订阅服务器之间的 DELETE 命令。 您可以使用合并复制来保留订阅数据库中的行，即使这些行已从发布中删除，反之亦然。 您可以通过编程方式指定在创建新项目时忽略 DELETE 命令，或者可以使用复制存储过程在以后启用此功能。  
  
> [!IMPORTANT]  
>  启用此功能将导致无法收敛，也就是说，位于订阅服务器上的数据将无法准确反映发布服务器上的数据。 您必须实现自己的用于手动删除已删除行的机制。  
  
### 指定对新合并项目忽略删除  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 将值指定为 **false** 为 **@delete_tracking**。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  如果在另一个发布中，值的已发布项目的源表 **delete_tracking** 必须是两个项目相同的。  
  
### 为现有的合并项目指定忽略删除  
  
1.  若要确定是否为项目启用错误补偿，执行 [sp_helpmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 记下的值和 **delete_tracking** 结果集中。 如果该值为 **0**，则删除已被忽略。  
  
2.  如果步骤 1 中的值为 **1**, ，执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 在发布数据库上的发布服务器。 将值指定为 **delete_tracking** 为 **@property**, ，且值为 **false** 为 **@value**。  
  
    > [!NOTE]  
    >  如果在另一个发布中，值的已发布项目的源表 **delete_tracking** 必须是两个项目相同的。  
  
## 另请参阅  
 [用条件性删除跟踪优化合并复制的性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  