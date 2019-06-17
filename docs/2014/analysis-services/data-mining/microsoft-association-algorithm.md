---
title: Microsoft 关联算法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MinimumProbability property
- itemsets [Analysis Services]
- MaximumItemsetCount property
- MinimumSupport property
- OPTIMIZED_PREDICTION_COUNT
- OptimizedPredictionCount property
- MaximumSupport property
- MINIMUM_PROBABILITY
- algorithms [data mining]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- MinimumItemsetSize property
- market basket analysis [Analysis Services]
- associations [Analysis Services]
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- MaximumItemsetSize property
ms.assetid: 8b6b8247-62f9-4f6f-b1af-d01dab290e4c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a799f5a8aef79dec7cb951e95e6f252b3be2626
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084073"
---
# <a name="microsoft-association-algorithm"></a>Microsoft 关联算法
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法是指 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的关联算法，对建议引擎非常有用。 建议引擎根据客户已购买的项或者客户已对其表现出兴趣的项向他们推荐产品。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法对市场篮分析也非常有用。 市场篮分析的示例，请参阅[第 3 课：生成市场篮方案&#40;数据挖掘中级教程&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)数据挖掘教程中。  
  
 关联模型基于包含各事例的标识符及各事例所包含项的标识符的数据集生成。 事例中的一组项称为“项集  ”。 关联模型由一系列项集和说明这些项在事例中如何分组的规则组成。 算法标识的规则可用于根据客户购物车中已有的项来预测客户将来可能购买的产品。 以下关系图显示了项集中的一系列规则。  
  
 ![对于关联模型的规则的一组](../media/association.gif "一组对于关联模型的规则")  
  
 正如该关系图中所示， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法可能会在数据集中找到许多规则。 该算法使用两个参数（support 和 probability）来说明项集以及该算法生成的规则。 例如，假定 X 和 Y 表示购物车中的两个项，则 support 参数是数据集中同时包含这两个项（X 和 Y）的事例的数目。通过将 support 参数与用户定义的 *MINIMUM_SUPPORT* 和 *MAXIMUM_SUPPORT,* 参数结合使用，该算法可控制生成的项集数。 probability 参数（也称为置信度  ）表示数据集中既包含 X 也包含 Y 的一部分事例。通过将 probability 参数与 *MINIMUM_PROBABILITY* 参数结合使用，该算法可控制生成的规则数。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] Cycle 公司正在重新设计其网站的功能。 重新设计的目的是提高产品的零售量。 由于该公司在事务数据库中记录了每个销售，因此它们可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法来标识倾向于集中购买的产品集。 然后，他们可以根据客户购物篮中已有的项来预测客户可能感兴趣的其他项。  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 关联算法遍历数据集以查找同时出现在某个事例中的项。 然后，该算法按照由 *MINIMUM_SUPPORT* 参数指定的事例数，将出现次数最少的关联项分组为项集。 例如，项集可以为“Mountain 200=Existing, Sport 100=Existing”，并且支持的数目可以为 710。 该算法将根据项集生成规则。 可以使用这些规则根据是否存在该算法标识为重要项的其他特定项，预测数据库中的某项是否存在。 例如，某规则可以为“if Touring 1000=existing and Road bottle cage=existing, then Water bottle=existing”，并且其概率可能为 0.812。 在此例中，该算法发现由于购物篮中存在 Touring 1000 轮胎和水壶套，因此预测购物篮中也可能存在水壶。  
  
 有关该算法以及在挖掘模型中自定义该算法行为并控制结果的参数列表的更多详细说明，请参阅 [Microsoft 关联算法技术参考](microsoft-association-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-association-models"></a>关联模型所必需的数据  
 在准备用于关联规则模型的数据时，应理解特定算法的要求，其中包括所需要的数据量以及使用数据的方式。  
  
 关联规则模型的要求如下：  
  
-   **单键列** 每个模型都必须包含一个用于唯一标识每条记录的数值列或文本列。 不允许复合键。  
  
-   **单个可预测列** 一个关联模型只能有一个可预测列。 通常它是嵌套表的键列，例如列出已购买的产品的字段。 这些值必须是离散或离散化值。  
  
-   **输入列** 输入列必须为离散列。 关联模型的输入数据通常包含在两个表中。 例如，一个表可能包含客户信息，而另一个表可能包含客户购物情况。 您可以使用嵌套表将该数据输入到模型中。 有关嵌套表的详细信息，请参阅[嵌套表（Analysis Services - 数据挖掘）](nested-tables-analysis-services-data-mining.md)。  
  
 有关关联模型支持的内容类型和数据类型的详细信息，请参阅 [Microsoft 关联算法技术参考](microsoft-association-algorithm-technical-reference.md)的“要求”部分。  
  
## <a name="viewing-an-association-model"></a>查看关联模型  
 若要浏览该模型，可以使用 **Microsoft 关联查看器**。 查看关联模型时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会从各个角度展示相关性，从而您可以更好地理解数据中所找到的关系和规则。 查看器中的 **“项集”** 窗格提供最常见组合或项集的详细明细。 **“规则”** 窗格显示从数据中生成的规则列表，添加概率的计算，并根据关联重要性对规则进行排名。 通过依赖关系网络查看器，您可以用可视方式浏览连接各个不同项的方式。 有关详细信息，请参阅 [使用 Microsoft 分类查看器浏览模型](browse-a-model-using-the-microsoft-cluster-viewer.md)。  
  
 如果需要查找有关任一项集和规则的更多详细信息，可以在 [Microsoft 一般内容树查看器](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中浏览模型。 为模型存储的内容包括对每个项集的支持，每个规则的分数以及其他统计信息。 有关详细信息，请参阅[关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 处理完模型后，可以使用规则和项集来做出预测。 在关联模型中，如果有指定项存在，预测将告诉您有可能发生的项，而且预测可以包含诸如概率、支持或重要性等信息。 有关如何创建针对关联模型的查询的示例，请参阅 [关联模型查询示例](association-model-query-examples.md)。  
  
 有关如何创建针对数据挖掘模型的查询的信息，请参阅 [数据挖掘查询](data-mining-queries.md)。  
  
## <a name="performance"></a>性能  
 创建项集和对关联进行计数的过程可能会非常耗时。 尽管[!INCLUDE[msCoName](../../includes/msconame-md.md)]关联规则算法使用优化技术来节省空间并使处理更快，则应了解在如下所示的情况下可能会出现性能问题：  
  
-   数据集很大，包含许多单个项。  
  
-   设置的最小项集大小过小。  
  
 若要尽量缩短处理时间，并降低项集的复杂度，可以在分析数据之前尝试按照类别对关联项进行分组。  
  
## <a name="remarks"></a>备注  
  
-   不支持使用预测模型标记语言 (PMML) 创建挖掘模型。  
  
-   支持钻取。  
  
-   支持使用 OLAP 挖掘模型。  
  
-   支持创建数据挖掘维度。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [使用 Microsoft 关联规则查看器浏览模型](browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [Microsoft 关联算法技术参考](microsoft-association-algorithm-technical-reference.md)   
 [关联模型查询示例](association-model-query-examples.md)  
  
  
