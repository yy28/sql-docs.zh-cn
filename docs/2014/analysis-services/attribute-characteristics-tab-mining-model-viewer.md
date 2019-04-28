---
title: 属性特征选项卡 （挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.characteristics.f1
ms.assetid: f0c3350d-84c0-4ab8-9fb8-1527c2647299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 724ac86a4566bac4647e8e7358608c0f5e4ccd85
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650708"
---
# <a name="attribute-characteristics-tab-mining-model-viewer"></a>“属性特征”选项卡（挖掘模型查看器）
  可以使用 **“属性特征”** 窗格浏览 Naïve Bayes 模型中结果和输入属性之间的关系。 可以选择目标属性的值，然后查看对结果产生的影响最大的输入属性的列表。  
  
 **有关详细信息：**[Microsoft Naive Bayes 算法](data-mining/microsoft-naive-bayes-algorithm.md)，[使用 Microsoft Naive Bayes 查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的模型中选择一个挖掘模型以进行查看。 挖掘模型将自动在最适用于所选特定类型的模型的自定义查看器中打开。  
  
 **Viewer**  
 选择用于浏览所选挖掘模型的查看器。 对于每个模型，您可以选择自定义查看器或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 插件查看器也将出现在此列表中（如果有）。  
  
 **Attribute**  
 选择要分析的可预测属性。  
  
 **ReplTest1**  
 选择在“属性”中设置的可预测属性的状态。 由于 Naïve Bayes 模型不支持连续变量，因此，所有目标属性都包含离散或离散化结果。 始终会自动将 Missing 属性添加到列表。  
  
 **特征\<可预测状态 >**  
 图形包含以下列，这些列对输入属性状态与所选可预测属性状态之间的关系进行了说明：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**变量**|列出挖掘模型中的输入属性。|  
|**值**|列出 **“变量”** 中每个输入属性状态。|  
|**概率**|条形表示该行中的属性和值与可预测属性的选定状态相关联的概率。 将鼠标指针悬停在条形上方可查看以百分比表示的概率。|  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器（数据挖掘模型设计器）](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
