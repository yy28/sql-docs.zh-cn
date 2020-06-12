---
title: 神经网络（挖掘模型查看器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.neuralnet.f1
ms.assetid: 18d87e7b-a821-40ea-9bd8-c6fecf189a1c
author: minewiskan
ms.author: owend
ms.openlocfilehash: d69c7efb919a01e6e9d704c4f0fe2ef3d7c25799
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541159"
---
# <a name="neural-network-mining-model-viewer"></a>神经网络（挖掘模型查看器）
  可以使用 **“神经网络”** 查看器浏览基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 神经网络算法或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 逻辑回归算法的挖掘模型。  
  
 **有关详细信息：** [Microsoft 神经网络算法](data-mining/microsoft-neural-network-algorithm.md)、[Microsoft 逻辑回归算法](data-mining/microsoft-logistic-regression-algorithm.md)、[使用 Microsoft 神经网络查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型以进行查看。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览所选挖掘模型的查看器。 您可以使用自定义查看器或 **“Microsoft 一般内容树查看器”**。 还可以使用插件查看器（如果有）。  
  
 **输入**  
 使用此区域可选择输入属性和值，以便您稍后能浏览它们影响结果的方式。  
  
|值|说明|  
|-----------|-----------------|  
|**特性**|从列表中选择输入属性。 如果将选定内容保留为默认值， **\<All>** 则图表将显示所有输入属性的列表（按其对可预测属性的影响进行排名）。|  
|**值**|为输入属性选择值。|  
  
 **输出**  
 使用这些控件可选择一个可预测属性和值，以在条形图中进行分析和比较。 如果您不更改选定内容，则条形图将比较最上面的两个结果状态。  
  
|值|说明|  
|-----------|-----------------|  
|**输出属性**|选择一个可预测属性。 如果您在创建模型时未将列定义为可预测列，则无法在此处添加列。|  
|**值 1**|选择可预测属性的状态以与 **“值 2”** 中所包含状态进行比较。<br /><br /> 可以比较任意两个离散或离散化值；但您无法像在其他查看器中一样，将一个值与其补数进行比较。|  
|**值 2**|选择可预测属性的状态以与 **“值 1”** 中所包含状态进行比较。|  
  
 **变量**  
 “神经网络”**** 选项卡的此部分包含一个交互条形图，该图会对你选择的输入和结果属性进行响应。 由于神经网络会计算某个特定值影响特定结果的可能性，因此，您可以选择任何输入组合，并且条形图将显示该组合影响要比较的结果对的方式。  
  
|值|说明|  
|-----------|-----------------|  
|**特性**|显示您在 **“属性”** 中选择的输入属性的名称。|  
|**值**|显示选定输入属性的值。|  
|**有利\<Value 1>**|显示一个条形，该条形指示此特定属性-值组合影响“值 1”**** 中选择的目标结果的程度。|  
|**有利\<Value 2>**|显示一个条形，该条形指示此特定属性-值组合影响“值 2”**** 中选择的目标结果的程度。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
