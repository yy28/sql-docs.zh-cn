---
title: "Integration Services 服务（SSIS 服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 服务, 关于 Integration Services 服务"
  - "SQL Server Integration Services 服务"
  - "服务 [Integration Services], 关于 Integration Services 服务"
  - "服务 [Integration Services]"
  - "SQL Server Integration Services, 服务"
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Integration Services 服务（SSIS 服务）
  本节中的主题论述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 此服务不是创建、保存和运行集成服务包所必需的。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支持 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务以便与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的早期版本向后兼容。  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将对象、设置和运行数据存储在使用项目部署模型部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的项目的 **SSISDB** 数据库中。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的实例，它承载该数据库。 有关数据库的详细信息，请参阅 [SSIS 目录](../../integration-services/service/ssis-catalog.md)。 有关将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的详细信息，请参阅[将项目部署到 Integration Services 服务器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)。  
  
## 管理功能  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务是用于管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的 Windows 服务。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务只在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中可用。  
  
 运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务可以提供下列管理功能：  
  
-   启动远程和本地存储的包  
  
-   停止远程和本地运行的包  
  
-   监视远程和本地运行的包  
  
-   导入和导出包  
  
-   管理包存储  
  
-   自定义存储文件夹  
  
-   在服务停止时停止正在运行的包  
  
-   查看 Windows 事件日志  
  
-   连接到多台 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器  
  
## 用于集成服务服务的启动类型  
 在安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件时会安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务。 默认情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务已启动，该服务的启动类型已设置为自动。 该服务必须运行，才能监视存储在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中的包。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中的 msdb 数据库，也可以是文件系统中指定的文件夹。  
  
 如果只希望设计和执行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不是必需的。 但是，若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]列出和监视包，则该服务是必需的。  
  
## 相关任务  
  
-   [设置 Integration Services 服务的属性](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
-   [查看 Integration Services 服务的事件](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
  