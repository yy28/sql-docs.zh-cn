---
title: 指定分区和角色部署选项 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 01cab4f372335ddeb2f3798b635b661c5469b43c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>部署脚本文件的分区和角色部署选项
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导读取从分区和角色部署选项\<*项目名称*>.deploymentoptions 文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]生成时创建此文件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用分区和角色部署选项的当前项目时\<*项目名称*> 创建.deploymentoptions 文件。 有关配置设置的详细信息，请参阅 [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)。  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>检查分区和角色部署选项  
 部署选项中\<*项目名称*>.deploymentoptions 文件包括以下：  
  
 **分区部署选项**  
 \<*项目名称*>.deploymentoptions 文件指定是否保留目标数据库中的现有分区或覆盖 （默认值）。 如果保留现有分区，则仅部署新的分区，所有现有度量值组的分区和聚合设计均保持不变。  
  
> [!NOTE]  
>  如果删除了分区所在的度量值组，则自动删除该分区。  
  
 **角色部署选项**  
 \<*项目名称*>.deploymentoptions 文件指定以下角色部署选项之一：  
  
-   保留目标数据库中现有的角色和角色成员，仅部署新的角色和角色成员。  
  
-   目标数据库中所有现有的角色和成员将被当前部署的角色和成员替换。  
  
-   保留目标数据库中现有的角色和角色成员，不部署任何新的角色。  
  
-   **请注意** 保留现有角色和成员时，与这些角色关联的权限将重置为无。 安全权限包含在这些权限保护的对象中，而非包含在与这些权限关联的安全角色中。 有关如何通过使用 Analysis Service 部署指南处理此行为的详细信息，请参阅 Microsoft 知识库中的“保留角色和成员”。  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>修改分区和角色部署选项  
 你可能需要部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目使用比存储在不同的分区和角色选项\<*项目名称*>.deploymentoptions 文件。 例如，你可能想要保留现有分区、 角色和角色成员，而不是替换所有现有分区、 角色和成员中所示\<*项目名称*>.deploymentoptions 文件。  
  
 若要修改的分区和角色中的部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目中，你无法更改项目中的分区和角色设置，因为*\<项目名称 >* **属性页**中的对话框[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]不会显示这些选项。 如果你想要更改角色和分区的部署选项，则必须更改中的此信息\<*项目名称*>.deploymentoptions 文件本身。 以下过程介绍如何更改中的分区和角色部署选项\<*项目名称*>.deploymentoptions 文件。  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>在生成了输入文件后更改分区或角色的部署  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，然后在 **“分区和角色部署选项”** 页上，为分区和角色指定新的部署选项。  
  
     — 或 —  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并将该向导设置为以应答文件模式运行。 （有关应答文件模式的详细信息，请参阅 [运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。）  
  
     — 或 —  
  
-   打开\<*项目名称*>.deploymentoptions 在任何文本编辑器并手动更改的选项。  
  
## <a name="see-also"></a>另请参阅  
 [指定安装目标](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [指定解决方案部署的配置的设置](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [指定处理选项](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
