---
title: 缺少值 (Analysis Services-数据挖掘) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 662fdd55fc5929fe56734b9894bf971962ff2a7b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="missing-values-analysis-services---data-mining"></a>Missing 值（Analysis Services - 数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  正确处理“Missing 值”   是有效建模的重要组成部分。 本节说明什么是 Missing 值，并介绍在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的、用于处理在生成数据挖掘结构和挖掘模型时的 Missing 值的功能。  
  
## <a name="definition-of-missing-values-in-data-mining"></a>数据挖掘中 Missing 值的定义  
 Missing 值可表示很多不同情况： 可能表示字段不适用，事件未发生或者数据不可用。 可能输入数据的人不知道正确的值，或不介意字段未填充。  
  
 但是，在很多数据挖掘方案中 Missing 值提供了重要的信息。 Missing 值的含义主要取决于上下文。 例如，发票列表中日期的 Missing 值的含义与指示雇员雇用日期的列中缺少日期有很大区别。 通常， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会将 Missing 值处理为信息性内容，并调整概率以将 Missing 值包括到其计算之中。 这样做即可确保模型平衡，又避免过多地偏重于现有的事例。  
  
 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了两种截然不同的机制用于管理和计算 Missing 值。 第一种方法在挖掘结构级别控制 Null 值的处理。 第二种方法的每个算法的实现均与第一种方法不同，但是通常定义在允许 Null 值的模型中如何处理和计入 Missing 值。  
  
## <a name="specifying-handling-of-nulls"></a>指定 Null 值的处理  
 在您的数据源中，可能以很多方式表示 Missing 值：为 Null、为电子表格中的空单元、为 N/A 值或其他代码，或为像 9999 这样的自定义值。 但是，为了进行数据挖掘，只有 Null 值被视为 Missing 值。 如果您的数据包含不是 Null 的占位符值，它们可能影响模型的结果，因此，您应用 Null 替换它们或在可能的情况下推断正确的值。 有许多工具可以用来推断并填充适当的值，例如，SQL Server Integration Services 中的查找转换或数据事件探查任务，或者 Excel 数据挖掘外接程序提供的“从示例填充”工具。  
  
 如果正在建模的任务指定某列一定不能有 Missing 值，则应当在定义挖掘结构时将 **NOT_NULL** 建模标志应用到该列。 此标志指示如果某个事例不具有适当值，处理将失败。 如果处理模型时出现此错误，您可以记录该错误并采取措施来更正为该模型提供的数据。  
  
## <a name="calculation-of-the-missing-state"></a>Missing 状态的计算  
 对于数据挖掘算法，Missing 值为信息性内容。 在事例表中， **Missing** 与其他任何值一样为有效状态。 此外，数据挖掘模型还可以使用其他值来预测某个值是否为 Missing 值。 也就是说，值缺失这种情况不会被视为错误。  
  
 创建挖掘模型时，对于所有离散列， **Missing** 状态会自动添加到模型中。 例如，如果输入列 [性别] 包含两个可能的值（男和女），将自动添加第三个值来表示 **Missing** 值，而且显示该列所有值分布的直方图将始终包含一个具有 **Missing** 值的事例的计数。 如果性别列不缺少任何值，则直方图显示发现 0 个事例的状态为 Missing。  
  
 当您认为数据可能不具有所有可能值的示例，并且不希望仅仅因为数据中没有任何示例而使模型排除该可能性时，则默认包含 **Missing** 状态很有必要。 例如，即使某商店的销售数据显示所有购买某种产品的客户恰巧都为女性，您也不希望创建一个预测只有女性才可能购买此产品的模型。 相反， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为额外未知的值添加占位符，称之为 **缺少**，作为容纳其他可能状态的一种方法。  
  
 例如，下表显示了为自行车购买者教程创建的决策树模型中的（所有）节点的值的分布。 在示例方案中，[Bike Buyer] 列为可预测属性，其中，1 表示“是”，0 表示“否”。  
  
|“值”|事例|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 此分布显示大约一半的客户已经购买了自行车，而一半的客户还没有购买自行车。 此特定数据集十分清晰；因此，每个事例的 [Bike Buyer] 列中都有一个值，并且 **Missing** 值的计数为 0。 但是，只要事例的 [Bike Buyer] 字段值为 Null， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就会将该行计为具有 **Missing** 值的事例。  
  
 如果输入为连续的列，则模型将属性的两个可能的状态 **Existing** 和 **Missing**排列成表格报表的形式。 也就是说，该列或者包含某种数值数据类型的值，或者不包含任何值。 对于有值的事例，模型会计算平均值、标准偏差以及其他有意义的统计。 对于没有值的事例，模型将提供 **Missing** 值的计数并相应调整预测。 调整预测的方法因算法而异，下面一节将对其进行介绍。  
  
