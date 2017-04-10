---
title: "MSSQL_ENG021330 | Microsoft Docs"
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
  - "MSSQL_ENG021330 错误"
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021330
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21330|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法在复制工作目录下创建子目录。(%ls)|  
  
## 解释  
 当手动初始化订阅而且创建存储复制脚本的目录有问题时，会出现此错误。 权限问题可导致此错误：在不使用快照的情况下初始化订阅时，在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户对分发服务器上的快照文件夹必须具有写权限。  
  
## 用户操作  
 请确保已为快照文件夹指定正确的路径，并且在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户具有足够的权限。  
  
## 另请参阅  
 [指定默认快照位置 & #40;SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  