---
title: "Integration Services (SSIS) 项目和解决方案 | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.importprojectwizard.f1"
helpviewer_keywords: 
  - "项目 [Integration Services], 创建"
  - "文件夹 [Integration Services], 项目"
  - "文件 [Integration Services], 项目"
  - "文件夹 [Integration Services]"
  - "项目 [Integration Services], 关于项目"
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# Integration Services (SSIS) 项目和解决方案
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 用于开发 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
 将包部署到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区时，使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务来管理包。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务只在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中可用。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../integration-services/service/integration-services-service-ssis-service.md)。 有关包部署的详细信息，请参阅[早期包部署 (SSIS)](../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
 将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器时，您在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用 Transact-SQL 视图和存储过程来管理项目。 有关项目部署的详细信息，请参阅 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)。 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的详细信息，请参阅 [Integration Services (SSIS) 服务器](https://msdn.microsoft.com/library/ms137731.aspx)。  
  
 有关 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的概述，请参阅 [Integration Services (SSIS) 和管理工具](https://msdn.microsoft.com/library/ms140028.aspx)%20and%20Studio%20Environments.md)。  
  
## Integration Services 项目包含包  
 项目是您开发 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的容器。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目可以存储与该包相关的文件并对这些文件进行分组。 例如，项目包括创建特定提取、传输和加载 (ETL) 解决方案所需的文件。  
  
 在创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目之前，应熟悉此类项目的基本内容。 在了解项目包含的内容之后，即可开始创建和使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
## Integration Services 项目中的文件夹  
 下面的关系图显示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中一个 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目中的文件夹。  
  
 ![Integration Services 项目中的文件夹](../integration-services/media/solutionexplorer.gif "Integration Services 项目中的文件夹")  
  
 下表介绍 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中出现的文件夹。  
  
|文件夹|Description|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 包|包含包。 有关详细信息，请参阅 [Integration Services (SSIS) 包](../integration-services/integration-services-ssis-packages.md)。|  
|杂项|包含除包文件以外的文件。|  
  
## Integration Services 项目中的文件  
 向解决方案添加新的或现有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目时， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建具有扩展名 .dtproj 、.dtproj.user 和 .database 的项目文件。  
  
-   *.dtproj 文件包含有关项目配置以及像包这类项的信息。  
  
-   *.dtproj.user 文件包含有关使用项目的首选项的信息。  
  
-   *.database 文件包含 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 打开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目所需的信息。  
  
## Integration Services 项目中面向的版本  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，可以创建、维护和运行面向 SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的包。  
  
 在解决方案资源管理器中，右键单击 Integration Services 项目并选择“属性”以打开该项目的属性页。 在“配置属性”  的“常规” 选项卡上，选择“TargetServerVersion”  属性，然后选择 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
  
 ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
## 解决方案包含项目  
 解决方案是对开发端到端商业解决方案时所使用的项目进行分组和管理的容器。 使用解决方案，您可以将多个项目作为一个单元处理，并将构成商业解决方案的一个或多个相关项目组合在一起。  
  
 解决方案可以包含不同类型的项目。 如果要用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包，请使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的解决方案中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目。  
  
 创建新的解决方案时， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将在解决方案资源管理器中添加一个解决方案文件夹，并创建扩展名为 .sln 和 .suo 的文件：  
  
-   *.sln 文件包含有关解决方案配置的信息，并列出解决方案中的项目。  
  
-   *.suo 文件包含有关使用解决方案的首选项的信息。  
  
 当您创建新项目时 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将自动创建解决方案，但您也可创建空解决方案，然后再添加项目。  
  
> **注意：**默认情况下，在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中创建新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目时，“项目资源管理器”窗格不会显示解决方案。 若要更改此默认行为，请在 **“工具”** 菜单上单击 **“选项”**。 在 **“选项”** 对话框中，展开 **“项目和解决方案”**，然后单击 **“常规”**。 在 **“常规”** 页上，选择 **“总是显示解决方案”**。  
  
## 相关任务  
 [在解决方案中添加或删除 Integration Services 项目](../Topic/Add%20or%20Remove%20an%20Integration%20Services%20Project%20in%20a%20Solution.md)  
  
 [创建新的 Integration Services 项目](../Topic/Create%20a%20New%20Integration%20Services%20Project.md)  
  
 [向 Integration Services 项目添加项](../Topic/Add%20an%20Item%20to%20an%20Integration%20Services%20Project.md)  
  
 [复制项目项](../Topic/Copy%20Project%20Items.md)  
  
## 相关内容  
 [Integration Services 项目的开发](../Topic/Development%20of%20an%20Integration%20Services%20Project.md)  
  
  