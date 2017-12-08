---
title: "Microsoft 顺序分析算法技术参考 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9c624a1c14614d62c200e1f3afdfe5623a318853
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Microsoft 顺序分析和聚类分析算法技术参考
  Microsoft 顺序分析和聚类分析算法是一种综合算法，它使用 Markov 链分析来识别有序序列，并会综合利用此分析结果和聚类分析技术基于模型中的序列和其他属性生成分类。 本主题介绍该算法的实现以及如何自定义算法，最后还对顺序分析和聚类分析模型的特殊要求进行了说明。  
  
 有关该算法的详细常规信息，包括如何浏览和查询顺序分析和聚类分析模型，请参阅 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)。  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Microsoft 顺序分析和聚类分析算法的实现  
 Microsoft 顺序分析和聚类分析模型使用 Markov 模型来识别序列并确定序列的概率。 Markov 模型是存储不同状态之间的转换的定向图形。 Microsoft 顺序分析和聚类分析算法使用 N 阶 Markov 链，而不使用隐 Markov 模型。  
  
 您可由 Markov 链中的阶数知道有多少个状态用于确定当前状态的概率。 在一阶 Markov 模型中，当前状态的概率仅取决于前一个状态。 在二阶 Markov 链中，当前状态的概率取决于前两个状态。其他情况下的概率可依此类推。 对于每个 Markov 链，转换矩阵都会存储每种状态组合的转换。 当 Markov 链的长度增加时，转换矩阵的规模也会呈指数增长，但同时会变得非常稀疏。 处理时间也会按比例增加。  
  
 点击流分析法是一种分析网站网页的访问情况的方法，它可帮助进行链的可视化处理。 对于每个会话，用户都会创建一个很长的点击序列。 通过创建模型来分析用户在网站中的行为时，用于定型的数据集就是一个 URL 序列；该序列可转换为一个图形，其中包含相同点击路径的所有实例的计数。 例如，该图形可包含用户从第 1 页转到第 2 页的概率 (10%) 以及用户从第 1 页转到第 3 页的概率 (20%)，其余依此类推。 当将所有可能的路径以及路径片段整合到一起时，就可获得一张图，它比所观察到的任何单个路径都长，而且更复杂。  
  
 默认情况下，Microsoft 顺序分析和聚类分析算法使用聚类分析的 Expectation Maximization (EM) 方法。 有关详细信息，请参阅 [Microsoft 聚类分析算法技术参考](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)。  
  
 聚类分析的目标是序列属性和非序列属性。 每个分类都是利用概率分布随机选择的。 每个分类都具有表示完整路径集的 Markov 链以及包含序列状态转换和概率的矩阵。 算法会基于初始分布，使用 Bayes 定理来计算所有属性（包括序列）属于特定分类的概率。  
  
 Microsoft 顺序分析和聚类分析算法支持在模型中使用其他非序列属性。 这意味着将会将这些非序列属性与序列属性组合起来，创建具有相似属性的事例分类，就像典型的聚类分析模型中一样。  
  
 与典型的聚类分析模型相比，顺序分析和聚类分析模型通常会创建更多的分类。 因此，Microsoft 顺序分析和聚类分析算法会执行“群集分解” ，以基于序列属性和其他属性分离群集。  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>顺序分析和聚类分析模型中的功能选择  
 生成序列时不会调用功能选择，但会在聚类分析阶段应用功能选择。  
  
|模型类型|功能选择方法|注释|  
|----------------|------------------------------|--------------|  
|顺序分析和聚类分析|未使用|不调用功能选择；但可以通过设置参数 MINIMUM_SUPPORT 和 MINIMUM_PROBABILIITY 的值来控制算法的行为。|  
|群集|兴趣性分数|尽管聚类分析算法可能使用离散算法或离散化算法，但每个属性的分数仍将作为间距进行计算，并且是连续的，因此使用兴趣性分数。|  
  
 有关详细信息，请参阅 [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70)。  
  
### <a name="optimizing-performance"></a>优化性能  
 Microsoft 顺序分析和聚类分析算法支持多种处理优化方法：  
  