> [!NOTE]  
>  对于嵌套表中的属性，Missing 值为非信息性内容。 例如，如果某个客户未购买某种产品，则嵌套 **Products** 表中将不会有对应该产品的行，挖掘模型也不会为该缺少的产品创建属性。 但是，如果您对未购买某种产品的客户感兴趣，则可以创建一个模型，在该模型中对嵌套表中的不存在的产品进行筛选，其方法是在模型筛选器中使用 NOT EXISTS 语句。 有关详细信息，请参阅 [对挖掘模型应用筛选器](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
## <a name="adjusting-probability-for-missing-states"></a>调整 Missing 状态的概率  
 除了对值进行计数外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还计算整个数据集中的任何值的概率。 这对于 **Missing** 值同样适用。 例如，下表显示了前面示例中事例的概率：  
  
|“值”|事例|概率|  
|-----------|-----------|-----------------|  
|0|9296|50.55%|  
|1|9098|49.42%|  
|Missing|0|0.03%|  
  
 当事例个数为 0 时，计算得出的 **Missing** 值的概率为 0.03%，这好像有些奇怪。 实际上，此行为是设计造成的，目的是通过这种调整使模型可以适当地处理未知值。  
  
 通常，概率计算如下：良好的事例除以所有可能的事例。 在此示例中，算法计算符合某个特定条件（[Bike Buyer] = 1 或 [Bike Buyer] = 0）的事例的总和，并用该数除以总行数。 但是，为了将 **Missing** 事例考虑在内，将 1 添加到所有可能的事例数中。 因此，未知事例的概率不再为零，而是一个非常小的数，表示此状态仅仅是不大可能的状态，但不是不可能的状态。  
  
 较小的 **Missing** 值的添加不会更改预测因子的输出；但是，对于历史数据不包含所有可能结果的情况，使用该值可以改善建模。  
  
> [!NOTE]  
>  各个数据挖掘访问接口处理 Missing 值的方式不同。 例如，某些访问接口假定嵌套列中缺少的数据为稀疏表示方式，但却假定非嵌套列中缺少的数据为随机缺少。  
  
 如果确定所有的结果均在数据中指定，并需要防止概率调整，则应对挖掘结构中的列设置 NOT_NULL 建模标志。  
  
> [!NOTE]  
>  每个算法（包括可能从第三方插件中获取的自定义算法）都可以用不同的方式处理 Missing 值。  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>决策树模型中 Missing 值的特殊处理  
 Microsoft 决策树算法计算 Missing 值的概率的方法不同于其他算法。 不仅仅向事例总数加 1，该决策树算法还使用稍有差别的公式来针对 **Missing** 状态进行调整。  
  
 在决策树模型中， **Missing** 状态的概率按如下公式进行计算：  
  
 StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStates)  
  
决策树算法提供了额外的调整，可帮助该算法补偿模型，这可能导致在定型期间排除许多状态筛选器存在。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，如果在定型期间存在某种状态，但是恰巧在某个节点中有零支持，则将进行标准调整。 但是，如果在定型期间从未遇到某种状态，该算法会将其概率精确设置为零。 此项调整不仅适用于 **Missing** 状态，还适用于在定型数据中存在、但模型筛选结果具有零支持的其他状态。  
  
 此额外调整产生以下公式：  
  
 StateProbability = 0.0（如果在定型集中该状态具有 0 支持）  
  
 ELSE StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStatesWithNonZeroSupport)  
  
 此调整的净效果是保持树的稳定性。  
  
## <a name="related-tasks"></a>相关任务  
 下列主题提供有关如何处理 Missing 值的详细信息。  
  
|“任务”|链接|  
|-----------|-----------|  
|将标志添加到各个模型列来控制对 Missing 值的处理|[查看或更改建模标志 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|设置挖掘模型的属性来控制对 Missing 值的处理|[更改挖掘模型的属性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)|  
|了解如何在 DMX 中指定建模标志|[建模标志 & #40; DMX & #41;](../../dmx/modeling-flags-dmx.md)|  
|更改挖掘结构处理 Missing 值的方式|[更改挖掘结构的属性](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型内容 & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [建模标志 & #40; 数据挖掘 & #41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
