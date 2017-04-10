---
title: "监视运行包和其他操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# 监视运行包和其他操作
  您可以使用以下一个或多个工具监视 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包执行、项目验证和其他操作。 某些工具（如数据分流）只适用于部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的项目。  
  
-   日志  
  
     有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
-   报表  
  
     有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。  
  
-   视图  
  
     有关详细信息，请参阅[视图（Integration Services 目录）](../../integration-services/system-views/views-integration-services-catalog.md)。  
  
-   性能计数器  
  
     有关详细信息，请参阅[性能计时器](../../integration-services/performance/performance-counters.md)。  
  
-   数据分流  
  
## 操作类型  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的 **SSISDB** 目录中监视几种不同的操作类型。 每个操作可以具有多个与其关联的消息。 每个消息可划分为若干不同类型之一。 例如，消息可以是信息、警告或错误类型。 有关消息类型的完整列表，请参阅针对 Transact-SQL [catalog.operation_messages（SSISDB 数据库）](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)视图的文档。 有关操作类型的完整列表，请参阅 [catalog.operations（SSISDB 数据库）](../../integration-services/system-views/catalog-operations-ssisdb-database.md)。  
  
 使用九种不同的状态类型来指示操作的状态。 有关状态类型的完整列表，请参阅 [catalog.operations（SSISDB 数据库）](../../integration-services/system-views/catalog-operations-ssisdb-database.md)视图。  
  
## 相关内容  
 blogs.msdn.com 上的博客文章 [SSIS T-SQL API 概述](http://go.microsoft.com/fwlink/?LinkId=249051)。  
  
  