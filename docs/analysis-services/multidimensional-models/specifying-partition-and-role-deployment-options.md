---
title: "指定分区和角色部署选项 | Microsoft Docs"
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
  - "分区 [Analysis Services], 部署选项"
  - "Analysis Services 部署, 角色"
  - "Analysis Services 部署, 分区"
  - "Analysis Services 部署向导, 角色"
  - "Analysis Services 部署向导, 分区"
  - "部署 [Analysis Services], 角色"
  - "角色 [Analysis Services], 部署选项"
  - "部署 [Analysis Services], 分区"
  - "修改角色部署"
  - "修改分区部署"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 指定分区和角色部署选项
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导从 \<项目名称>.deploymentoptions 文件中读取分区和角色部署选项。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 在生成时创建此文件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 创建 \<项目名称>.deploymentoptions 文件时，使用当前项目的分区和角色部署选项。 有关配置设置的详细信息，请参阅 [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)。  
  
## 检查分区和角色部署选项  
 \<项目名称>.deploymentoptions 文件包括下列部署选项：  
  
 **分区部署选项**  
 \<项目名称>.deploymentoptions 文件指定了是保留还是覆盖（默认值）目标数据库中的现有分区。 如果保留现有分区，则仅部署新的分区，所有现有度量值组的分区和聚合设计均保持不变。  
  
> [!NOTE]  
>  如果删除了分区所在的度量值组，则自动删除该分区。  
  
 **角色部署选项**  
 \<项目名称>.deploymentoptions 文件指定了下列角色部署选项之一：  
  
-   保留目标数据库中现有的角色和角色成员，仅部署新的角色和角色成员。  
  
-   目标数据库中所有现有的角色和成员将被当前部署的角色和成员替换。  
  
-   保留目标数据库中现有的角色和角色成员，不部署任何新的角色。  
  
-   **请注意** 保留现有角色和成员时，与这些角色关联的权限将重置为无。 安全权限包含在这些权限保护的对象中，而非包含在与这些权限关联的安全角色中。 有关如何通过使用 Analysis Service 部署指南处理此行为的详细信息，请参阅 Microsoft 知识库中的“保留角色和成员”。  
  
## 修改分区和角色部署选项  
 可能必须使用与 \<项目名称>.deploymentoptions 文件中存储的选项不同的分区和角色选项来部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。 例如，你可能想保留现有的分区、角色和角色成员，而不是替换 \<项目名称>.deploymentoptions 文件中所示的所有现有分区、角色和成员。  
  
 若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中修改分区和角色的部署，则不能在项目内更改分区和角色设置，因为 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“\<项目名称>属性页”对话框不会显示这些选项。 如果要更改角色和分区的部署选项，则必须在 \<项目名称>.deploymentoptions 文件中更改这一信息。 以下步骤介绍如何在 \<项目名称>.deploymentoptions 文件中更改分区和角色部署选项。  
  
#### 在生成了输入文件后更改分区或角色的部署  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，然后在 **“分区和角色部署选项”** 页上，为分区和角色指定新的部署选项。  
  
     — 或 —  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并将该向导设置为以应答文件模式运行。 （有关应答文件模式的详细信息，请参阅 [运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。）  
  
     — 或 —  
  
-   在任何文本编辑器中打开 \<项目名称>.deploymentoptions，再手动更改选项。  
  
## 另请参阅  
 [指定安装目标](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [为解决方案部署指定配置设置](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [指定处理选项](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  