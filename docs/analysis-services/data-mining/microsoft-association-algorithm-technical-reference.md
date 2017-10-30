---
title: "Microsoft 关联算法技术参考 |Microsoft 文档"
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
- MINIMUM_ITEMSET_SIZE parameter
- MAXIMUM_SUPPORT parameter
- association algorithms [Analysis Services]
- MINIMUM_SUPPORT parameter
- OPTIMIZED_PREDICTION_COUNT parameter
- associations [Analysis Services]
- MAXIMUM_ITEMSET_COUNT parameter
- MAXIMUM_ITEMSET_SIZE parameter
- MINIMUM_PROBABILITY parameter
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a029a6efad9ebdbc15e42d593db28f9530b1b8e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-association-algorithm-technical-reference"></a>Microsoft 关联算法技术参考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法是熟知的 Apriori 算法的简单实现。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法均可用于分析关联，但每种算法找到的规则可能不同。 在决策树模型中，导致特定规则的拆分基于信息获取，而在关联模型中，规则完全基于置信度。 因此，在关联模型中，强规则或具有高置信度的规则由于不提供新信息，可能不一定会受到关注。  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Microsoft 关联算法的实现  
 Apriori 算法不分析模式，而是生成“候选项集 ”，然后计算该项集的数目。 根据要分析的数据类型，项目可表示事件、产品或属性值。  
  
 在最常见的关联模型类型布尔变量下，表示将 Yes/No 或 Missing/Existing 值分配给每个属性，如产品名称或事件名称。 例如，市场篮分析就是关联规则模型的一个示例，它使用布尔变量表示特定产品在客户的购物篮是存在还是不存在。  
  
 然后该算法为每个项集创建表示支持和置信度的分数。 这些分数可用于排名以及从项集中获取感兴趣的规则。  
  
 也可以为数值属性创建关联模型。 如果属性是连续的，则可以将数值“  离散化”或使用存储桶对其进行分组。 然后，即可将离散化值作为布尔值或属性值对来处理。  
  
### <a name="support-probability-and-importance"></a>支持、概率和重要性  
 “支持”（有时候将其称为“频率”）表示包含目标项目或项目组合的事例的数目。 只有至少具有指定支持量的项目才可包含在模型中。  
  
 “常用项集”指满足以下条件的项目集合：该项目集合所具有的支持超过由 MINIMUM_SUPPORT 参数定义的阈值。 例如，如果项集为 {A,B,C} 且 MINIMUM_SUPPORT 值为 10，则每个单个项目 A、B 和 C 必须均可在要包括在模型中的至少 10 个事例中找到，而且项目 {A,B,C} 的组合也必须可在至少 10 个事例中找到。  
  
 **注意** 通过指定项集的最大长度（这里长度指项目数目），还可控制挖掘模型中项集的数目。  
  
 默认情况下，对任何特定项目或项集的支持均表示包含该项目或项集的事例的计数。 不过，还可以将 MINIMUM_SUPPORT 表示为占数据集的总事例的百分比，方法是键入数字作为小于 1 的小数值。 例如，如果指定 MINIMUM_SUPPORT 值为 0.03，就意味着至少有 3% 的数据集总事例必须包含该项目或项集以包含在模型中。 应当试用模型，以确定是使用计数还是百分比更有意义。  
  
 恰恰相反，规则的阈值不用计数或百分比表示，而用概率（有时称为“置信度 ”）表示。 例如，如果项集 {A,B,C} 和项集 {A,B,D} 均出现在 50 个事例中，而项集 {A,B} 出现在另外 50 个事例中，则很明显，{A,B} 不是 {C} 的强预测因子。 因此，为了将某个特定结果对所有已知结果加权， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 通过将项集 {A,B,C} 支持除以所有相关项集支持来计算单个规则的概率（例如 If {A,B} Then {C}）。  
  
 可以通过设置 MINIMUM_PROBABILITY 的值来限制模型生成的规则的数目。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为创建的每个规则输出一个指示其“重要性”（也称为“提升”）的分数。 项集和规则的提升重要性的计算方法不同。  
  
 项集重要性的计算方法为项集概率除以项集中各个项的合成概率。 例如，如果项集包含 {A,B}， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 首先计算包含此 A 和 B 组合的所有事例的数目，并用此事例数除以事例总数，然后将得到的概率规范化。  
  
 规则重要性的计算方法为：在已知规则左侧的情况下，求规则右侧的对数可能性值。 例如，如果规则为 `If {A} Then {B}`，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 计算具有 A 和 B 的事例与具有 B 但不具有 A 的事例之比，然后使用对数刻度将该比率规范化。  
  
### <a name="feature-selection"></a>功能选择  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法不执行任何一种自动功能选择， 而是提供参数来控制其自身使用的数据。 上述情况可能包括对每个项集大小的限制，或对将项集添加到模型中所需的最大和最小支持的设置。  
  
