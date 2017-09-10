---
title: "Microsoft 决策树算法技术参考 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c098b5144a06cae6afb5b79ca4bf395a68768bd3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Microsoft 决策树算法技术参考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法是一种混合算法，它综合了多种不同的创建树的方法，并支持多种分析任务，包括回归、分类以及关联。 Microsoft 决策树算法支持对离散属性和连续属性进行建模。  
  
 本主题说明此算法的实现，介绍如何针对不同的任务自定义算法行为，并提供指向有关决策树模型查询的其他信息的链接。  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>决策树算法的实现  
 Microsoft 决策树算法通过获取模型的近似后验分布，将 Bayesian 方法应用于学习因果交互模型。 有关此方法的详细说明，请参阅 Microsoft Research 站点上的文章 [结构和参数学习](http://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409)。  
  
 用于评估学习所需的“先验知识”  的信息值的方法基于“可能性均等” 假定。 该假定认为数据对区分以不同方式表示同一条件独立断言的网络结构没有帮助。 先假定每个事例都有一个 Bayesian 先验网络和一个网络置信度的度量值。  
  
 然后，算法会利用给定的当前定型数据，使用这些先验网络计算网络结构的相对“后验概率”  ，并标识出具有最高后验概率的网络结构。  
  
 Microsoft 决策树算法使用不同的方法来计算最佳的树。 所使用的方法具体取决于任务，任务可为线性回归、分类或关联分析。 一个模型可包含多个针对不同可预测属性的树。 而且，每个树可包含多个分支，具体取决于数据中包含的属性和值的数量。 特定模型中生成的树的形状和深度取决于所使用的计分方法以及其他参数。 参数更改还会影响节点的拆分位置。  
  
### <a name="building-the-tree"></a>生成树  
 创建可能的输入值集时，Microsoft 决策树算法会执行 *feature selection* 来标识提供大部分信息的属性和值，而不会考虑非常少见的值。 该算法还会通过将值分组到“收集箱” 来创建值分组，这样的值分组可作为一个单元进行处理，从而使性能得到优化。  
  
 树是通过确定输入和目标结果之间的相关性而生成的。 关联完所有属性后，算法会标识出最能完全分隔结果的属性。 最佳分隔点是通过使用计算信息获取分数的公式确定的。 信息获取分数最高的属性将用于将事例分为各个子集；然后，还会利用同一过程，以递归方式分析各子集，直至树无法拆分为止。  
  
 用于计算信息获取分数的确切公式取决于创建算法时设置的参数、可预测列的数据类型以及输入的数据类型。  
  
### <a name="discrete-and-continuous-inputs"></a>离散输入和连续输入  
 如果可预测属性和输入都是离散的，则计算每个输入对应的结果数量只涉及创建一个矩阵并为矩阵中的每个单元生成分数。  
  
 但是，如果可预测属性是离散的，而输入是连续的，则会自动离散化连续的输入列。 你可以接受默认值，并让 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 查找最佳桶数，或者通过设置 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 属性来控制离散化连续输入的方式。 有关详细信息，请参阅 [更改挖掘模型中列的离散化](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)。  
  
 对于连续属性，该算法使用线性回归确定决策树的拆分位置。  
  
 如果可预测属性为连续数值数据类型，则还会对输出应用功能选择，以减少可能的结果数量，并更快地生成模型。 您可以通过设置 MAXIMUM_OUTPUT_ATTRIBUTES 参数来更改功能选择的阈值，从而增加或减少可能值的数量。  
  
 有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法如何处理离散可预测列的详细说明，请参阅 [学习 Bayesian 网络：知识与统计数据的组合](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf)。 有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法如何处理可预测的连续列的详细信息，请参阅 [Autoregressive Tree Models for Time-Series Analysis](http://go.microsoft.com/fwlink/?LinkId=45966)（时序分析的自动回归树模型）的附录。  
  
### <a name="scoring-methods-and-feature-selection"></a>计分方法和功能选择  
 Microsoft 决策树算法提供了三种信息获取计分公式：Shannon 平均信息量、使用 K2 先验的 Bayesian 网络和使用先验统一 Dirichlet 分布的 Bayesian 网络。 这三种都是数据挖掘领域中已经确立的方法。 建议您利用不同的参数，分别试用这些方法，以确定哪种方法结果最佳。 有关这些计分方法的详细信息，请参阅 [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70)。  
  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘算法都会自动使用功能选择来改善分析效果和减轻处理工作量。 用于功能选择的方法取决于生成模型所用的算法。 控制决策树模型的功能选择的算法参数为 MAXIMUM_INPUT_ATTRIBUTES 和 MAXIMUM_OUTPUT。  
  
|Algorithm|分析方法|注释|  
|---------------|------------------------|--------------|  
|决策树|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|如果任何列包含非二进制连续值，则兴趣性分数将用于所有列，以确保一致性。 否则，将使用默认方法或指定的方法。|  
|线性回归|兴趣性分数|线形回归仅使用兴趣性分数，原因是它仅支持连续列。|  
  
### <a name="scalability-and-performance"></a>可伸缩性和性能  
 分类是一种重要的数据挖掘策略。 通常，分类事例所需的信息量同输入记录的数量成正比例增长。 这将会限制可进行分类的数据量。 Microsoft 决策树算法使用以下方法来解决这些问题、提高性能并消除内存限制：  
  
-   使用功能选择优化属性的选择。  
  
-   使用 Bayesian 计分控制树的增长。  
  
-   优化连续属性的收集。  
  
-   动态分组输入值以确定最重要的值。  
  
 Microsoft 决策树算法高效快速且可伸缩，可轻松实现并行化，这意味着所有处理器均可协同工作，共同生成一个一致的模型。 这些特征使决策树分类器成为了理想的数据挖掘工具。  
  
 如果性能约束比较严格，则您可以使用以下方法来缩短决策树模型定型过程中的处理时间。 如果使用这些方法，请注意：通过消除属性来改善处理性能将会使模型的结果发生变化，可能无法很好地显示总体情况。  
  
-   增大 COMPLEXITY_PENALTY 参数的值以限制树的增长。  
  
-   限制关联模型中的项数以限制生成的树的数量。  
  
-   增大 MINIMUM_SUPPORT 参数的值以避免过度拟合。  
  
-   将所有属性的离散值的数量限制为 10 或更小。 您可尝试以不同的方式，对不同模型中的值进行分组。  
  
    > [!NOTE]  
    >  您可以使用  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中提供的数据浏览工具，在进行数据挖掘之前，先对数据中的值的分布进行可视化处理，并对这些值进行适当地分组。 有关详细信息，请参阅 [数据事件探查任务和查看器](../../integration-services/control-flow/data-profiling-task-and-viewer.md)。 你还可以使用 [Excel 2007 数据挖掘外接程序](http://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)，在 Microsoft Excel 中浏览、分组和重新标记数据。  
  
## <a name="customizing-the-decision-trees-algorithm"></a>自定义决策树算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法支持多个参数，这些参数可影响所生成的挖掘模型的性能和准确性。 您还可以对挖掘模型列或挖掘结构列设置建模标志来控制数据的处理方式。  
  
> [!NOTE]  
>  在所有版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中均提供 Microsoft 决策树算法；但是，用于自定义 Microsoft 决策树算法行为的某些高级参数仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的特定版本中提供。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2012 各个版本支持的功能](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表介绍了可用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法的参数。  
  
 *COMPLEXITY_PENALTY*  
 控制决策树的增长。 该值较低时，会增加拆分数；该值较高时，会减少拆分数。 默认值基于特定模型的属性数，详见以下列表：  
  
-   对于 1 到 9 个属性，默认值为 0.5。  
  
-   对于 10 到 99 个属性，默认值为 0.9。  
  
-   对于 100 或更多个属性，默认值为 0.99。  
  
 *FORCE_REGRESSOR*  
 强制算法将指定的列用作回归量，而不考虑算法计算出的列的重要性。 此参数只用于预测连续属性的决策树。  
  
> [!NOTE]  
>  通过设置此参数，您可以强制要求算法尝试将属性用作回归量。 但是，属性实际是否会在最终模型中用作回归量取决于分析结果。 您可以通过查询模型内容来确定用作了回归量的列。  
  
 [仅可用于某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 定义算法在调用功能选择之前可以处理的输入属性数。  
  
 默认值为 255。  
  
 如果将此值设置为 0，则表示关闭功能选择。  
  
 [仅可用于某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 定义算法在调用功能选择之前可以处理的输出属性数。  
  
 默认值为 255。  
  
 如果将此值设置为 0，则表示关闭功能选择。  
  
 [仅可用于某些版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MINIMUM_SUPPORT*  
 确定在决策树中生成拆分所需的叶事例的最少数量。  
  
 默认值为 10。  
  
 如果数据集非常大，则可能需要增大此值，以避免过度定型。  
  
 *SCORE_METHOD*  
 确定用于计算拆分分数的方法。 可用选项包括：  
  
|ID|名称|  
|--------|----------|  
|1|Entropy|  
|3|Bayesian with K2 Prior|  
|4|Bayesian Dirichlet Equivalent (BDE) with uniform prior<br /><br /> （默认值）|  
  
 默认值为 4 或 BDE。  
  
 有关这些计分方法的说明，请参阅 [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70)。  
  
 *SPLIT_METHOD*  
 确定用于拆分节点的方法。 可用选项包括：  
  
|ID|名称|  
|--------|----------|  
|1|**Binary:** 指示无论属性值的实际数量是多少，树都拆分为两个分支。|  
|2|**Complete:** 指示树可以创建与属性值数目相同的分叉。|  
|3|**Both:** 指定 Analysis Services 可确定应使用 binary 还是 complete，以获得最佳结果。|  
  
 默认值为 3。  
  
### <a name="modeling-flags"></a>建模标志  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法支持下列建模标志。 创建挖掘结构或挖掘模型时，定义建模标志以指定分析期间如何处理每列中的值。 有关详细信息，请参阅[建模标志（数据挖掘）](../../analysis-services/data-mining/modeling-flags-data-mining.md)。  
  
|建模标志|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|表示列将被视为具有两个可能状态： **Missing** 和 **Existing**。 Null 表示缺失值。<br /><br /> 适用于挖掘模型列。|  
|NOT NULL|指示该列不能包含 Null。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。<br /><br /> 适用于挖掘结构列。|  
  
### <a name="regressors-in-decision-tree-models"></a>决策树模型中的回归量  
 即使不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法，所有其输入和输出均为连续数值的决策树模型都可能会包含表示连续属性的回归的节点。  
  
 您无需指定连续数值数据列表示回归量。 即使不对列设置 REGRESSOR 标志， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法也会自动将列用作潜在回归量，并会将数据集分区成具有一定意义的模式的区域。  
  
 您可以使用 FORCE_REGRESSOR 参数来确保算法将使用某一特定回归量。 此参数只可用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法。 设置建模标志时，算法会尝试查找具有 `a*C1 + b*C2 + ...` 形式的回归公式，以拟合树中节点的模式。 将对剩余的总和进行计算，如果偏差过大，则在树中执行强制拆分。  
  
 例如，如果要将 **Income** 用作属性来预测客户的购买行为，并对列设置 REGRESSOR 建模标志，则算法将会先通过使用标准回归公式来尝试拟合 **Income** 值。 如果偏差过大，则会放弃回归公式，并根据其他属性对树进行拆分。 拆分完毕后，决策树算法将尝试拟合每个分支中的 Income 的回归量。  
  
## <a name="requirements"></a>要求  
 一个决策树模型必须包含一个键列、若干输入列和至少一个可预测列。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法支持下表中列出的特定输入列和可预测列。 有关内容类型在用于挖掘模型中时的含义的详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|列|内容类型|  
|------------|-------------------|  
|输入属性|Continuous、Cyclical、Discrete、Discretized、Key、Ordered 和 Table|  
|可预测属性|Continuous、Cyclical、Discrete、Discretized、Ordered 和 Table|  
  
> [!NOTE]  
>  支持 Cyclical 和 Ordered 内容类型，但算法会将它们视为离散值，不会进行特殊处理。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [决策树模型查询示例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)   
 [决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
