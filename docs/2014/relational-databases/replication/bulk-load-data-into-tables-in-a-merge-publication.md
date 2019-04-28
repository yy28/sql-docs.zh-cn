---
title: 大容量加载数据到表中的合并发布 （复制 TRANSACT-SQL 编程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09e535057fcf573dfa189b7e5fdc0e0df06e5d4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721759"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication-replication-transact-sql-programming"></a>将数据大容量加载到合并发布中的表（复制 Transact-SQL 编程）
  使用 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 命令将数据加载到表时，默认情况下，不会触发在 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql) 系统表中保留跟踪数据的合并复制触发器。 可以在加载数据时强制触发合并复制触发器，也可以使用复制存储过程，在大容量复制操作之后以编程方式插入生成的复制元数据。  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>使用 bcp 实用工具将数据大容量加载到合并复制所发布的表中  
  
1.  在发布服务器或订阅服务器上，执行 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 以将数据插入到使用合并复制发布的表中。  
  
2.  使用以下方法之一来确保为插入的数据生成复制元数据。  
  
    -   使用 FIRE_TRIGGERS 选项执行大容量复制。  
  
    -   对插入数据的数据库执行 [sp_addtabletocontents (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql)。 为 **@table_name**。  
  
  
