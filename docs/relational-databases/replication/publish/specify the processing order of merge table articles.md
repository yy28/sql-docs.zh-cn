---
title: "指定合并表项目的处理顺序（复制 Transact-SQL 编程） | Microsoft Docs"
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
  - "项目 [SQL Server 复制], 处理顺序"
  - "合并复制 [SQL Server 复制], 项目处理顺序"
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 指定合并表项目的处理顺序（复制 Transact-SQL 编程）
  通过使用合并复制，您可以指定在同步过程中合并代理处理项目的顺序。 您可以在使用复制存储过程创建项目时以编程方式为每个项目指定顺序。 项目按值的由低到高顺序进行处理。 如果两个项目具有相同值，将对其进行并发处理。 有关详细信息，请参阅 [指定处理顺序的合并项目](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。  
  
### 为新的合并项目指定处理顺序  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定一个整数值，表示项目的处理顺序 **@processing_order**。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  创建指定了顺序的项目时，应在项目顺序值之间留有间隔。 这样便于以后设置新值。 例如，如果您有三个项目，您需要指定固定的处理顺序，设置的值 **@processing_order** 到 10、 20 和 30 而不是 1、 2 和 3，分别。  
  
### 更改合并项目的处理顺序  
  
1.  若要确定处理顺序的一篇文章，请执行 [sp_helpmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 记下的值和 **processing_order** 结果集中。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将值指定为 **processing_order** 为 **@property** 和一个整数值，该值表示的处理顺序 **@value**。  
  
## 另请参阅  
 [指定合并项目的处理顺序](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  