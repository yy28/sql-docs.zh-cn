---
title: "数据挖掘算法 (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
caps.latest.revision: "74"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 092ec27d421f91a1dc4484298139783df1695594
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>数据挖掘算法（Analysis Services – 数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]*算法*在数据挖掘 （或机器学习） 是从数据创建模型的启发式技术并计算一组。 为了创建模型，算法将首先分析您提供的数据，并查找特定类型的模式和趋势。 算法使用此分析在许多次迭代中的结果来查找用于创建挖掘模型的最佳参数。 然后，这些参数应用于整个数据集，以便提取可行模式和详细统计信息。  
  
 算法根据您的数据创建的挖掘模型可以采用多种形式，这包括：  
  
-   说明数据集中的事例如何相关的一组分类。  
  
-   预测结果并描述不同条件是如何影响该结果的决策树。  
  
-   预测销量的数学模型。  
  
-   说明在事务中如何将产品分组到一起的一组规则，以及一起购买产品的概率。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘中提供的算法是最受欢迎、精心研究的从数据派生模式方法。 举例而言，K-means 聚类分析是最古老的聚类分析算法之一，广泛用于许多不同工具中以及许多不同实现和选项中。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘中使用的 K-means 聚类分析的特定实现是由 Microsoft Research 开发的，因而针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]性能进行了优化。 所有 Microsoft 数据挖掘算法都可以广泛地自定义，并且可使用提供的 API 完全编程。 还可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中的数据挖掘组件自动执行模型的创建、定型和重新定型。  
  
 还可以使用符合 OLE DB for Data Mining 规范的第三方算法，或者开发可注册为服务、然后在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘框架中使用的自定义算法。  
  
## <a name="choosing-the-right-algorithm"></a>选择正确的算法  
 为特定的分析任务选择最佳算法很有挑战性。 您可以使用不同的算法来执行同样的业务任务，每个算法会生成不同的结果，而某些算法还会生成多种类型的结果。 例如，您不仅可以将 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策数算法用于预测，而且还可以将它用作一种减少数据集的列数的方法，因为决策树能够识别出不影响最终挖掘模型的列。  
  
### <a name="choosing-an-algorithm-by-type"></a>按类型选择算法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘包括以下算法类型：  
  
-    “分类算法”基于数据集中的其他属性预测一个或多个离散变量。  
  
-   **回归算法**基于数据集中的其他属性预测一个或多个连续数值变量，如利润或亏损。  
  
-    “分段算法”将数据划分为组或分类，这些组或分类的项具有相似的属性。  
  
-    “关联算法”查找数据集中不同属性之间的相关性。 这类算法最常见的应用是创建可用于市场篮分析的关联规则。  
  
-   **顺序分析算法** 汇总数据中的常见顺序或事件，如 Web 站点中的一系列单击或机器维护之前的一系列日志事件。  
  
 但是，限制为您的解决方案中的一种算法是没有必要的。 有经验的分析人员有时候将使用一种算法来确定最高效的输入（即变量），然后应用其他算法以便基于这些数据预测特定结果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘使你可以在单个挖掘结构的基础上生成多个模型，这样，在单个数据挖掘解决方案内，可以使用聚类分析算法、决策树模型和 naïve Bayes 模型来针对数据获取不同视图。 还可以在单个解决方案内使用多种算法来执行单独的任务：例如，可以使用回归来获取财务预测，并且使用神经网络算法执行预测影响因素分析。  
  
### <a name="choosing-an-algorithm-by-task"></a>按任务选择算法  
 为帮助您选择用于特定任务的算法，下表给出了每种算法在传统上用于的任务类型的建议。  
  
|任务示例|可使用的 Microsoft 算法|  
|-----------------------|---------------------------------|  
|**预测离散属性：**<br /><br /> 将预期购买者列表中的客户标记为好或差的潜在客户。<br /><br /> 计算服务器在未来 6 个月内将出现故障的概率。<br /><br /> 将患者结果分类并探讨相关因素。|[Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft Naive Bayes 算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 聚类分析算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 神经网络算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**预测连续属性：**<br /><br /> 预测下一年的销售额。<br /><br /> 根据过去的历史信息和季节趋势，预测网站访问者。<br /><br /> 根据人口统计信息生成风险评分。|[Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 时序算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Microsoft 线性回归算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**预测顺序：**<br /><br /> 执行公司网站的点击流分析。<br /><br /> 分析导致服务器故障的因素。<br /><br /> 捕获和分析门诊访问期间活动的顺序，以便围绕一般的活动形成最佳做法。|[Microsoft 顺序分析和聚类分析算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**查找事务中常见项的组：**<br /><br /> 使用市场篮分析来确定产品摆放。<br /><br /> 建议客户购买其他产品。<br /><br /> 分析来自事件访问者的调查数据，确定哪些活动或展台是相关的，以便计划将来的活动。|[Microsoft 关联算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**查找相似项的组：**<br /><br /> 基于人口统计信息和行为之类的属性，创建患者风险配置文件组。<br /><br /> 按照浏览和购买模式分析用户。<br /><br /> 标识具有相似使用特性的服务器。|[Microsoft 聚类分析算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 顺序分析和聚类分析算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>相关内容  
 下表提供指向一些学习资源的链接，这些学习资源针对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘中提供的各数据挖掘算法：  
  
|||  
|-|-|  
|**基本算法说明**|说明了算法用途和工作原理，概述了算法可能有用的可能的业务方案。|  
||[Microsoft 关联算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Microsoft 聚类分析算法](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Microsoft 决策树算法](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Microsoft 线性回归算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Microsoft 逻辑回归算法](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Microsoft Naive Bayes 算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Microsoft 神经网络算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Microsoft 顺序分析和聚类分析算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Microsoft 时序算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**技术参考**|提供与算法实施有关的技术细节，并且根据需要提供学术方面的参考。 列出了可在模型中设置以便控制算法行为并自定义结果的参数。 描述数据要求并根据需要提供性能提示。|  
||[Microsoft 关联算法技术参考](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Microsoft 聚类分析算法技术参考](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 决策树算法技术参考](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Microsoft 线性回归算法技术参考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft 逻辑回归算法技术参考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Microsoft Naive Bayes 算法技术参考](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Microsoft 神经网络算法技术参考](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Microsoft 顺序分析和聚类分析算法技术参考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Microsoft 时序算法技术参考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**模型内容**|说明在每种类型的数据挖掘模型内信息是如何组织的，并且说明如何解释在各节点中存储的信息。|  
||[关联模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [逻辑回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [Naive Bayes 模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**数据挖掘查询**|提供可用于各模型类型的多个查询。 示例包括可让您了解与模型中的模式有关的详细信息的内容查询以及可帮助您基于这些模式生成预测的预测查询。|  
||[关联模型查询示例](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [聚类分析模型查询示例](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [决策树模型查询示例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [线性回归模型查询示例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [逻辑回归模型查询示例](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [Naive Bayes 模型查询示例](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [神经网络模型查询示例](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [顺序分析和聚类分析模型查询示例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [时序模型查询示例](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>相关任务  
  
|**主题**|**Description**|  
|---------------|---------------------|  
|确定数据挖掘模型使用的算法|[查询用于创建挖掘模型的参数](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|创建自定义插件算法|[插件算法](../../analysis-services/data-mining/plugin-algorithms.md)|  
|使用特定于算法的查看器浏览模型|[数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|使用一般的表格式查看模型的内容|[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|了解如何设置您的数据，并使用算法来创建模型|[挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)  
  
  
