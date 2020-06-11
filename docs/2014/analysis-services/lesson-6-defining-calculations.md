---
title: 第6课：定义计算 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e0a1e354-e879-4eb8-bb2b-6c3809e32cb6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5ac7db8cdf02b2d38004aadfe67d0e154fc5d450
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542479"
---
# <a name="lesson-6-defining-calculations"></a>第 6 课：定义计算
  在此课程中，将了解如何定义计算（多维表达式 (MDX) 表达式或脚本）。 计算功能允许您定义计算成员、命名集并执行其他脚本命令，以扩展 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集的功能。 例如，您可以运行脚本命令来定义子多维数据集，然后为该子多维数据集中的单元分配计算。  
  
 在“多维数据集设计器”中定义新的计算时，会将该计算添加到“多维数据集设计器”的“计算”**** 选项卡上的“脚本组织程序”**** 窗格中，并在“计算表达式”**** 窗格中的计算窗体内显示特定计算类型的字段。 计算将按照它们在“脚本组织程序”**** 窗格中列出的顺序执行。 可以重新排列计算，方法是右键单击特定计算，再选择“上移”**** 或“下移”****，或者单击特定的计算，再使用“计算”**** 选项卡的工具栏上的“上移”**** 或“下移”**** 图标。  
  
 在“计算”**** 选项卡上，可以添加新的计算，并在“计算表达式”**** 窗格中的下列视图内查看或编辑现有计算：  
  
-   窗体视图。 此视图以图形格式显示单个命令的表达式和属性。 编辑 MDX 脚本时，表达式框将填充窗体视图。  
  
-   脚本视图。 此视图显示代码编辑器中的所有计算脚本，这让您很容易更改计算脚本。 “计算表达式”**** 窗格在“脚本视图中”时，将隐藏“脚本组织程序”****。 脚本视图提供了彩色编码、括号匹配、自动完成和 MDX 代码区域。 可以展开或折叠 MDX 代码区域，以使编辑更容易。  
  
 若要在“计算表达式”**** 窗格中的这些视图之间进行切换，请在“计算”**** 选项卡的工具栏上单击“窗体视图”**** 或“脚本视图”****。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在任何计算中检测到语法错误，将不会显示窗体视图，直到在脚本视图中将错误纠正。  
  
 还可以使用商业智能向导，将某些计算添加到多维数据集中。 例如，可以使用此向导将时间智能添加到多维数据集中，这意味着为与时间相关的计算（例如，“本期截止到现在”、“移动平均”和“期间到期间”）定义计算成员。 有关详细信息，请参阅 [使用商业智能向导定义时间智能计算](multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)。  
  
> [!IMPORTANT]  
>  在“计算”**** 选项卡上，计算脚本从 CALCULATE 命令开始。 CALCULATE 命令控制多维数据集中的单元的聚合，应当只在需要手动指定多维数据集单元应当如何聚合时，才编辑此命令。  
  
 有关详细信息，请参阅 [计算](multidimensional-models-olap-logical-cube-objects/calculations.md)和 [多维模型中的计算](multidimensional-models/calculations-in-multidimensional-models.md)。  
  
> [!NOTE]  
>  本教程的所有课程中的已完成项目均可以从网上获得。 您可以通过将前一课程的已完成项目作为起始点，跳转到后面的任何课程。 [单击此处](https://go.microsoft.com/fwlink/?LinkID=221866) 可以下载本教程随附的示例项目。  
  
 本课程包含以下任务：  
  
 [定义计算成员](lesson-6-1-defining-calculated-members.md)  
 在此任务中，将了解定义计算成员。  
  
 [定义命名集](lesson-6-2-defining-named-sets.md)  
 在此任务中，将了解定义命名集。  
  
## <a name="next-lesson"></a>下一课  
 [第 7 课：定义关键绩效指标 (KPI)](lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 教程方案](analysis-services-tutorial-scenario.md)   
 [&#40;艾德作品的多维建模教程&#41;](multidimensional-modeling-adventure-works-tutorial.md)   
 [创建命名集](multidimensional-models/create-named-sets.md)   
 [创建计算成员](multidimensional-models/create-calculated-members.md)  
  
  
