---
title: "MSSQL_ENG003724 | Microsoft Docs"
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
  - "MSSQL_ENG003724 错误"
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG003724
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3724|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法对 %S_MSG '%.*ls' 执行 %S_MSG，因为它正用于复制。|  
  
## 解释  
 当复制了数据库中的对象时，它们会标记为已复制系统表中 **sysarticles** （对于快照和事务发布） 或 **sysmergearticles** （对于合并发布）。 尝试删除复制的对象时，会引发此错误。  
  
## 用户操作  
 尝试删除对象之前，请确保数据库对象未经复制。 例如：  
  
-   如果此错误发生在发布数据库中，则先从发布中删除项目，然后再删除对象。 有关详细信息，请参阅 [添加项目和删除现有发布的文章](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
-   如果此错误发生在订阅数据库中，则先删除订阅，然后再删除对象。 有关详细信息，请参阅 [订阅的发布](../../relational-databases/replication/subscribe-to-publications.md)。 对于事务发布的订阅，可以删除单个项目的订阅，而不用删除整个发布。 有关详细信息，请参阅 [sp_dropsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。  
  
 如果不会被复制的数据库中发生此错误，则执行 [sp_removedbreplication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 若要确保数据库中的对象未标记为已复制。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  