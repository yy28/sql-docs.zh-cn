---
title: "远程服务器上的负载平衡包的日志记录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "日志 [Integration Services], 远程包"
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# 远程服务器上的负载平衡包的日志记录
  如果所有子包都使用相同的日志提供程序并且它们全部写入相同的目标，则管理员更容易管理在各个服务器上运行的所有子包的日志。 创建所有子包公用日志文件的一种方式是：将子包配置为“将子包事件记录到 SQL Server 日志提供程序”。 可以将所有包配置为使用相同的数据库、相同的服务器和相同的服务器实例。  
  
 若要查看日志文件，管理员只须登录到单个服务器上，即可查看所有子包的日志文件。  
  
## 相关任务  
 有关如何在包中启用日志记录的信息，请参阅[在 SQL Server Data Tools 中启用包日志记录](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)。  
  
## 另请参阅  
 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  