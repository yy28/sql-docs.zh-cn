---
title: 规则选项卡 （挖掘模型查看器） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.rules.f1
ms.assetid: 705d5492-b58f-45d9-94d7-ed57b7025823
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 78c8cb99023f4e28300ff8eb3f8eb27e4884bf0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015329"
---
# <a name="rules-tab-mining-model-viewer"></a>“规则”选项卡（挖掘模型查看器）
  可以使用关联模型中的 **“规则”** 窗格来查看算法从数据中提取的规则。 规则不仅说明了各项之间相互关联的方式，并且可用于创建建议。  
  
 您可以使用查看器中的选项进行筛选以更改查看器中显示的规则数。  
  
> [!WARNING]  
>  默认情况下，查看器中仅显示大于 **“最小概率”** 中定义的概率阈值的规则。 无法使用查看器减小该值，因为规则输出的概率阈值是在创建模型时确定的。 有关详细信息，请参阅 [Microsoft 关联算法技术参考](data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 **有关详细信息：**[Microsoft 关联算法](data-mining/microsoft-association-algorithm.md)、[使用 Microsoft 关联规则查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>“常规”  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于查看所选挖掘模型的查看器。 可以对每个挖掘模型使用自定义查看器，也可以使用 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **最小概率**  
 更改此值可设置在查看器中显示规则所需的最小概率。 增大概率值将减少显示的规则的数目。  
  
 **最低重要性**  
 更改此值可设置在查看器中显示规则所需的最低重要性。 增大重要性的值将减少显示的规则的数目。  
  
 **筛选器规则**  
 键入一个字符串值可筛选查看器中显示的规则数。  
  
 还可以键入 .NET 正则表达式作为筛选条件。 例如，下面的表达式将返回其左侧包含“Road Bottle Cage”的所有规则：  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*->.*`  
  
 请注意，您可能需要刷新视图以查看筛选条件应用情况。 还可以启用和禁用 **“显示长名称”** 选项以刷新列表。  
  
 默认情况下，筛选条件应用于属性-值组合的完整名称；因此，如果您只查看属性名称，则可能无法明确知道已正确应用筛选条件。 使用 **“显示”** 下拉列表可选择 **“显示属性名称和值”**，并验证是否已正确筛选项集的列表。  
  
 **显示**  
 调整规则在查看器中的显示方式。 可以选择以下三个选项之一：  
  
-   显示属性名称和值  
  
-   仅显示属性值  
  
-   仅显示属性名称  
  
 **显示长名称**  
 当规则显示在挖掘模型内容中时显示其全名。  
  
 **最大行数**  
 限制查看器中显示的规则数。  
  
 **概率**  
 此列将在图表中显示每个规则的概率。  
  
 可以单击列标题来按概率进行排序。  
  
 **重要性**  
 此列将在图表中显示每个规则的重要性。  
  
 可以单击列标题来按重要性进行排序。  
  
 **规则**  
 此列将在图表中显示每个规则的文本说明，具体取决于使用选项“显示”和“显示长名称”指定的格式。  
  
 可以单击列标题来按规则的文本进行排序。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器&#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  