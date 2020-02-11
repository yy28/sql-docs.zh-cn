---
title: 创建部署实用工具 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- deploying packages [Integration Services], deployment utility
- deployment utility [Integration Services]
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e5f7959496cfa2b473fbf5c500f424647df0a1c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060232"
---
# <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  部署包的第一步是为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目创建一个部署实用工具。 部署实用工具是一个文件夹，其中包含在不同服务器上部署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中的包所需的文件。 部署实用工具是在存储 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的计算机上创建的。  
  
 通过首先配置创建部署实用工具的生成过程，然后生成 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，可以为该项目创建一个包部署实用工具。 在生成项目时，将自动包括项目中的所有包和包配置。 若要部署其他文件（如项目的自述文件），请将这些文件放在 **项目的** “杂项” [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 文件夹中。 当生成项目时，也会自动包括这些文件。  
  
 您可以按照不同的方式配置每个项目部署。 在生成项目和创建包部署实用工具之前，您可以设置部署实用工具的属性，自定义项目中包的部署方法。 例如，您可以指定在部署项目时是否可以更新包配置。 若要访问 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的属性，请右键单击该项目，再单击****“属性”。  
  
 下表列出了部署实用工具属性。  
  
|properties|说明|  
|--------------|-----------------|  
|AllowConfigurationChange|一个指定在部署过程中是否可以更新配置的值。|  
|CreateDeploymentUtility|一个指定在生成项目时是否创建包部署实用工具的值。 此属性必须为 `True` 才能创建部署实用工具。|  
|DeploymentOutputPath|部署实用工具的位置，相对于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。|  
  
 在生成 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目时，除了创建项目包的副本和包依赖项外，还会创建一个清单文件 \<project name>.SSISDeploymentManifest.xml，并将它们都添加到项目的 bin\Deployment 文件夹中，或添加到 DeploymentOutputPath 属性中所指定的位置。 该清单文件列出了项目中的包、包配置和所有杂项文件。  
  
 每次生成项目时将刷新部署文件夹的内容。 这意味着系统将删除所有已保存到此文件夹中但未由生成进程再次复制到该文件夹中的文件。 例如，将删除保存到部署文件夹中的包配置文件。  
  
### <a name="to-create-a-package-deployment-utility"></a>创建包部署实用工具  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含要为其创建包部署实用工具的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的解决方案。  
  
2.  右键单击该项目，再单击“属性”****。  
  
3.  在** \<项目名称> 属性页**"对话框中，单击"**部署实用工具**"。  
  
4.  若要在部署包时更新包配置，请**** 将 AllowConfigurationChanges `True`设置为。  
  
5.  将 `CreateDeploymentUtility` 设置为 `True`。  
  
6.  还可以通过修改 `DeploymentOutputPath` 属性来更新部署实用工具的位置。  
  
7.  单击“确定”。   
  
8.  在解决方案资源管理器中，右键单击该项目，再单击****“生成”。  
  
9. 在 **“输出”** 窗口中查看生成进度和生成错误。  
  
## <a name="see-also"></a>另请参阅  
 [包配置](../../2014/integration-services/package-configurations.md)   
 [创建包配置](../../2014/integration-services/create-package-configurations.md)   
 [使用部署实用工具部署包](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)   
 [包部署 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
