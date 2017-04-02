---
title: "客户端协议 - Named Pipes 属性（“协议”选项卡） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "管道 [SQL Server], 连接至"
  - "已命名 [SQL Server], 默认管道"
  - "客户端协议 [SQL Server]"
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 客户端协议 - Named Pipes 属性（“协议”选项卡）
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中，使用 **“Named Pipes 属性”** 对话框中的 **“协议”** 选项卡可以查看或修改默认管道的说明。 若要连接到其他管道，请在 **“默认管道”** 框中键入该管道。 有关连接字符串的详细信息，请参阅 [Creating a Valid Connection String Using Named Pipes](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)。  
  
## 选项  
 **默认管道**  
 指定 Named Pipes 网络库用来尝试连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标实例的默认管道。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听： `\\.\pipe\sql\query`  
  
 若要连接到默认管道，请输入 `sql\query`  
  
 **已启用**  
 可能的值为“是”和“否”。  
  
## 另请参阅  
 [选择网络协议](../Topic/Choosing%20a%20Network%20Protocol.md)  
  
  