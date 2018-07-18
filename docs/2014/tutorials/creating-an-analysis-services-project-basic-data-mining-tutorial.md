---
title: 创建 Analysis Services 项目 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
caps.latest.revision: 50
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7f191090750d9a4417b6432ce31f24f3214376b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260113"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>创建 Analysis Services 项目（数据挖掘基础教程）
  每个[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]项目定义的对象在单个[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。 一个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库可以包含很多不同类型的对象  
  
-   多维模型（多维数据集）  
  
-   挖掘结构和挖掘模型  
  
-   支持各种对象，如数据源、数据源视图和自定义程序集  
  
 请注意您 **不** 需要有多维数据集就可以进行数据挖掘。 如果您需要对现有多维数据集执行数据挖掘，应将数据挖掘模型添加到用于生成多维数据集的同一项目。 但是，对于大多数用途，您可以针对关系数据源（如数据仓库）生成模型，如果不涉及多维数据集，将获得更好的性能。  
  
 在本教程中，您将使用关系数据仓库[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]，作为数据源。 将部署到所有数据挖掘对象[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]名为数据库`BasicDataMining`、 仅用于数据挖掘。  
  
 默认情况下[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]使用**localhost**为新项目实例。 如果使用命名实例或者另一台服务器，则必须首先创建和打开该项目，然后更改实例名称。  
  
 有关详细信息[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]项目，请参阅[创建 Analysis Services 项目](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md)。  
  
### <a name="to-create-an-analysis-services-project"></a>创建 Analysis Services 项目  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，然后选择 **“项目”**。  
  
3.  确保已选中 **“项目类型”** 窗格中的 **“商业智能项目”** 。  
  
4.  在 **“模板”** 窗格中选择 **“Analysis Services 多维和数据挖掘项目”**。  
  
5.  在中**名称**框中，将新项目命名`BasicDataMining`。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>更改存储数据挖掘对象的实例  
  
1.  在中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，然后在**项目**菜单中，选择**属性**。  
  
2.  在 **“属性页”** 窗格左侧的 **“配置属性”** 下，单击 **“部署”**。  
  
3.  在 **“属性页”** 窗格右侧的 **“目标”** 下，确保 **“服务器”** 名称为 **localhost**。 如果使用的是其他实例，请键入该实例的名称。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建数据源&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [生成 Analysis Services 项目&#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [创建 Analysis Services 项目 (SSDT)](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
