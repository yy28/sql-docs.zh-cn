---
title: "MSSQL_ENG014121 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014121 错误"
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG014121
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14121|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法删除分发服务器 '%s'。 此分发服务器与分发数据库相关联。|  
  
## 解释  
 配置为分发服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例无法从分发服务器的角色中删除，因为存在与此实例相关联的分发数据库。 如果试图删除与一个或多个发布服务器相关联的分发数据库，将发生此错误。  
  
## 用户操作  
 若要查找的所有发布服务器和与此分发服务器相关联的分发数据库的名称，请执行 [sp_helpdistpublisher & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md) 从分发服务器上的任何数据库。  
  
 执行 [sp_dropdistributiondb & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) 有关与此分发服务器关联的所有分发数据库。 删除所有分发数据库关联后，才可以禁用分发。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  