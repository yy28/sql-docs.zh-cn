---
title: 项集选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b34031f0554fd9743ba036c9ce0f1bebe2c3d44d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079562"
---
# <a name="itemsets-tab-mining-model-viewer"></a>“项集”选项卡（挖掘模型查看器）
  可以使用 **“项集”** 窗格查看关联规则挖掘模型包含的频繁项集。 由于关联模型可包含多个项集，因此，查看器中提供了一些控件，帮助您筛选在查看器中显示的项集。  
  
 **有关详细信息：** [Microsoft 关联算法](data-mining/microsoft-association-algorithm.md)，[使用 Microsoft 关联规则查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **Viewer**  
 选择用于查看所选挖掘模型的查看器。 可以对关联模型使用自定义查看器，也可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 一般内容树查看器。 还可以使用插件查看器（如果有）。  
  
 **最低支持**  
 更改此值可设置项集要显示在查看器中所必须具有的最低支持。 模型将计算您在首次打开它时显示的默认值，但您可以更改该值以查看更多或更少项集。  
  
 **最小项集大小**  
 更改此值可设置在查看器中可以显示某个项集之前，必须包含在该项集中的项的最小数目。  
  
 **筛选项集**  
 键入一个字符串值可筛选查看器中显示的项集数。  
  
 还可以键入 .NET 正则表达式作为筛选条件。 例如，下面的表达式将返回包含“Road Bottle Cage”的所有项集：  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 请注意，您可能需要刷新视图以查看筛选条件应用情况。 还可以启用和禁用 **“显示长名称”** 选项以刷新列表。  
  
 默认情况下，筛选条件应用于属性-值组合的完整名称；因此，如果您只查看属性名称，则可能无法明确知道已正确应用筛选条件。 使用 **“显示”** 下拉列表可选择 **“显示属性名称和值”** ，并验证是否已正确筛选项集的列表。  
  
 **显示**  
 调整项集在查看器中的显示方式。 可以选择以下三个选项之一：  
  
-   “显示属性名称和值”  
  
-   仅显示属性值  
  
-   仅显示属性名称  
  
 请注意，此选项不会重新查询模型；它仅筛选所显示的属性或值。  
  
 **显示长名称**  
 选择此选项可当项集显示在挖掘模型内容中时显示其全名。  
  
 **最大行数**  
 限制查看器中显示的项集数。 默认情况下，按照支持以降序顺序对项集进行排序，因此，减小此值将限制为仅列出最常用项集。  
  
 **支持**  
 显示对每个项集的支持。  
  
 **大小**  
 显示每个项集中包含的项数。  
  
 **Itemset**  
 显示每个项集的说明。 默认情况下，项集将表示为属性及其值的以逗号分隔的列表。 可以使用 **“显示”** 选项来更改其显示方式。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
