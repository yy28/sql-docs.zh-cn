---
title: "MSSQL_ENG021286 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021286 错误"
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021286
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21286|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|冲突表 '%s' 不存在。|  
  
## 解释  
 如果项目的冲突表中列出，则会引发此错误 [sysmergearticles & #40;Transact SQL & #41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 实际上不存在。 尝试向为合并复制发布的表中添加列或从中删除列，也会发生此错误。  
  
## 用户操作  
 执行 [DBCC CHECKDB & #40;Transact SQL & #41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 对缺少冲突表，若要验证的数据库没有数据一致性问题。  
  
 如果订阅服务器上缺少冲突表，请删除订阅并重新创建它。 如果发布服务器上缺少冲突表，请删除所有订阅，删除发布，然后重新创建发布和所有订阅。 有关详细信息，请参阅 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md) 和 [订阅的发布](../../relational-databases/replication/subscribe-to-publications.md)。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  