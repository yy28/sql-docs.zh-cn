---
title: "控制同步期间触发器和约束的行为（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "标识 [SQL Server 复制]"
  - "约束 [SQL Server], 复制"
  - "触发器 [SQL Server], 复制"
  - "触发器 [SQL Server 复制]"
  - "约束 [SQL Server 复制]"
  - "NOT FOR REPLICATION 选项"
  - "NFR 选项"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）
  在同步期间，复制代理执行 [插入 & #40;Transact SQL & #41;](../../t-sql/statements/insert-transact-sql.md), ，[更新 & #40;Transact SQL & #41;](../../t-sql/queries/update-transact-sql.md), ，和 [DELETE & #40;Transact SQL & #41;](../../t-sql/statements/delete-transact-sql.md) 复制的表，这要执行这些表上可能导致数据操作语言 (DML) 触发器的语句。 有些情况下，可能需要在同步期间防止这些触发器触发或防止约束被强制执行。 此行为取决于触发器或约束的创建方式。  
  
### 防止触发器在同步期间执行  
  
1.  在创建新的触发器，指定的 NOT FOR REPLICATION 选项 [CREATE TRIGGER & #40;Transact SQL & #41;](../../t-sql/statements/create-trigger-transact-sql.md)。  
  
2.  对于现有的触发器，指定 NOT FOR REPLICATION 选项 [ALTER TRIGGER & #40;Transact SQL & #41;](../../t-sql/statements/alter-trigger-transact-sql.md)。  
  
### 防止约束在同步期间被强制执行  
  
1.  创建新的 CHECK 或 FOREIGN KEY 约束时，约束的定义中指定 CHECK NOT FOR REPLICATION 选项 [CREATE TABLE & #40;Transact SQL & #41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## 另请参阅  
 [创建表 & #40; 数据库引擎 & #41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  