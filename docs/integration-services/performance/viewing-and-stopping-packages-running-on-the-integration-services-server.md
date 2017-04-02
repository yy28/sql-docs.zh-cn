---
title: "查看和停止在 Integration Services 服务器上运行的包 | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "包 [Integration Services], 管理"
  - "管理正在运行的包 [Integration Services]"
  - "包 [Integration Services], 运行"
  - "运行包 [Integration Services], 管理"
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# 查看和停止在 Integration Services 服务器上运行的包
  **SSISDB** 数据库在对用户不可见的内部表中存储执行历史记录。 不过，它通过您可以查询的公共视图公开您所需的信息。 它还提供存储过程，您可以调用这些存储过程以执行与包相关的常见任务。  
  
 通常，您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的服务器上管理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对象。 不过，您还可以查询数据库视图和直接调用存储过程，或者编写调用托管 API 的自定义代码。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和托管 API 查询视图并调用存储过程以便执行其许多任务。 例如，您可以查看当前正在服务器上运行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的列表，并且在需要时请求包停止运行。  
  
## 查看正在运行的包的列表  
 您可以在 **“活动操作”** 对话框中查看当前正在服务器上运行的包的列表。 有关详细信息，请参阅 [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md)。  
  
 有关可用于查看正在运行的包列表的其他方法的信息，请参阅以下主题。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要查看正在服务器上运行的包的列表，请为其状态为 2 的包查询视图 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。  
  
 通过托管 API 以编程方式访问  
 请参阅 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间及其类。  
  
## 停止正在运行的包  
 您可以在 **“活动操作”** 对话框中请求正在运行的包停止。 有关详细信息，请参阅 [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md)。  
  
 有关可用于停止正在运行的包的其他方法的信息，请参阅以下主题。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要停止正在服务器上运行的包，请调用存储过程 [catalog.stop_operation（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)。  
  
 通过托管 API 以编程方式访问  
 请参阅 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间及其类。  
  
## 查看已运行的包的历史记录  
 若要查看在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中已运行的包的历史记录，请使用 **“全部执行”** 报表。 有关“全部执行”报表和其他标准报表的详细信息，请参阅 [Integration Services 服务器的报告](../../integration-services/performance/reports-for-the-integration-services-server.md)。  
  
 有关可用于查看正在运行的包的历史记录的其他方法的信息，请参阅以下主题。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要查看与已运行的包有关的信息，请查询视图 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。  
  
 通过托管 API 以编程方式访问  
 请参阅 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间及其类。  
  
## 另请参阅  
 [项目和包的执行](https://msdn.microsoft.com/library/hh213290.aspx)   
 [对包执行进行故障排除的报告](https://msdn.microsoft.com/library/gg471512.aspx)  
  
  