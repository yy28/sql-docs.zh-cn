---
title: 指定分区和角色部署选项 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
ms.openlocfilehash: f4f2f5bb2f3f39636541d5aea5b931b1dcc72534
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546859"
---
# <a name="specifying-partition-and-role-deployment-options"></a>指定分区和角色部署选项
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导从 d 文件中读取分区和角色部署选项 \<*project name*> 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在生成项目时创建此文件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]当创建 d 文件时，使用当前项目的分区和角色部署选项 \<*project name*> 。 有关配置设置的详细信息，请参阅 [Understanding the Input Files Used to Create the Deployment Script](deployment-script-files-input-used-to-create-deployment-script.md)。  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>检查分区和角色部署选项  
 D 文件中的部署选项 \<*project name*> 包括以下各项：  
  
 **分区部署选项**  
 \<*project name*>D 文件指定是保留还是覆盖目标数据库中的现有分区（默认值）。 如果保留现有分区，则仅部署新的分区，所有现有度量值组的分区和聚合设计均保持不变。  
  
> [!NOTE]  
>  如果删除了分区所在的度量值组，则自动删除该分区。  
  
 **角色部署选项**  
 \<*project name*>D 文件指定下列角色部署选项之一：  
  
-   保留目标数据库中现有的角色和角色成员，仅部署新的角色和角色成员。  
  
-   目标数据库中所有现有的角色和成员将被当前部署的角色和成员替换。  
  
-   保留目标数据库中现有的角色和角色成员，不部署任何新的角色。  
  
-   **请注意** 保留现有角色和成员时，与这些角色关联的权限将重置为无。 安全权限包含在这些权限保护的对象中，而非包含在与这些权限关联的安全角色中。 有关如何通过使用 Analysis Services 部署向导来处理此行为的详细信息，请参阅 Microsoft 知识库中的 "保留角色和成员"。  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>修改分区和角色部署选项  
 可能需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用不同于 d 文件中存储的分区和角色选项来部署项目 \<*project name*> 。 例如，你可能想要保留现有的分区、角色和角色成员，而不是替换 d 文件中所示的所有现有分区、角色和成员。 \<*project name*>  
  
 若要在项目中修改分区和角色的部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您不能在项目中更改分区和角色设置，因为中的 " *\<project name>* **属性页**" 对话框 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 不会显示这些选项。 如果要更改角色和分区的部署选项，则必须在 d 文件本身中更改此信息 \<*project name*> 。 下面的过程介绍如何更改 d 文件中的分区和角色部署选项 \<*project name*> 。  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>在生成了输入文件后更改分区或角色的部署  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，然后在 **“分区和角色部署选项”** 页上，为分区和角色指定新的部署选项。  
  
     -或-  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并将该向导设置为以应答文件模式运行。 （有关应答文件模式的详细信息，请参阅[运行 Analysis Services 部署向导](running-the-analysis-services-deployment-wizard.md)。）  
  
     -或-  
  
-   \<*project name*>在任何文本编辑器中打开 d，并手动更改选项。  
  
## <a name="see-also"></a>另请参阅  
 [指定安装目标](deployment-script-files-specifying-the-installation-target.md)   
 [为解决方案部署指定配置设置](deployment-script-files-solution-deployment-config-settings.md)   
 [指定处理选项](deployment-script-files-specifying-processing-options.md)  
  
  
