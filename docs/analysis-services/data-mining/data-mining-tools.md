---
title: "数据挖掘工具 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tools [Analysis Services]
- mining models [Analysis Services], tools
- data mining [Analysis Services], tools
- data mining [Analysis Services], development
ms.assetid: 003ada6a-0bcd-4f16-8c34-1a9ffc75cd2c
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 130c8098a7083019671b3b799246b16757fd1b5b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-tools"></a>数据挖掘工具
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供了以下工具，可用于创建数据挖掘解决方案：  
  
-   利用 **中的** 数据挖掘向导 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，可以使用关系数据源或多维数据集中的多维数据来轻松创建挖掘结构和挖掘模型。  
  
     在该向导中，您可以选择要使用的数据，然后应用特定的数据挖掘技术，如聚类分析、神经网络或时序建模。  
  
-    和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都提供了模型查看器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，可用于在创建挖掘模型后对其进行浏览。  可以使用为每种算法定制的查看器来浏览模型，或使用模型内容查看器进行更深入的分析。  
  
-    和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都提供了预测查询生成器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，可帮助您创建预测查询。 还可以针对维持数据集或外部数据来测试模型的准确性，或使用交叉验证来评估数据集的质量。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是一个接口，可用于管理已部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的现有数据挖掘解决方案。 可以重新处理结构和模型以更新其包含的数据。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含了一些工具，可用于清除数据﹑自动完成任务（如创建预测和更新模型）以及创建文本挖掘解决方案。  
  
 下面详细地介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据挖掘工具。  
  
## <a name="data-mining-wizard"></a>中的  
 可使用数据挖掘向导开始创建数据挖掘解决方案。 该向导简单易用，可指导您完成创建数据挖掘结构和初始相关挖掘模型的过程，其中包括选择算法类型和数据源以及定义用于分析的事例数据等任务。  
  
 **有关详细信息：**[数据挖掘向导（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Data Mining Designer  
 在使用数据挖掘向导创建挖掘结构和挖掘模型后，您可以从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用数据挖掘设计器来处理现有模型和结构。  
  
 该设计器包含用于执行以下任务的工具：  
  
-   修改挖掘结构的属性，添加列并创建列别名，更改值的装箱方法或预期分布。  
  
-   向现有结构中添加新模型；复制模型，更改模型属性或元数据，或定义挖掘模型的筛选器。  
  
-   浏览模型中的模式和规则；浏览关联或决策树。 获取有关为  
  
     每个不同的模型时间提供的自定义查看器的详细统计信息，以帮助您分析数据和浏览数据挖掘所显示的模式。  
  
-   通过创建提升图或分析模型的利润曲线来验证模型。 使用分类矩阵比较模型，或使用交叉验证来验证数据集及其模型。  
  
-   创建针对现有挖掘模型的预测和内容查询。 生成一次性查询，或设置用于为整个外部数据表生成预测的查询。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 在创建挖掘模型并将其部署到服务器之后，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来管理承载数据挖掘对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 也可以继续执行使用模型的任务，如浏览模型、处理新数据和创建预测。  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 还包含查询编辑器，可用于设计和执行数据挖掘扩展插件 (DMX) 查询或用于通过使用 XMLA 来处理数据挖掘对象。  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Integration Services 数据挖掘任务和转换  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了多个支持数据挖掘的组件。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的一些工具旨在帮助自动执行常见数据挖掘任务，包括预测、建模和处理。 例如：  
  
-   创建一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，每当用新客户更新数据集时，该包会自动更新模型。  
  
-   对事例记录进行自定义分段或自定义采样。  
  
-   自动生成通过参数传递的模型。  
  
 但是，您还可以在包工作流中将数据挖掘用作其他进程的输入。 例如：  
  
-   使用模型所生成的概率值来加权文本挖掘或其他分类任务的分数。  
  
-   基于之前的数据自动生成预测，并使用这些值来评估新数据的有效性。  
  
-   使用逻辑回归按风险划分传入客户。  
  
 **有关详细信息：**[数据挖掘解决方案的相关项目](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 (DMX) 参考](../../dmx/data-mining-extensions-dmx-reference.md)   
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
