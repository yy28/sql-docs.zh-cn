---
title: 多维建模 （Adventure Works 教程） |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def2d0f3b09fd7f78b499ed64b83661e6e51f690
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>多维建模（Adventure Works 教程）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

欢迎使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程。 本教程通过在所有示例中使用虚构公司 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ，说明如何使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 开发和部署 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 项目。  
  
## <a name="what-you-learn"></a>你掌握的内容  
在本教程中，您将了解以下内容：  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]项目中定义数据源、数据源视图、维度、属性、属性关系、层次结构和多维数据集。  
  
-   如何通过将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例来查看多维数据集和维度数据，以及如何在随后处理已部署的对象以使用基础数据源中的数据来填充对象。  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中修改度量值、维度、层次结构、属性和度量值组，以及如何将增量更改部署到开发服务器上的已部署多维数据集。  
  
-   如何定义多维数据集内的计算、关键绩效指标 (KPI)、操作、透视、翻译和安全角色。  
  
在此教程中随附应用场景说明，以便您可以更好地理解这些课程的上下文。 有关详细信息，请参阅 [Analysis Services Tutorial Scenario](../analysis-services/analysis-services-tutorial-scenario.md)。  
  
## <a name="prerequisites"></a>先决条件  
要完成本教程的所有课程，您将需要示例数据、示例项目文件以及软件。 有关如何查找和安装本教程的必备组件的说明，请参阅 [安装 Analysis Services 多维建模教程的示例数据和项目](../analysis-services/install-sample-data-and-projects.md)。  
  
此外，必须具有下列权限才能成功完成本教程：  
  
-   您必须是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 计算机上本地管理员组的成员或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例中的服务器管理角色的成员。  
  
-   您必须具有读取权限**AdventureWorksDW**示例数据库。 此示例数据库对于 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本有效。  
  
## <a name="lessons"></a>课程  
本教程包括以下几课。  
  
|课程|学完本课的估计时间|  
|----------|------------------------------|  
|[第 1 课： 定义数据源视图中分析服务项目](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 分钟|  
|[第 2 课︰ 定义和部署多维数据集](../analysis-services/lesson-2-defining-and-deploying-a-cube.md)|30 分钟|  
|[第 3 课︰ 修改度量值、 属性和层次结构](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 分钟|  
|[第 4 课： 定义高级的属性和维度属性](../analysis-services/lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 分钟|  
|[第 5 课： 定义维度和度量值组之间的关系](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 分钟|  
|[第 6 课： 定义计算](../analysis-services/lesson-6-defining-calculations.md)|45 分钟|  
|[第 7 课： 定义关键绩效指标 & #40;Kpi & #41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)|30 分钟|  
|[第 8 课： 定义操作](../analysis-services/lesson-8-defining-actions.md)|30 分钟|  
|[Lesson 9: Defining Perspectives and Translations](../analysis-services/lesson-9-defining-perspectives-and-translations.md)|30 分钟|  
|[第 10 课： 定义管理角色](../analysis-services/lesson-10-defining-administrative-roles.md)|15 分钟|  
  
> [!NOTE]  
> 将在本教程中创建的多维数据集数据库是的简化的版本[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]是可用于在 GitHub 上的下载的 Adventure Works 示例数据库的一部分的多维模型项目。 对 Adventure Works 多维数据库的教程版本进行了简化，以便重点关注您将要立即掌握的特定技能。 在完成该教程后，请考虑自己探索该多维模型项目，以便进一步理解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维建模。  
  
## <a name="next-step"></a>下一步  
要开始学习本教程，请转到第一课： [第 1 课：在 Analysis Services 项目中定义数据源视图](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)。  
  
  
  
