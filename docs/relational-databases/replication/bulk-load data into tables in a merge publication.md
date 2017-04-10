---
title: "将数据大容量加载到合并发布中的表（复制 Transact-SQL 编程） | Microsoft Docs"
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
  - "大容量加载 [SQL Server 复制]"
  - "合并复制大容量加载 [SQL Server 复制]"
  - "sp_addtabletocontents"
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 将数据大容量加载到合并发布中的表（复制 Transact-SQL 编程）
  当将数据加载到表使用 [bcp 实用工具](../../tools/bcp-utility.md) 或 [大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md) 命令时，默认情况下中, 保留跟踪数据的合并复制触发器 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 系统表不会触发。 可以在加载数据时强制触发合并复制触发器，也可以使用复制存储过程，在大容量复制操作之后以编程方式插入生成的复制元数据。  
  
### 使用 bcp 实用工具将数据大容量加载到合并复制所发布的表中  
  
1.  在发布服务器或订阅服务器上，执行 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 以将数据插入到使用合并复制发布的表中。  
  
2.  使用以下方法之一来确保为插入的数据生成复制元数据。  
  
    -   使用 FIRE_TRIGGERS 选项执行大容量复制。  
  
    -   插入数据的数据库上执行 [sp_addtabletocontents & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md)。 指定数据的插入的表名 **@table_name**。  
  
  