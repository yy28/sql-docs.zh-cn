---
title: "了解用于创建部署脚本的输入的文件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dcf9b0c4869542727ed8e29699cddaada4c60e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>部署脚本文件-输入用于创建部署脚本
  当生成[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]生成的项目文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]将这些文件放入的输出文件夹[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。 默认情况下，输出将输出到 \Bin 文件夹之中。 下表列出了 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 创建的 XML 文件。  
  
|文件|Description|  
|---------------|-----------------|  
|\<*项目名称*>.asdatabase|用于多维或 1100年/1103年表格模型项目的 XMLA 文件或表格 1200年和更高版本的模型项目的 JSON 文件。 包含项目中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的声明性定义。|  
|\<*项目名称*>.deploymenttargets|包含将在其中创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库的名称。|  
|\<*项目名称*>.configsettings|包含特定于环境的设置，如数据源连接信息和对象存储位置。 此文件中的设置重写中的设置\<*项目名称*>.asdatabase 文件。|  
|\<*项目名称*>.deploymentoptions|包含部署选项，例如部署是否是事务性的，以及是否在部署后处理已部署的对象。|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 从不在其项目文件中存储密码。  
  
## <a name="modifying-the-input-files"></a>修改输入文件  
 修改输入文件中中的值或从输入文件中，检索到的值使成为可能更改的部署目标，配置设置，并且部署选项而无需编辑整个\<*项目名称*>.asdatabase 文件 (或整个脚本文件，如果从现有生成脚本[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库)。 能够修改各个文件使您可以轻松地创建用于不同用途的不同部署脚本。  
  
 以下主题解释了如何修改各个输入文件中的值：  
  
-   [指定安装目标](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [指定分区和角色部署选项](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [为解决方案部署指定配置设置](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [指定处理选项](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>另请参阅  
 [运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解 Analysis Services 部署脚本](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  

