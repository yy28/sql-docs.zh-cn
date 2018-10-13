---
title: 线性回归模型的挖掘模型内容 (Analysis Services-数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- mining model content, linear regression models
- regression algorithms [Analysis Services]
ms.assetid: a6abcb75-524e-4e0a-a375-c10475ac0a9d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c39ec7718ee2d79ab95c13ebfd3e30afc189d805
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120034"
---
# <a name="mining-model-content-for-linear-regression-models-analysis-services---data-mining"></a>线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）
  本主题介绍使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法的模型特有的挖掘模型内容。 有关所有模型类型的挖掘模型内容的常规说明，请参阅 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-linear-regression-model"></a>了解线性回归模型的结构  
 线性回归模型的结构非常简单。 每个模型具有表示该模型及其元数据的单一父节点和回归树节点 (NODE_TYPE = 25)，其中包含每个可预测属性的回归公式。  
  
 ![用于线性回归模型的结构](../media/modelcontentstructure-linreg.gif "用于线性回归模型的结构")  
  
 线性回归模型与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树使用相同的算法，但线性回归模型使用不同的参数来约束树，并且仅接受连续属性作为输入。 但是，由于线性回归模型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法，线性回归模型使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树查看器来显示。 有关详细信息，请参阅 [使用 Microsoft 树查看器浏览模型](browse-a-model-using-the-microsoft-tree-viewer.md)。  
  
 以下部分将说明如何解释回归公式节点中的信息。 该信息不仅适用于线性回归模型，还适用于将回归作为树的一部分包括在其中的决策树模型。  
  
## <a name="model-content-for-a-linear-regression-model"></a>线性回归模型的模型内容  
 本部分提供的详细信息和示例仅针对挖掘模型内容中与线性回归有特殊关系的列。  
  
 有关架构行集中的通用列的信息，请参阅 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)。  
  
 MODEL_CATALOG  
 存储模型的数据库的名称。  
  
 MODEL_NAME  
 模型的名称。  
  
 ATTRIBUTE_NAME  
 **根节点：** 空白  
  
 **回归节点：** 可预测属性的名称。  
  
 NODE_NAME  
 始终与 NODE_UNIQUE_NAME 相同。  
  
 NODE_UNIQUE_NAME  
 此模型中节点的唯一标识符。 此值不能更改。  
  
 NODE_TYPE  
 线性回归模型输出以下节点类型：  
  
|节点类型 ID|类型|Description|  
|------------------|----------|-----------------|  
|25|回归树根节点|包含描述输入和输出变量之间的关系的公式。|  
  
 NODE_CAPTION  
 与节点关联的标签或标题。 此属性主要用于显示目的。  
  
 **根节点：** 空白  
  
 **回归节点：** 全部。  
  
 CHILDREN_CARDINALITY  
 对节点所具有的子节点数的估计。  
  
 **根节点：** 指示回归节点的数目。 为模型中的每个可预测属性创建一个回归节点。  
  
 **回归节点：** 始终为 0。  
  
 PARENT_UNIQUE_NAME  
 节点的父节点的唯一名称。 根级别上的任何节点均返回 NULL。  
  
 NODE_DESCRIPTION  
 节点的说明。  
  
 **根节点：** 空白  
  
 **回归节点：** 全部。  
  
 NODE_RULE  
 不用于线性回归模型。  
  
 MARGINAL_RULE  
 不用于线性回归模型。  
  
 NODE_PROBABILITY  
 与此节点相关联的概率。  
  
 **根节点：** 0  
  
 **回归节点：** 1  
  
 MARGINAL_PROBABILITY  
 从父节点到达该节点的概率。  
  
 **根节点：** 0  
  
 **回归节点：** 1  
  
 NODE_DISTRIBUTION  
 提供有关节点中的值的统计信息的嵌套表。  
  
 **根节点：** 0  
  
 **回归节点：** 包含用于生成回归公式的元素的表。 回归节点包含下列值类型：  
  
|VALUETYPE|  
|---------------|  
|1（缺失）|  
|3（连续）|  
|7（系数）|  
|8（得分）|  
|9（统计信息）|  
|11（截距）|  
  
 NODE_SUPPORT  
 支持此节点的事例的数目。  
  
 **根节点：** 0  
  
 **回归节点：** 定型事例的计数。  
  
 MSOLAP_MODEL_COLUMN  
 可预测属性的名称。  
  
 MSOLAP_NODE_SCORE  
 与 NODE_PROBABILITY 相同  
  
 MSOLAP_NODE_SHORT_CAPTION  
 用于显示的标签。  
  
