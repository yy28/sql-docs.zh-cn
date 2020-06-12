---
title: "\"分类配置文件\" 选项卡（挖掘模型查看器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 31620135818f77db11938c67059319932e98fc51
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527433"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>“分类剖面图”选项卡（挖掘模型查看器）
  可以使用 **“分类剖面图”** 选项卡，提供算法在分类模型中发现的分类的总体视图。 该选项卡可显示每个属性及其在每个分类中的分布情况。  
  
 **有关详细信息，请参阅 ** [Microsoft 聚类分析算法](data-mining/microsoft-clustering-algorithm.md)和[使用 Microsoft 分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于查看所选挖掘模型的查看器。 可以对挖掘模型使用自定义查看器，也可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **显示图例**  
 选择此选项可显示一个键，该键将显示查看器中的颜色与“状态”**** 列中的值之间的映射。  
  
 **直方图条**  
 更改此值可控制每个直方图中包含的状态的数目。 如果存在的状态数多于您选择显示的状态数，则直方图中将显示概率最高的状态，其余状态则组合到 **“其他”** 中。  
  
 **特性**  
 列出分类模型中包含的列。 每个属性的直方图均演示该属性在算法所标识的分类中的分布方式。  
  
 **状态**  
 提供一个键，用于指示代表分类的对应行中的每个状态的颜色，或提供一个菱形滑块，用于指示连续数值的分布。 可以使用 **“显示图例”** 复选框来显示或隐藏此列。  
  
 **分类剖面图**  
 本节对于模型中的每个分类都包含一个列。 对于每个属性，直方图显示该属性的值相对于相应分类的分布情况。 此图表还包含一个 **“总体”** 列，该列也会使用直方图来显示每个属性的值的分布情况（但针对的是模型中的事例）。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
