---
title: "使用中央管理服务器管理多台服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "08/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "多服务器查询"
  - "中央管理服务器"
  - "多服务器管理 [SQL Server]"
  - "主服务器 [SQL Server], 中央管理服务器"
  - "目标配置 [SQL Server]"
  - "服务器配置 [SQL Server]"
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# 使用中央管理服务器管理多台服务器
  您可以通过指定中央管理服务器并创建服务器组来管理多台服务器。  
  
## 什么是中央管理服务器和服务器组？  
 指定为中央管理服务器的 SQL Server 实例维护服务器组，这些组包含一个或多个实例的连接信息。 可以对服务器组同时执行 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句和基于策略的管理策略。 还可以查看通过中央管理服务器管理的实例上的日志文件。 
 
 中央管理服务器实际上是一个包含托管服务器列表的中央存储库。 不能将早于 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 的版本指定为中央管理服务器。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。  
  
## 创建中央管理服务器和服务器组 
 若要创建中央管理服务器和服务器组，请使用 **中的** “已注册的服务器” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]窗口。 请注意，中央管理服务器不能是它所维护的组的成员。 
 
 有关如何创建中央管理服务器和服务器组的信息，请参阅[创建中央管理服务器和服务器组 (SQL Server Management Studio)](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)。  
  
## 另请参阅  
 [使用基于策略的管理来管理服务器](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  