## <a name="remarks"></a>备注  
 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法创建模型时，数据挖掘引擎创建决策树模型的特殊实例，并提供约束树的参数，将树约束为在单个节点中包含所有定型数据。 将标记所有连续输入并将其视为潜在回归量，但仅将适合数据的回归量作为回归量保留在最终模型中。 分析过程要么为每个回归量各生成一个回归公式，要么根本不生成任何回归公式。  
  
 你可以在“挖掘图例”中查看完整的回归公式，方法是在 [Microsoft 树查看器](browse-a-model-using-the-microsoft-tree-viewer.md)中单击“(全部)”节点。  
  
 此外，在创建包括连续可预测属性的决策树模型时，有时树具有的回归节点会共享回归树节点的属性。  
  
##  <a name="NodeDist_Regression"></a> 连续属性的节点分布  
 回归节点中大多数重要信息都包含在 NODE_DISTRIBUTION 表中。 下面的示例演示 NODE_DISTRIBUTION 表的布局。 在此示例中，使用目标邮件挖掘结构创建的线性回归模型基于客户的年龄预测其收入。 该模型仅用于演示目的，因为使用现有 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 示例数据和挖掘结构可以方便地生成该模型。  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|SUPPORT|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|年龄|471.687717702463|0|0|126.969442359327|7|  
|年龄|234.680904692439|0|0|0|8|  
|年龄|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 NODE_DISTRIBUTION 表包含多个行，每个行按变量进行分组。 前两个行的值类型始终为 1 和 3，用于描述目标属性。 后续行提供有关特定“回归量”的公式的详细信息。 回归量是与输出变量具有线性关系的输入变量。 您可以拥有多个回归量，并且每个回归量将针对系数 (VALUETYPE = 7)、得分 (VALUETYPE = 8) 和统计信息 (VALUETYPE = 9) 包含单独的行。 最后，表还具有一个包含公式的截距 (VALUETYPE = 11) 的行。  
  
### <a name="elements-of-the-regression-formula"></a>回归公式的元素  
 NODE_DISTRIBUTION 嵌套表将回归公式的每个元素包含在一个单独的行中。 示例结果的前两行数据包含有关可预测属性 **Yearly Income**的信息，该属性建立了依赖变量的模型。 SUPPORT 列显示支持该属性的以下两种状态的事例计数： **Yearly Income** 值可用或缺少 **Yearly Income** 值。  
  
 VARIANCE 列提供可预测属性的计算出的方差。  “方差”可度量示例中的值在给定预期分布情况下的离散程度。 此处的方差通过取平均值偏差的平方的平均值计算而来。 方差的平方根也称为标准偏差。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 未提供标准偏差，但是可通过计算轻松得出其值。  
  
 对于每个回归量，输出包括三行。 它们包括系数、得分和回归量统计信息。  
  
 最后，表还包含一个提供公式的截距的行。  
  
#### <a name="coefficient"></a>系数  
 对于每个回归量，会计算出一个系数 (VALUETYPE = 7)。 系数自身显示在 ATTRIBUTE_VALUE 列中，而 VARIANCE 列显示系数的方差。 计算系数的目的在于实现最大程度的线性。  
  
#### <a name="score-gain"></a>得分  
 每个回归量的得分 (VALUETYPE = 8) 表示属性的兴趣性分数。 您可以使用此值来估计多个回归量的有用性。  
  
#### <a name="statistics"></a>统计信息  
 回归量统计信息 (VALUETYPE = 9) 是其事例具有相应值的属性的平均值。 ATTRIBUTE_VALUE 列包含平均值自身，而 VARIANCE 列包含平均值偏差的总和。  
  
#### <a name="intercept"></a>截距  
 通常，回归公式中的“截距”(VALUETYPE = 11) 或“残差”指示当输入属性为 0 时可预测属性的值。 在大多数情况下都不可能发生这种情况，该情况可能产生不够直观的结果。  
  
 例如，在根据年龄预测收入的模型中，了解 0 岁时的收入毫无用处。 在现实生活中，了解与平均值有关的人类行为通常更有用。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 修改了截距，以便说明每个回归量与平均值的关系。  
  
 在挖掘模型内容中很难显示此调整，但是如果在 **Microsoft 树查看器** 的 **“挖掘图例”** 中查看完成后的公式，则可以很清楚地显示这一调整。 回归公式从点 0 移向表示平均值的点。 这样，可以根据当前数据呈现一个更直观的视图。  
  
 因此，假定平均年龄约为 45，回归公式的截距 (VALUETYPE = 11) 则指示平均收入。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft 线性回归算法](microsoft-linear-regression-algorithm.md)   
 [Microsoft 线性回归算法技术参考](microsoft-linear-regression-algorithm-technical-reference.md)   
 [线性回归模型查询示例](linear-regression-model-query-examples.md)  
  
  
