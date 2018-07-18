---
title: Microsoft 神经网络算法 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54896093b887985fc658e823f7d277347a70f0ea
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015536"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft 神经网络算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法是用于机器学习的流行且适应性强的神经网络体系结构实现。  该算法的工作原理是针对可预测属性的每个可能状态来测试输入属性的每个可能状态，并基于定型数据计算每个组合的概率。 可以将这些概率用于分类或回归任务，以便基于某些输入属性来预测结果。 神经网络还可以用于关联分析。  
  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法创建挖掘模型时，可以包含多个输出，该算法会创建多个网络。 包含在单个挖掘模型中的网络数取决于 输入列中的状态（或属性值）数，以及挖掘模型使用的可预测列数和这些列中的状态数。  
  
## <a name="example"></a>示例  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法对分析复杂输入数据（如来自制造或商业流程的数据）很有用；对于那些提供了大量定型数据，但使用其他算法很难为其派生规则的业务问题，这种算法也很有用。  
  
 在以下情况下，建议使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法：  
  
-   营销和促销分析，如评估直接邮件促销或一个电台广告活动的成功情况  
  
-   根据历史数据预测股票升降、汇率浮动或其他频繁变动的金融信息  
  
-   分析制造和工业流程  
  
-   文本挖掘  
  
-   分析多个输入和相对较少的输出之间的复杂关系的任何预测模型  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法创建由多至三层节点（有时称为神经元）组成的网络。 这些层分别是输入层、隐藏层和输出层。  
  
 **输入层：** 输入节点定义数据挖掘模型的所有输入属性值及其概率。  
  
 **隐藏层：** 隐藏节点接收来自输入节点的输入，并向输出节点提供输出。 隐藏层是向各种输入概率分配权重的位置。 权重说明某一特定输入对于隐藏节点的相关性或重要性。 输入所分配的权重越大，则输入的值越重要。 权重可为负值，表示输入抑制而不是促进某一特定结果。  
  
 **输出层：** 输出节点代表数据挖掘模型的可预测属性值。  
  
 有关如何构造和评价输入层、隐藏层和输出层的详细说明，请参阅 [Microsoft 神经网络算法技术参考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-neural-network-models"></a>神经网络模型所需的数据  
 神经网络模型必须包含一个键列、一个或多个输入列以及一个或多个可预测列。  
  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的数据挖掘模型与为该算法的可用参数指定的值紧密相关。 这些参数定义如何对数据进行采样、数据在每个列中的分布方式或预期分布方式以及何时调用功能选择以限制在最终模型中使用的值。  
  
 有关设置参数以自定义模型行为的详细信息，请参阅 [Microsoft 神经网络算法技术参考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="viewing-a-neural-network-model"></a>查看神经网络模型  
 您可以使用 **Microsoft 神经网络查看器**处理数据，并查看模型如何将输入与输出关联。 使用此自定义查看器，您可以筛选输入属性及其值，并查看显示它们如何影响输出的图形。 查看器中的工具提示显示与每对输入和输出值关联的概率和提升。 有关详细信息，请参阅 [使用 Microsoft 神经网络查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 浏览模型结构的最简便方式是使用 **Microsoft 一般内容树查看器**。 您可以查看输入、输出以及模型创建的网络，并单击展开任何节点，查看与输入、输出或隐藏层节点相关的统计信息。 有关详细信息，请参阅 [使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 处理完模型后，可以使用每个节点中存储的网络和权重来做出预测。 神经网络模型支持回归、关联和分类分析，因此，每个预测的含义可能各不相同。 此外，还可以查询模型自身，以查看找到的相关性并检索相关统计信息。 有关如何创建针对神经网络模型的查询的示例，请参阅 [神经网络模型查询示例](../../analysis-services/data-mining/neural-network-model-query-examples.md)。  
  
 有关如何创建针对数据挖掘模型的查询的信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。  
  
## <a name="remarks"></a>注释  
  
-   不支持钻取或数据挖掘维度， 这是因为挖掘模型中节点的结构不一定直接与基础数据对应。  
  
-   不支持以预测模型标记语言 (PMML) 格式创建模型。  
  
-   支持使用 OLAP 挖掘模型。  
  
-   不支持创建数据挖掘维度。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 神经网络算法技术参考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [神经网络模型 & #40; 的挖掘模型内容Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [神经网络模型查询示例](../../analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft 逻辑回归算法](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)  
  
  
