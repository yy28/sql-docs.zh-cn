---
title: "执行合并项目的虚更新（复制 Transact-SQL 编程） | Microsoft Docs"
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
  - "sp_mergedummyupdate"
  - "虚更新 [SQL Server 复制]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 执行合并项目的虚更新（复制 Transact-SQL 编程）
  合并复制将触发器作为复制过程的一部分；在对发布的表进行更新时，将会触发更新触发器。 在某些情况下，无需触发触发器便可以更新数据，比如在 WRITETEXT 和 UPDATETEXT 操作期间。 在这些情况下，您需要显式添加虚 UPDATE 语句来复制更改。 可以使用复制存储过程添加虚 UPDATE 语句。  
  
### 添加虚 UPDATE 语句  
  
1.  请对需要虚更新的合并发布表中的行执行操作（例如，UPDATETEXT）。  
  
2.  在服务器上 （发布服务器或订阅服务器） 进行了更改数据库上，执行 [sp_mergedummyupdate & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md)。 指定的表更改出于 **@source_object**, ，以及有关已更改的行的唯一标识符 **@rowguid**。  
  
3.  同步此订阅以复制更改行。  
  
  