-   若要筛选出太常见因而不受关注的项目和事件，请减小 MAXIMUM_SUPPORT 的值以将常见项集从模型中删除。  
  
-   若要筛选出罕见的项目和项集，请增大 MINIMUM_SUPPORT 的值。  
  
-   若要筛选出规则，请增大 MINIMUM_PROBABILITY 的值。  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>自定义 Microsoft 关联规则算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法支持多个参数，这些参数可以影响生成的挖掘模型的行为、性能和准确性。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 在任何时候均可使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的数据挖掘设计器来更改挖掘模型的参数。 你还可以更改参数以编程方式使用<xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A>在 AMO 中，或通过使用集合[MiningModels 元素 & #40;ASSL & #41;](../../analysis-services/scripting/collections/miningmodels-element-assl.md)在 XMLA。 下表对各参数进行了说明：  
  
> [!NOTE]  
>  不能使用 DMX 语句更改现有模型中的参数；在创建模型时必须指定 DMX CREATE MODEL 或 ALTER STRUCTURE… ADD MODEL 中的参数。  
  
 *MAXIMUM_ITEMSET_COUNT*  
 指定要生成的最大项集数。 如果不指定任何数目，则使用默认值。  
  
 默认值为 200000。  
  
> [!NOTE]  
>  项集按支持排名。 对具有相同支持的项集进行的排序是任意的。  
  
 *MAXIMUM_ITEMSET_SIZE*  
 指定一个项集中允许的最大项数。 将该值设置为 0 将指定对项集的大小没有限制。  
  
 默认值为 3。  
  
> [!NOTE]  
>  由于该参数达到限制时对模型的处理将停止，因此减小该值可能会减少创建该模型所需的时间。  
  
 *MAXIMUM_SUPPORT*  
 指定一个项集中包含的支持事例的最大数目。 该参数可用于消除频繁出现从而可能没有多少意义的项目。  
  
 如果该值小于 1，则表示事例总计的百分比。 如果该值大于 1，则表示可以包含项集的事例的绝对数。  
  
 默认值为 1。  
  
 *MINIMUM_ITEMSET_SIZE*  
 指定一个项集中允许的最小项数。 若增大该数值，模型包含的项集可能会减少。 例如，在希望忽略单项目项集时，这会很有帮助。  
  
 默认值为 1。  
  
> [!NOTE]  
>  由于无论如何 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 都必须在处理模型过程中为单个项目计算概率，因而不能通过增大该最小值来减少模型处理时间。 但通过增大该值，可筛选出较小的项集。  
  
 *MINIMUM_PROBABILITY*  
 指定规则为 True 的最小概率。  
  
 例如，如果将该值设置为 0.5，这将意味着不生成概率小于百分之五十的规则。  
  
 默认值为 0.4。  
  
 *MINIMUM_SUPPORT*  
 指定在该算法生成规则之前必须包含项集的事例的最小数目。  
  
 如果将该值设置为小于 1，则最小事例数的计算方式为占总事例的百分比。  
  
 如果将该值设置为大于 1 的整数，则指定最小事例数的计算方式为必须包含该项集的事例计数。 如果内存有限，则该算法可能会自动增大此参数的值。  
  
 默认值为 0.03。 这就意味着若要使某个项集包含在模型中，必须在至少 3% 的事例中可以找到该项集。  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 定义为优化预测而需要缓存的项目的数目。  
  
 默认值为 0。 使用默认值时，算法生成的预测与在查询中请求的预测数量相同。  
  
 如果为 OPTIMIZED_PREDICTION_COUNT 指定非零值，即使你请求了其他预测，预测查询也将最多返回指定项目数。 不过，设置值可提高预测性能。  
  
 例如，如果将该值设置为 3，算法将仅缓存 3 个项目进行预测。 无法看到与返回的这 3 个项目具有同等可能的其他预测。  
  
### <a name="modeling-flags"></a>建模标志  
 支持以下建模标志与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法配合使用。  
  
 NOT NULL  
 指示该列不能包含 Null。 在模型定型过程中，如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 遇到 Null，将导致错误。  
  
 适用于挖掘结构列。  
  
 MODEL_EXISTENCE_ONLY  
 表示列将被视为具有两个可能状态： **Missing** 和 **Existing**。 Null 表示缺失值。  
  
 适用于挖掘模型列。  
  
## <a name="requirements"></a>要求  
 关联模型必须包含一个键列、多个输入列和单个可预测列。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联规则算法支持特定的输入列和可预测列，如下表所示。 有关挖掘模型中内容类型含义的详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|列|内容类型|  
|------------|-------------------|  
|输入属性|循环、离散、离散化、键、表和已排序|  
|可预测属性|Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
> [!NOTE]  
>  支持 Cyclical 和 Ordered 内容类型，但算法会将它们视为离散值，不会进行特殊处理。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 关联算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [关联模型查询示例](../../analysis-services/data-mining/association-model-query-examples.md)   
 [关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  

