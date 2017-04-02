---
title: "MSSQL_ENG020598 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020598 错误"
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020598
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20598|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|应用复制的命令时在订阅服务器上找不到该行。|  
  
## 解释  
 如果分发代理尝试更新订阅服务器上的行，但该行已删除或该行的主键已更改，则事务性复制中会出现此错误。 默认情况下，事务发布的订阅服务器应视为只读，因为更改不会传播回发布服务器。 对于事务性复制，只有使用可更新订阅或对等复制，才能在订阅服务器上进行用户更改。 有关这些选项的信息，请参阅 [对于事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) 和 [对等事务复制](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
## 用户操作  
 **解决此问题：**  
  
1.  如果复制必须继续在确定错误源的同时，指定参数 **-SkipErrors 20598** 分发代理程序。 这样可以使代理跳过导致错误 20598 的更改，同时还可以复制其他更改。  
  
2.  标识订阅服务器上已删除的行，或主键与发布服务器上的相应行的主键不同的行。 可以使用 [tablediff Utility](../../tools/tablediff-utility.md) 来确定发布服务器和订阅服务器中不同的行。 有关使用此实用工具处理复制的数据库的信息，请参阅 [之间的差异和 #40; 比较复制表复制编程 & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
3.  使用 **tablediff** 实用工具或其他方法更正订阅服务器上的行。  
  
4.  （可选）删除 **-SkipErrors** 参数。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  