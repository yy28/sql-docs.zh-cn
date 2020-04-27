---
title: Microsoft 神经网络算法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- training neural networks
- output neurons [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- neurons [Analysis Services]
- classification algorithms [Analysis Services]
- neural networks
- multilayer perceptron network of neurons [Analysis Services]
- hidden neurons
- Back-Propagated Delta Rule network
- input neurons [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7330fab8b4c0ecdff296e0daa5e529442fd8b94
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083869"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中， [!INCLUDE[msCoName](../../includes/msconame-md.md)]神经网络算法将输入属性的每个可能状态与可预测属性的每个可能状态相结合，并使用定型数据来计算概率。 之后，可以根据输入属性，将这些概率用于分类或回归，并预测被预测属性的结果。  
  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经元网络算法构造的挖掘模型可以包含多个网络，这取决于用于输入和预测的列的数量，或者取决于仅用于预测的列的数量。 一个挖掘模型包含的网络数取决于挖掘模型使用的输入列和预测列包含的状态数。  
  
## <a name="example"></a>示例  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法对分析复杂输入数据（如来自制造或商业流程的数据）很有用；对于那些提供了大量定型数据，但使用其他算法很难为其派生规则的业务问题，这种算法也很有用。  
  
 在以下情况下，建议使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法：  
  
-   营销和促销分析，如评估直接邮件促销或一个电台广告活动的成功情况。  
  
-   根据历史数据预测股票升降、汇率浮动或其他频繁变动的金融信息。  
  
-   分析制造和工业流程。  
  
-   文本挖掘。  
  
-   分析多个输入和相对较少的输出之间的复杂关系的任何预测模型。  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法创建由多至三层神经元组成的网络。 这些层分别是输入层、可选隐藏层和输出层。  
  
 **输入层：** 输入神经元定义了数据挖掘模型的所有输入属性值及其概率。  
  
 **隐藏层：** 隐藏神经元接收来自输入神经元的输入，并向输出神经元提供输出。 隐藏层是向各种输入概率分配权重的位置。 权重说明某一特定输入对于隐藏神经元的相关性或重要性。 输入所分配的权重越大，则输入的值越重要。 权重可为负值，表示输入抑制而不是促进某一特定结果。  
  
 **输出层：** 输出神经元代表数据挖掘模型的可预测属性值。  
  
 有关如何构造和评价输入层、隐藏层和输出层的详细说明，请参阅 [Microsoft 神经网络算法技术参考](microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-neural-network-models"></a>神经网络模型所需的数据  
 神经网络模型必须包含一个键列、一个或多个输入列以及一个或多个可预测列。  
  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的数据挖掘模型与为该算法的可用参数指定的值紧密相关。 这些参数定义如何对数据进行采样、数据在每个列中的分布方式或预期分布方式以及何时调用功能选择以限制在最终模型中使用的值。  
  
 有关设置参数以自定义模型行为的详细信息，请参阅 [Microsoft 神经网络算法技术参考](microsoft-neural-network-algorithm-technical-reference.md)。  
  
## <a name="viewing-a-neural-network-model"></a>查看神经网络模型  
 您可以使用 **Microsoft 神经网络查看器**处理数据，并查看模型如何将输入与输出关联。 使用此自定义查看器，您可以筛选输入属性及其值，并查看显示它们如何影响输出的图形。 查看器中的工具提示显示与每对输入和输出值关联的概率和提升。 有关详细信息，请参阅 [使用 Microsoft 神经网络查看器浏览模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 浏览模型结构的最简便方式是使用 **Microsoft 一般内容树查看器**。 您可以查看输入、输出以及模型创建的网络，并单击展开任何节点，查看与输入、输出或隐藏层节点相关的统计信息。 有关详细信息，请参阅 [使用 Microsoft 一般内容树查看器浏览模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 处理完模型后，可以使用每个节点中存储的网络和权重来做出预测。 神经网络模型支持回归、关联和分类分析，因此，每个预测的含义可能各不相同。 此外，还可以查询模型自身，以查看找到的相关性并检索相关统计信息。 有关如何创建针对神经网络模型的查询的示例，请参阅 [神经网络模型查询示例](neural-network-model-query-examples.md)。  
  
 有关如何创建针对数据挖掘模型的查询的信息，请参阅 [数据挖掘查询](data-mining-queries.md)。  
  
## <a name="remarks"></a>备注  
  
-   不支持钻取或数据挖掘维度， 这是因为挖掘模型中节点的结构不一定直接与基础数据对应。  
  
-   不支持以预测模型标记语言 (PMML) 格式创建模型。  
  
-   支持使用 OLAP 挖掘模型。  
  
-   不支持创建数据挖掘维度。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 神经网络算法技术参考](microsoft-neural-network-algorithm-technical-reference.md)   
 [&#40;Analysis Services 数据挖掘的神经网络模型的挖掘模型内容&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [神经网络模型查询示例](neural-network-model-query-examples.md)   
 [Microsoft 逻辑回归算法](microsoft-logistic-regression-algorithm.md)  
  
  
