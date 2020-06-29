---
title: Integration Services （SSIS）项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 21c87a2b8697c3c9e83bc82edac79dacd3481b35
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436404"
---
# <a name="integration-services-ssis-projects"></a>Integration Services (SSIS) 项目
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 用于开发 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。

 将包部署到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 包存储区时，可以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务来管理包。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务只在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中可用。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](service/integration-services-service-ssis-service.md)。 有关包部署的详细信息，请参阅[包部署 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)。

 将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器时，您在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用 Transact-SQL 视图和存储过程来管理项目。 有关项目部署的详细信息，请参阅 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)。 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的详细信息，请参阅 [Integration Services (SSIS) 服务器](catalog/integration-services-ssis-server-and-catalog.md)。

 有关 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的概述，请参阅 [Integration Services (SSIS) 和 Studio 环境](integration-services-ssis-development-and-management-tools.md)。

## <a name="understanding-integration-services-projects"></a>了解 Integration Services 项目
 项目是您开发 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的容器。

 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目可以存储与该包相关的文件并对这些文件进行分组。 例如，项目包括创建特定提取、传输和加载 (ETL) 解决方案所需的文件。

 在创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目之前，应熟悉此类项目的基本内容。 在了解项目包含的内容之后，即可开始创建和使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。

### <a name="folders-in-integration-services-projects"></a>Integration Services 项目中的文件夹
 下面的关系图显示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中一个 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目中的文件夹。

 ![集成服务项目中的文件夹](media/solutionexplorer.gif "集成服务项目中的文件夹")

 下表介绍 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中出现的文件夹。

|Folder|说明|
|------------|-----------------|
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 包|包含包。 有关详细信息，请参阅 [Integration Services (SSIS) 包](../../2014/integration-services/integration-services-ssis-packages.md)。|
|杂项|包含除包文件以外的文件。|

### <a name="files-in-integration-services-projects"></a>Integration Services 项目中的文件
 向解决方案添加新的或现有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目时， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 创建具有扩展名 .dtproj 、.dtproj.user 和 .database 的项目文件。

-   *.dtproj 文件包含有关项目配置以及像包这类项的信息。

-   *.dtproj.user 文件包含有关使用项目的首选项的信息。

-   *.database 文件包含 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 打开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目所需的信息。

## <a name="understanding-solutions"></a>了解解决方案
 解决方案是对开发端到端商业解决方案时所使用的项目进行分组和管理的容器。 使用解决方案，您可以将多个项目作为一个单元处理，并将构成商业解决方案的一个或多个相关项目组合在一起。

 解决方案可以包含不同类型的项目。 如果要用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包，请使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的解决方案中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目。

 创建新的解决方案时， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将在解决方案资源管理器中添加一个解决方案文件夹，并创建扩展名为 .sln 和 .suo 的文件：

-   *.sln 文件包含有关解决方案配置的信息，并列出解决方案中的项目。

-   *.suo 文件包含有关使用解决方案的首选项的信息。

 当您创建新项目时 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将自动创建解决方案，但您也可创建空解决方案，然后再添加项目。

> [!NOTE]
>  默认情况下，在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中创建新 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]项目时， **“项目资源管理器”** 窗格不会显示解决方案。 若要更改此默认行为，请在 **“工具”** 菜单上单击 **“选项”**。 在 **“选项”** 对话框中，展开 **“项目和解决方案”**，然后单击 **“常规”**。 在 **“常规”** 页上，选择 **“总是显示解决方案”**。

## <a name="related-tasks"></a>Related Tasks
 [在解决方案中添加或删除 Integration Services 项目](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)

 [创建新的 Integration Services 项目](../../2014/integration-services/create-a-new-integration-services-project.md)

 [向 Integration Services 项目添加项](../../2014/integration-services/add-an-item-to-an-integration-services-project.md)

 [复制项目项](../../2014/integration-services/copy-project-items.md)

## <a name="related-content"></a>相关内容
 [Integration Services 项目的开发](../../2014/integration-services/development-of-an-integration-services-project.md)


