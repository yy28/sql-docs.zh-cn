---
title: Microsoft 逻辑回归算法 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dc5fbf84c23d93efcf6efa02c128f4e978624b6a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024230"
---
# <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 逻辑回归算法
  逻辑回归是一种众所周知的统计方法，用于对二进制结果建模。  
  
 通过采用不同的学习方法，可以在统计研究中以各种方式实现逻辑回归。 已通过使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法的一种变体来实现 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 逻辑回归算法。 虽然此算法与神经网络算法有许多共性，但逻辑回归算法更易于定型。  
  
 逻辑回归算法的一大优势是，该算法可采用任何类型的输入，因此非常灵活，并且支持若干不同的分析任务：  
  
-   使用人口统计信息预测相关结果，如某种特定疾病的风险。  
  
-   浏览并权衡导致结果的因素。 例如，查找影响客户反复光顾某一商店的因素。  
  
-   对文档、电子邮件或具有多个属性的其他对象进行分类。  
  
## <a name="example"></a>示例  
 设想这样一组人员，他们共享类似的人口统计信息并从 Adventure Works 公司购买产品。 通过对与特定结果（如购买目标产品）相关的数据进行建模，您可以查看人口统计信息对客户购买目标产品的可能性的影响。  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 逻辑回归是一种众所周知的统计方法，用于确定多个因素对一对结果的影响。 Microsoft 实现使用修改后的神经网络，对输入和输出之间的关系进行建模。 测量每个输入对输出的影响，并权衡不同输入在完成的模型中的作用。 名称逻辑回归来自这样一个事实：使用逻辑转换压缩数据曲线，以使极值的影响减至最小。 有关该实现以及如何自定义算法的详细信息，请参阅 [Microsoft 逻辑回归算法技术参考](microsoft-logistic-regression-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-logistic-regression-models"></a>逻辑回归模型所需的数据  
 准备用于定型逻辑回归模型的数据时，应理解特定算法的要求，其中包括所需要的数据量以及使用数据的方式。  
  
 逻辑回归模型的要求如下：  
  
 **单键列** 每个模型都必须包含一个用于唯一标识每条记录的数值列或文本列。 不允许复合键。  
  
 **输入列** 每个模型都必须至少包含一个输入列，该输入列包含用作分析因素的值。 可以根据需要拥有任意多的输入列，但是具体取决于每个列中值的数量，添加额外列会增加定型模型所需的时间。  
  
 **至少有一个可预测列** 模型必须至少包含一个可预测列，该预测列可以为任意数据类型，包括连续数值数据。 还可以将可预测列的值视为模型的输入，或者将其指定为仅用于预测。 嵌套表不允许用于可预测列，但是可作为输入使用。  
  
 有关逻辑回归模型支持的内容类型和数据类型的详细信息，请参阅 [Microsoft 逻辑回归算法技术参考](microsoft-logistic-regression-algorithm-technical-reference.md)的“要求”部分。  
  
## <a name="viewing-a-logistic-regression-model"></a>查看逻辑回归模型  
 您可以使用 Microsoft 神经网络查看器或 Microsoft 一般内容树查看器浏览模型。  
  
 使用 Microsoft 神经网络查看器查看模型时，Analysis Services 显示影响特定结果的因素，这些因素按重要性进行排序。 您可以选择一个属性以及要比较的值。 有关详细信息，请参阅 [使用 Microsoft 神经网络查看器浏览模型](browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 如果希望了解更多信息，您可以使用 Microsoft 一般内容树查看器浏览模型的详细信息。 逻辑回归模型的模型内容包含的边际节点显示该模型的所有输入以及可预测属性的子网。 有关详细信息，请参阅[逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-logistic-regression-models.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 定型模型之后，您可以针对模型内容创建查询以获取回归系数和其他详细信息，还可以使用模型进行预测。  
  
-   有关如何创建针对数据挖掘模型的查询的常规信息，请参阅 [数据挖掘查询](data-mining-queries.md)。  
  
-   有关查询逻辑回归模型的示例，请参阅 [聚类分析模型查询示例](clustering-model-query-examples.md)。  
  
## <a name="remarks"></a>Remarks  
  
-   不支持钻取， 这是因为挖掘模型中节点的结构不一定直接与基础数据对应。  
  
-   不支持创建数据挖掘维度。  
  
-   支持使用 OLAP 挖掘模型。  
  
-   不支持使用预测模型标记语言 (PMML) 创建挖掘模型。  
  
## <a name="see-also"></a>请参阅  
 [逻辑回归模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](mining-model-content-for-logistic-regression-models.md)   
 [Microsoft 逻辑回归算法技术参考](microsoft-logistic-regression-algorithm-technical-reference.md)   
 [逻辑回归模型查询示例](logistic-regression-model-query-examples.md)  
  
  