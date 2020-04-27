---
title: 将项目部署到 Integration Services Server |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6e9402f4-4d50-49ff-820d-65a77829c4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4e260825532f66205e301628f60d68d93f8e7c04
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059576"
---
# <a name="deploy-projects-to-integration-services-server"></a>Deploy Projects to Integration Services Server
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的当前版本中，您可以将您的项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 通过 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器，您可以使用环境来管理包、运行包以及为包配置运行时值。  
  
 有关环境的详细信息，请参阅 [创建和映射服务器环境](../../2014/integration-services/create-and-map-a-server-environment.md)。  
  
> [!NOTE]  
>  与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的早期版本一样，在当前版本中，您也可以将您的包部署到 SQL Server 实例并且使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务运行和管理包。 您使用包部署模型。 有关详细信息，请参阅[包部署 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)。  
  
 若要将项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器，请完成以下任务：  
  
1.  创建一个 SSISDB 目录（如果尚未创建）。 有关详细信息，请参阅 [创建 SSIS 目录](catalog/ssis-catalog.md)。  
  
2.  通过运行 **“Integration Services 项目转换向导”** 可以将项目转换为项目部署模型。 有关详细信息，请参阅下面的说明： [将项目转换为项目部署模型](#convert)  
  
    -   如果在 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]中创建了项目，默认情况下该项目使用项目部署模型。  
  
    -   如果您在早期版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中创建了项目，则在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中打开项目文件之后，将该项目转换为项目部署模型。  
  
        > [!NOTE]  
        >  如果项目包含一个或多个数据源，则在项目转换完成时删除数据源。 若要创建到项目中的包可共享的数据源的连接，请在项目级别添加连接管理器。 有关详细信息，请参阅 [在包中添加、删除或共享连接管理器](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
         根据您是从 **还是从** 运行 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] “Integration Services 项目转换向导” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，该向导将执行不同的转换任务。  
  
        -   如果您是从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]运行该向导的，则在项目中包含的包将从 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 2005、2008 或 2008 R2 转换为当前版本的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]使用的格式。 原始项目 (.dtproj) 和包 (.dtsx) 文件将升级。  
  
        -   如果你是从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]运行该向导的，则该向导将根据项目中包含的包和配置生成一个项目部署文件 (.ispac)。 原始包 (.dtsx) 文件不升级。  
  
             您可以在该向导的 **“选择目标”** 页中选择一个现有文件或创建一个新文件。  
  
             若要在转换项目时升级包文件，请从 **运行** “Integration Services 项目转换向导” [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 若要单独从项目转换中升级包文件，请从 **中运行** “Integration Services 项目转换向导” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，然后运行 **“SSIS 包升级向导”**。 如果单独升级包文件，请确保您保存了这些更改。 否则，在您将项目转换为项目部署模型时，将不会转换对包的任何未保存的更改。  
  
     有关包升级的详细信息，请参阅 [升级 Integration Services 包](install-windows/upgrade-integration-services-packages.md) 和 [使用 SSIS 包升级向导升级 Integration Services 包](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
3.  将项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。 有关详细信息，请参阅下面的说明：[将项目部署到 Integration Services 服务器](#deploy)。  
  
4.  （可选）创建已部署项目的环境。 有关详细信息，请参阅 [创建和映射服务器环境](../../2014/integration-services/create-and-map-a-server-environment.md)。  
  
##  <a name="to-convert-a-project-to-the-project-deployment-model"></a><a name="convert"></a>将项目转换为项目部署模型  
  
1.  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中打开该项目，然后在解决方案资源管理器中，右键单击该项目并单击“转换为项目部署模型”****。  
  
     \- 或 -  
  
     从 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的对象资源管理器中，右键单击“项目”**** 节点并选择“导入包”****。  
  
2.  完成向导。 有关详细信息，请参阅 [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md)。  
  
##  <a name="to-deploy-a-project-to-the-integration-services-server"></a><a name="deploy"></a>将项目部署到 Integration Services 服务器  
  
1.  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]并打开项目，然后从 **“项目”** 菜单，选择 **“部署”** 以便启动 **“Integration Services 部署向导”**。  
  
     \- 或 -  
  
     在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的对象资源管理器中，展开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] > SSISDB**** 节点，并查找想要部署的项目的项目文件夹。 右键单击“项目”**** 文件夹，然后单击“部署项目”****。  
  
     \- 或 -  
  
     在命令提示符下，从 **%ProgramFiles%\Microsoft SQL Server\110\DTS\Binn** 运行 **isdeploymentwizard.exe**。 在 64 位计算机上， **%ProgramFiles(x86)%\Microsoft SQL Server\100\DTS\Binn**中还有 32 位版本的工具。  
  
2.  在 **“选择源”** 页上，单击 **“项目部署文件”** 以便选择项目的部署文件。  
  
     - 或 -  
  
     单击 **“Integration Services 目录”** 以便选择已部署到 SSISDB 目录的项目。  
  
3.  完成向导。 有关详细信息，请参阅 [Integration Services Deployment Wizard](../../2014/integration-services/integration-services-deployment-wizard.md)。  
  
  
