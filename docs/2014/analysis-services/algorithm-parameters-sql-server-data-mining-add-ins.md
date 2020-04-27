---
title: 算法参数（SQL Server 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e902272c58f1e841a3108199e53d51ac12f8ae4a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062599"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>算法参数（SQL Server 数据挖掘外接程序）
  使用 Excel 表分析工具执行数据挖掘时，无需配置数据挖掘算法或参数；每一种工具都将对数据进行分析并自动选择最佳参数。 但是，如果您要修改模型，或要从头开始创建挖掘模型，可以使用 Excel 数据挖掘客户端提供的多种选项进行自定义。  
  
-   手动创建数据挖掘模型，方法是单击 "**高级**"，然后单击 "**将模型添加到结构**"。  
  
-   使用数据挖掘客户端中的任意建模向导，然后单击 "**参数**" 来控制[!INCLUDE[msCoName](../includes/msconame-md.md)]数据挖掘算法的行为。  
  
-   单击 "**查询**" 以打开 "查询模型向导"，然后单击 "**高级**" 以打开**数据挖掘高级查询编辑器**。 在此编辑器中，可以使用 DMX 模板创建模型。  
  
 您还可以修改已创建的挖掘模型的行为，或者在挖掘模型查看器中设置参数以筛选结果。  
  
## <a name="list-of-algorithm-parameters"></a>算法参数列表  
 所有的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 算法均可通过设置参数来进行自定义。 最佳的参数设置取决于您的数据组合，因此，本主题不对更改参数的效果进行完整的说明。  
  
 下表列出了有关参数，对它们的功能进行了说明，并提供了指向更详细的技术信息的链接。  
  
