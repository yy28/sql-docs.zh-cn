---
title: "监视错误日志 | Microsoft Docs"
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
  - "日志 [SQL Server]"
  - "数据库性能 [SQL Server], 错误"
  - "Windows 应用程序日志 [SQL Server]"
  - "监视性能 [SQL Server], 错误"
  - "服务器性能 [SQL Server], 错误"
  - "比较错误和应用程序日志输出"
  - "错误 [SQL Server], 日志"
  - "优化数据库 [SQL Server], 错误"
  - "数据库监视 [SQL Server], 错误"
  - "SQL Server 错误日志"
  - "日志 [SQL Server], SQL Server 错误日志"
  - "错误日志 [SQL Server]"
  - "日志 [SQL Server], Windows 应用程序日志"
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 监视错误日志
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将某些系统事件和用户定义事件记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 应用程序日志中。 这两种日志都会自动给所有记录事件加上时间戳。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中的信息可以解决 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相关问题。  
  
 Windows 应用程序日志完整地记录了 Windows 操作系统上发生的事件，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理中的事件。 使用 Windows 事件查看器可以查看 Windows 应用程序日志和筛选信息。 例如，可以筛选信息、警告、错误、审核成功和审核失败等事件。  
  
## 比较错误和应用程序日志输出  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志和 Windows 应用程序日志来标识产生问题的原因。 例如，监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志时，您可能会遇到不包含原因信息的错误消息。 通过比较两个日志中的事件日期和时间，可以缩小可能原因的范围。 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 日志文件查看器可以将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理和 Windows 日志集成到一个列表，这样可以轻松了解相关的服务器事件和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 有关详细信息，请参阅 SQL Server 联机丛书中的主题“日志文件查看器”。  
  
## 本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[查看 SQL Server 错误日志](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以及如何查看该日志。|  
|[查看 Windows 应用程序日志](../../tools/configuration-manager/viewing-the-windows-application-log.md)|介绍了 Windows 应用程序日志以及如何查看该日志。|  
  
  