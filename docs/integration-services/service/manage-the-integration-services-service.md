---
title: "管理 Integration Services 服务 | Microsoft Docs"
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
  - "Integration Services 服务, 配置"
  - "服务 [Integration Services], 配置"
ms.assetid: 45554117-a0df-4830-b41c-5ebb33b764a5
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 63
---
# 管理 Integration Services 服务
    
> **重要说明!!** 本主题论述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 在安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件时，也会安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。 默认情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务已启动，该服务的启动类型已设置为自动。 不过，若要使用该服务来管理已存储的和正在运行的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包，还必须安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
> **注意：**若要直接连接到旧 Integration Services 服务的实例，则必须使用与正在运行 Integration Services 服务的 SQL Server 版本保持一致的 SQL Server Management Studio (SSMS) 版本。 例如，要连接到在 SQL Server 2016 的实例上运行的旧 Integration Services 服务，则必须使用 SQL Server 2016 的 SSMS 版本。 [下载 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。
>
>   在 SSMS 的“连接到服务器”对话框中，不能输入正在运行早期版本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的服务器的名称。 但是，若要管理存储在某远程服务器上的包，则不必连接到该远程服务器上 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的实例。 只需编辑 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件，以便 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 显示存储在远程服务器上的包。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)。  
  
 在一台计算机上可以只安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的一个实例。 该服务并非特定于某个 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。 可以使用正在运行该服务的计算机的名称连接到该服务。  
  
 可以使用以下任一 Microsoft 管理控制台 (MMC) 管理单元来管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务：SQL Server 配置管理器或服务。 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中管理包，必须首先确保该服务已启动。  
  
 默认情况下，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为管理[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的 msdb 数据库中的包，该实例与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 同时安装。 如果未同时安装[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务可配置为管理本地默认[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的 msdb 数据库中的包。 若要管理 [!INCLUDE[ssDE](../../includes/ssde-md.md)]某个命名实例或远程实例中存储的包或 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的多个实例中存储的包，则必须修改该服务的配置文件。 有关详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)。  
  
 默认情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为在该服务停止时停止正在运行的包。 但是， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不会等待包停止，因此，在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务停止后，一些包可能仍在运行。  
  
 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务已停止，可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导、[!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器、执行包实用工具以及 **dtexec** 命令提示实用工具 (dtexec.exe) 继续运行包。 但是，您无法监视正在运行的包。  
  
 默认情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务在 NETWORK SERVICE 帐户的上下文中运行。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将信息写入 Windows 事件日志。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查看服务事件。 也可以通过 Windows 事件查看器查看服务事件。  
  
### 使用“服务”管理单元设置 Integration Services 服务的属性  
  
-   [设置 Integration Services 服务的属性](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
### 查看 Integration Services 服务的服务事件  
  
-   [查看 Integration Services 服务的事件](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
## 另请参阅  
 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)   
 [配置 Integration Services 服务（SSIS 服务）](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)   
 [SQL Server 导入和导出向导](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md)   
 [dtexec 实用工具](../../integration-services/packages/dtexec-utility.md)   
 [项目和包的执行](https://msdn.microsoft.com/library/ms141708(v=sql.130).aspx)  
  
  