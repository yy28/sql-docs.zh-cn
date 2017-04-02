---
title: "Integration Services (SSIS) 服务器和目录 | Microsoft Docs"
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
  - "包 [Integration Services], 管理"
  - "管理包 [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Integration Services (SSIS) 服务器和目录
  当您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中设计和测试包后，可将包含包的项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器是一个实例的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 承载 **SSISDB** 数据库。 该数据库存储以下对象：包、项目、参数、权限、服务器属性和操作历史记录。  
  
 **SSISDB** 数据库在您可以查询的公共视图中公开对象信息。 数据库还提供存储过程，您可以调用这些存储过程以管理该对象。  
  
 您可以将项目部署到之前 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器，则需要创建 **SSISDB** 目录。  
  
 SSISDB 目录功能的概述，请参阅 [SSIS 目录](../../integration-services/service/ssis-catalog.md)。  
  
## 高可用性  
 像其他用户数据库一样， **SSISDB** 数据库不支持数据库镜像和复制。 有关镜像和复制的详细信息，请参阅 [数据库镜像 & #40;SQL Server 和 #41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 您还可以通过提供 SSISDB 及其内容的高可用性利用 SSIS 和 Alwayson 可用性组。 有关详细信息，请参阅 Matt Masson 的博客文章 [使用 Always On 的 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873), ，blogs.msdn.com 上的。  
  
##  <a name="ssms"></a> SQL Server Management Studio 中的 Integration Services 服务器  
 当您连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 承载 **SSISDB** 数据库，请参阅对象资源管理器中的以下对象︰  
  
-   **SSISDB 数据库**  
  
     在对象资源管理器中的 **“数据库”** 节点下，您可以看到 **SSISDB** 数据库。 您可以查询视图和调用存储过程，这些存储过程既管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器，也管理在该服务器上存储的对象。  
  
-   **Integration Services 目录**  
  
     在 **“Integration Services 目录”** 节点下，有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目和环境的文件夹。  
  
## 相关任务  
  
-   [创建 SSIS 目录](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [查看 Integration Services 服务器上的包列表](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [将项目部署到 Integration Services 服务器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## 相关内容  
 博客文章 [使用 Always On 的 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873), ，blogs.msdn.com 上的。  
  
  