---
title: "了解用于创建部署脚本的输入文件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "输入文件 [Analysis Services]"
  - "Analysis Services 部署向导，脚本"
  - "部署 [Analysis Services]，输入文件"
  - "Analysis Services 部署向导，输入文件"
  - "脚本 [Analysis Services]，部署"
  - "Analysis Services 部署，输入文件"
  - "修改输入文件"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 了解用于创建部署脚本的输入文件
  在生成 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将为该项目生成 XML 文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将这些 XML 文件放在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的输出文件夹中。 默认情况下，输出将输出到 \\Bin 文件夹之中。 下表列出了 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 创建的 XML 文件。  
  
|XMLA 文件|Description|  
|---------------|-----------------|  
|\<*项目名称*\>.asdatabase|包含项目中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的声明性定义。|  
|\<*项目名称*\>.deploymenttargets|包含将在其中创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库的名称。|  
|\<*项目名称*\>.configsettings|包含特定于环境的设置，如数据源连接信息和对象存储位置。 此文件中的设置将覆盖 \<*项目名称*\>.asdatabase 文件中的设置。|  
|\<*项目名称*\>.deploymentoptions|包含部署选项，例如部署是否是事务性的，以及是否在部署后处理已部署的对象。|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 从不在其项目文件中存储密码。  
  
## 修改输入文件  
 通过修改输入文件中的值或修改从输入文件中检索的值，无需编辑整个 \<*项目名称*\>.asdatabase 文件\(或整个 XMLA 脚本文件，如果你基于现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库\)生成脚本，就可以更改部署目标、配置设置和部署选项。 能够修改各个文件使您可以轻松地创建用于不同用途的不同部署脚本。  
  
 以下主题解释了如何修改各个输入文件中的值：  
  
-   [指定安装目标](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [指定分区和角色部署选项](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [为解决方案部署指定配置设置](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [指定处理选项](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## 另请参阅  
 [运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解 Analysis Services 部署脚本](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  