---
title: 了解用于创建部署脚本的输入文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2eb377b29ef798b4cbdd02666b866c52eb8f8599
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546869"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>了解用于创建部署脚本的输入文件
  生成 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将为该项目生成 XML 文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将这些 XML 文件放在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的输出文件夹中。 默认情况下，输出将输出到 \Bin 文件夹之中。 下表列出了 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 创建的 XML 文件。  
  
|XMLA 文件|说明|  
|---------------|-----------------|  
|\<*project name*>。 .asdatabase|包含项目中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的声明性定义。|  
|\<*project name*>。 .deploymenttargets|包含将在其中创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库的名称。|  
|\<*project name*>。 .configsettings|包含特定于环境的设置，如数据源连接信息和对象存储位置。 此文件中的设置将替代 .asdatabase 文件中的设置 \<*project name*> 。|  
|\<*project name*>。 d|包含部署选项，例如部署是否是事务性的，以及是否在部署后处理已部署的对象。|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 从不在其项目文件中存储密码。  
  
## <a name="modifying-the-input-files"></a>修改输入文件  
 如果修改输入文件中的值或从输入文件中检索的值，则可以更改部署目标、配置设置和部署选项，而无需编辑整个 \<*project name*> .asdatabase 文件（如果从现有数据库生成脚本，则可以更改整个 XMLA 脚本文件 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ）。 能够修改各个文件使您可以轻松地创建用于不同用途的不同部署脚本。  
  
 以下主题解释了如何修改各个输入文件中的值：  
  
-   [指定安装目标](deployment-script-files-specifying-the-installation-target.md)  
  
-   [指定分区和角色部署选项](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [为解决方案部署指定配置设置](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [指定处理选项](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>另请参阅  
 [运行 Analysis Services 部署向导](running-the-analysis-services-deployment-wizard.md)   
 [了解 Analysis Services 部署脚本](understanding-the-analysis-services-deployment-script.md)  
  
  