-   通过设置 CLUSTER_COUNT 参数的值可以控制生成的分类数。  
  
-   通过增大 MINIMUM_SUPPORT 参数的值可以减少包含为属性的序列的数量。 这会导致删除一些罕见的序列。  
  
-   在处理模型之前，通过对相关属性进行分组可以降低复杂性。  
  
 通常，可以使用多种方法来优化 n 阶 Markov 链模式的性能：  
  
-   控制可能的序列的长度。  
  
-   以编程方式减小 n 值。  
  
-   仅存储超出指定阈值的概率。  
  
 有关这些方法的深入探讨不属于本主题的讨论范围。  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>自定义顺序分析和聚类分析算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法支持多个参数，这些参数可影响所生成的挖掘模型的行为、性能和准确性。 您还可以通过设置用于控制算法的定型数据处理方式的建模标志来修改已完成模型的行为。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表介绍可用于 Microsoft 顺序分析和聚类分析算法的参数。  
  
 CLUSTER_COUNT  
 指定将由算法生成的大致分类数。 如果无法基于相应的数据生成该大致数目的分类，则算法将生成尽可能多的分类。 如果将 CLUSTER_COUNT 设置为 0，则算法将会使用试探性方法确定要生成的分类的最佳数量。  
  
 默认值为 10。  
  
> [!NOTE]  
>  指定一个作为对算法的提示的非零数，算法将会查找该指定数，但最终的查找结果可能会大于或小于所指定的数。  
  
 MINIMUM_SUPPORT  
 指定支持属性创建分类所需的最小事例数。  
  
 默认值为 10。  
  
 MAXIMUM_SEQUENCE_STATES  
 指定一个顺序可以拥有的最大状态数。  
  
 将该值设置为大于 100 的数将导致算法创建一个不提供有意义的信息的模型。  
  
 默认值为 64。  
  
 MAXIMUM_STATES  
 指定算法支持的非序列属性的最大状态数。 如果非序列属性的状态数大于最大状态数，则算法将使用该属性最常见的状态，并将视剩余状态为 **Missing**。  
  
 默认值为 100。  
  
### <a name="modeling-flags"></a>建模标志  
 支持将以下建模标志与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法配合使用。  
  
 NOT NULL  
 指示该列不能包含 Null。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。  
  
 适用于挖掘结构列。  
  
 MODEL_EXISTENCE_ONLY  
 表示列将被视为具有两个可能状态： **Missing** 和 **Existing**。 Null 视为 **Missing** 值。  
  
 适用于挖掘模型列。  
  
 有关挖掘模型中 Missing 值的用法以及 Missing 值如何影响概率分数的详细信息，请参阅[缺失值（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)。  
  
## <a name="requirements"></a>要求  
 事例表必须具有事例 ID 列。 此外，事例表还可以包含其他存储事例属性的列。  
  
 Microsoft 顺序分析和聚类分析算法要求序列信息以嵌套表的形式存储。 该嵌套表必须包含一个 Key Sequence 列。 **Key Sequence** 列可包含可以存储的任何类型的数据（包括字符串数据类型），还必须包含每个事例的唯一值。 而且，在处理模型之前，您必须确保事例表和嵌套表要按与其相关的键的升序存储。  
  
> [!NOTE]  
>  如果创建使用 Microsoft 顺序分析算法、但却不使用序列的模型，则生成的模型将不包含任何序列，而仅会基于模型中包含的其他属性对事例进行分类。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法支持下表中列出的特定输入列和可预测列。 有关内容类型在用于挖掘模型中时的含义的详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|列|内容类型|  
|------------|-------------------|  
|输入属性|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Table 和 Ordered|  
|可预测属性|Continuous、Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
## <a name="remarks"></a>注释  
  
-   将 [PredictSequence (DMX)](../../dmx/predictsequence-dmx.md) 函数用于序列预测。 有关支持序列预测的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的详细信息，请参阅 [SQL Server 2012 各个版本支持的功能](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法不支持使用预测性模型标记语言 (PMML) 来创建挖掘模型。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法支持钻取，支持使用 OLAP 挖掘模型和数据挖掘维度。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [序列聚类分析模型查询示例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