|参数名称|适用范围|说明|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Microsoft 时序算法|指定一个介于 0 和 1 之间的数字值，用于检测周期。 如果将此值设置为更接近于 1 的数，则允许查找许多接近周期的模式并允许自动生成周期提示。 处理大量的周期提示可能会导致模型定型时间明显加长，模型更准确。 如果将此值设置为更接近于 0 的数，则只检测周期性强的数据的周期。<br /><br /> 默认值为 0.6。|  
|CLUSTER_COUNT|Microsoft Clustering Algorithm<br /><br /> Microsoft 顺序分析和聚类分析算法|指定将由算法生成的大致分类数。 如果无法基于相应的数据生成该大致数目的分类，则算法将生成尽可能多的分类。 如果将 CLUSTER_COUNT 设置为 0，则算法将使用试探性方法最准确地确定要生成的分类数。<br /><br /> 默认值为 10。|  
|CLUSTER_SEED|Microsoft Clustering Algorithm|指定在为建模初始阶段随机生成分类时所要使用的种子数量。<br /><br /> 默认值为 0。|  
|CLUSTERING_METHOD|Microsoft Clustering Algorithm|指定算法要使用的聚类分析方法。 可用的聚类分析方法有：scalable EM (1)、non-scalable EM (2)、scalable K-Means (3) 和 non-scalable K-Means (4)。<br /><br /> 默认值为 1。|  
|COMPLEXITY_PENALTY|Microsoft 决策树算法<br /><br /> Microsoft 时序算法|控制决策树的增长。 该值较低时，会增加拆分数；该值较高时，会减少拆分数。 默认值基于特定模型的属性数，详见以下列表：<br /><br /> 对于 1 到 9 个属性，默认值为 0.5。<br /><br /> 对于 10 到 99 个属性，默认值为 0.9。<br /><br /> 对于 100 或更多个属性，默认值为 0.99。<br /><br /> 注意：在时序模型中，此参数仅适用于使用 ARTxp 算法生成的模型或混合模型。|  
|FORCED_REGRESSOR|Microsoft 决策树算法<br /><br /> Microsoft 线性回归算法|强制算法将指示的列用作回归量，而不考虑算法为这些列计算出的重要性。<br /><br /> 注意：此参数仅用于预测连续属性的决策树。 根据定义，线性回归模型是一种特殊的决策树，可对连续属性进行预测。 但是，任何决策树模型都可包含表示线性回归公式的节点。|  
|FORECAST_METHOD|Microsoft 时序算法|指示是否应使用 ARTxp 算法、ARIMA 算法或二者的组合来生成预测。<br /><br /> 默认值为 MIXED。|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|指定隐藏神经元相对于输入和输出神经元的比率。 以下公式可确定隐藏层中神经元的初始数目：<br /><br /> HIDDEN_NODE_RATIO * SQRT（总输入神经元 \* 总输出神经元）<br /><br /> 默认值为 4.0。|  
|HISTORIC_MODEL_COUNT|Microsoft 时序算法|指定将要生成的历史模型的数量。<br /><br /> 默认值为 1。|  
|HISTORICAL_MODEL_GAP|Microsoft 时序算法|指定两个连续的历史模型之间的时间间隔。 例如，如果将此值设置为 g，则将以 g、2*g、3\*g（依此类推）的时间间隔为被时间段截断的数据生成历史模型。<br /><br /> 默认值为 10。|  
|HOLDOUT_PERCENTAGE|Microsoft 逻辑回归算法<br /><br /> Microsoft Neural Network Algorithm|指定定型数据中用于计算维持错误的事例的百分比，定型挖掘模型时的停止条件中将用到此百分比。<br /><br /> 默认值为 30。<br /><br /> 注意：此参数不同于应用到挖掘结构中的维持百分比值。|  
|HOLDOUT_SEED|Microsoft 逻辑回归算法<br /><br /> Microsoft Neural Network Algorithm|指定一个数字，用作在算法随机确定维持数据时伪随机生成器的种子。 如果此参数设置为 0，算法将基于挖掘模型的名称生成种子，以保证重新处理期间模型内容的一致性。<br /><br /> 默认值为 0。<br /><br /> 注意：此参数不同于应用到挖掘结构中的维持种子值。|  
|INSTABILITY_SENSITIVITY|Microsoft 时序算法|控制预测方差超过特定阈值的点，以及取消预测的 ARTxp 算法。 默认值为 1。<br /><br /> 注意：此参数仅适用于使用 ARTxp 算法的混合模型或模型。|  
|MAXIMUM_INPUT_ATTRIBUTES|Microsoft Clustering Algorithm<br /><br /> Microsoft 决策树算法<br /><br /> Microsoft 线性回归算法<br /><br /> Microsoft Naive Bayes 算法<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 逻辑回归算法|定义算法在调用功能选择之前可以处理的输入属性数。 如果将此值设置为 0，则表示关闭功能选择。<br /><br /> 默认值为 255。|  
|MAXIMUM_ITEMSET_COUNT|Microsoft 关联算法|指定要生成的最大项集数。 如果未指定数目，则该算法将生成所有可能的项集。<br /><br /> 默认值为 200000。|  
|MAXIMUM_ITEMSET_SIZE|Microsoft 关联算法|指定一个项集中允许的最大项数。 将该值设置为 0 将指定对项集的大小没有限制。<br /><br /> 默认值为 3。|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Microsoft 决策树算法<br /><br /> Microsoft 线性回归算法<br /><br /> Microsoft 逻辑回归算法<br /><br /> Microsoft Naive Bayes 算法<br /><br /> Microsoft Neural Network Algorithm|定义算法在调用功能选择之前可以处理的输出属性数。 如果将此值设置为 0，则表示关闭功能选择。<br /><br /> 默认值为 255。|  
|MAXIMUM_SEQUENCE_STATES|Microsoft 顺序分析和聚类分析算法|指定一个顺序可以拥有的最大状态数。 将该值设置为大于 100 的数将导致算法创建一个不提供有意义的信息的模型。<br /><br /> 默认值为 64。|  
|MAXIMUM_SERIES_VALUE|Microsoft 时序算法|指定用于预测的最大值。 此参数可与 MINIMUM_SERIES_VALUE 一起使用，以便将预测限制在预期范围内。 例如，您可以指定任何一天的预测销售数量决不应超过库存产品数量。|  
|MAXIMUM_STATES|Microsoft Clustering Algorithm<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft 顺序分析和聚类分析算法|指定算法支持的最大属性状态数。 如果属性的状态数大于最大状态数，则算法将使用属性的最常用状态，并忽略剩余状态。<br /><br /> 默认值为 100。|  
|MAXIMUM_SUPPORT|Microsoft 关联算法|指定支持项集的事例的最大数目。 如果该值小于 1，则表示事例总计的百分比。 如果此值大于1，则该值表示可以包含项集的事例的绝对值。<br /><br /> 默认值为 1。|  
|MINIMUM_IMPORTANCE|Microsoft 关联算法|指定关联规则的重要性阈值。 将筛选出重要性小于此值的规则。|  
|MINIMUM_ITEMSET_SIZE|Microsoft 关联算法|指定一个项集中允许的最小项数。<br /><br /> 默认值为 1。|  
|MINIMUM_DEPENDENCY_PROBABILITY|Microsoft Naive Bayes 算法|指定输入属性和输出属性之间的最小依赖关系概率。 该值用于限制算法生成的内容大小。 此属性可以设置为 0 到 1 之间的值。 较大的值减少模型内容中的特性数。<br /><br /> 默认值为 0.5。|  
|MINIMUM_PROBABILITY|Microsoft 关联算法|指定规则为 True 的最小概率。 例如，将该值设置为 0.5 将指定不生成概率小于百分之五十的规则。<br /><br /> 默认值为 0.4。|  
|MINIMUM_SERIES_VALUE|Microsoft 时序算法|指定用于任何时序预测的下限约束值。 在任何情况下预测值都不应小于该约束值。|  
|MINIMUM_SUPPORT|Microsoft 关联算法|指定在该算法生成规则之前必须包含项集的事例的最小数目。 将该值设置为小于 1 将指定最小事例数作为事例总计的百分比。 将该值设置为大于 1 的整数将指定最小事例数作为必须包含项集的事例的绝对数。 如果内存有限，则该算法可能会增大此参数的值。<br /><br /> 默认值为 0.03。|  
|MINIMUM_SUPPORT|Microsoft Clustering Algorithm|指定每个分类中的最小事例数。<br /><br /> 默认值为 1。|  
|MINIMUM_SUPPORT|Microsoft 决策树算法|确定在决策树中生成拆分所需的叶事例的最少数量。<br /><br /> 默认值为 10。|  
|MINIMUM_SUPPORT|Microsoft 顺序分析和聚类分析算法|指定每个分类中的最小事例数。<br /><br /> 默认值为 10。|  
|MINIMUM_SUPPORT|Microsoft 时序算法|指定在每个时序树中生成一个拆分所需的最小时间段数。<br /><br /> 默认值为 10。|  
|MISSING_VALUE_SUBSTITUTION|Microsoft 时序算法|指定用于填充历史数据中空白的方法。 默认情况下，数据中不允许存在不规则的空白或参差不齐的边缘。 以下是可用来填充不规则空白或边缘的方法：使用以前的值、使用平均值或使用特定数值常量。|  
|MODELLING_CARDINALITY|Microsoft Clustering Algorithm|指定在聚类分析过程中构建的示例模型数。<br /><br /> 默认值为 10。|  
|PERIODICITY_HINT|Microsoft 时序算法|提供算法的有关数据周期的提示。 例如，如果销售额按年度变化，且序列中的度量单位是月，则周期为 12。 此参数采用 {n [, n]} 格式，其中 n 为任意正数。 方括号 [] 中的 n 是可选项，可以根据需要重复多次。<br /><br /> 默认值为 {1}。|  
|PREDICTION_SMOOTHING|Microsoft 时序算法|控制 ARTXP 和 ARIMA 时序的混合算法。 仅当 FORECAST_METHOD 参数设置为 MIXED 时，该指定值才有效。 值必须介于 0 到 1 之间。 如果值为 0，则模型仅使用 ARTXP。 如果值为 1，则模型仅使用 ARIMA。 值越接近 0，则 ARTXP 的重要性就越高。 值越接近 1，则 ARIMA 的重要性就越高。|  
|SAMPLE_SIZE|Microsoft Clustering Algorithm|如果 CLUSTERING_METHOD 参数设置为其中一个可缩放聚类分析方法，请指定算法在每个传递中使用的事例数。 如果将 SAMPLE_SIZE 参数设置为 0，则会在单个传递中对整个数据集进行聚类分析操作， 从而导致内存和性能发生问题。<br /><br /> 默认值为 50000。|  
|SAMPLE_SIZE|Microsoft 逻辑回归算法<br /><br /> Microsoft Neural Network Algorithm|指定用来给模型定型的事例数。 算法提供程序将使用该数字或不包含在 HOLDOUT_PERCENTAGE 参数指定的维持百分比中的总的事例百分比，取两者中较小值。<br /><br /> 换言之，如果将 HOLDOUT_PERCENTAGE 设置为 30，则算法将使用该参数的值或等于事例总数百分之七十的值，取两者中较小值。<br /><br /> 默认值为 10000。|  
|SCORE_METHOD|Microsoft 决策树算法|确定用于计算拆分分数的方法。 可用选项有：(1) Entropy、(K2) Bayesian with K2 Prior 或 (3) Bayesian Dirichlet Equivalent (BDE) Prior。<br /><br /> 默认值为 3。|  
|SPLIT_METHOD|Microsoft 决策树算法|确定用于拆分节点的方法。 可用选项有：Binary (1)、Complete (2) 或 Both (3)。<br /><br /> 默认值为 3。|  
|STOPPING_TOLERANCE|Microsoft 聚类分析算法技术参考|指定一个值，它可确定何时达到收敛而且算法完成建模。 当分类概率中的整体变化小于 STOPPING_TOLERANCE 参数与模型大小之比时，即达到收敛。<br /><br /> 默认值为 10。|  
  
### <a name="comments"></a>说明  
 有关算法的更多详细信息，请参阅 SQL Server 联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据挖掘外接程序的数据挖掘算法 &#40;&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
