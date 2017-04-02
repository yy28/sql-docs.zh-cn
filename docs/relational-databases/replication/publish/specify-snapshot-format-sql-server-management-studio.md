---
title: "指定快照格式 (SQL Server Management Studio) | Microsoft Docs"
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
  - "快照 [SQL Server 复制]，格式"
  - "快照复制 [SQL Server]，格式"
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 指定快照格式 (SQL Server Management Studio)
  指定快照格式 **快照** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 指定快照格式  
  
1.  在 **快照** 页 **发布属性-\< 发布>** 对话框中，选择 **本机 SQL Server-所有订阅服务器必须是运行 SQL Server 服务器** 或 **字符-如果发布服务器或订阅服务器上未运行 SQL Server，则需要**。  
  
    > [!NOTE]  
    >  建议选择本机格式，除非此发布必须支持对 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 数据库或非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的订阅。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另请参阅  
 [配置快照属性和 #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  