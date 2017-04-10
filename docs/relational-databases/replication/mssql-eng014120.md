---
title: "MSSQL_ENG014120 | Microsoft Docs"
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
  - "MSSQL_ENG014120 错误"
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG014120
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14120|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法删除分发数据库 '%s'。 此分发服务器数据库与发布服务器相关联。|  
  
## 解释  
 分发数据库存储事务性复制的所有复制和事务类型的元数据和历史记录数据。 如果试图删除与一个或多个发布服务器相关联的分发数据库，将发生此错误。  
  
## 用户操作  
 若要删除分发数据库，必须先删除分发服务器与发布服务器之间的关联。 有关详细信息，请参阅 [sp_dropdistpublisher & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  