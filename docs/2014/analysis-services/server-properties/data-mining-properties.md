---
title: 数据挖掘属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5ed1c47faafeb0c680e6afb6f8e509c426760da2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940715"
---
# <a name="data-mining-properties"></a>数据挖掘属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的数据挖掘服务器属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
 **适用于：** 仅限多维服务器模式  
  
## <a name="non-specific-category"></a>非特定类别  
 `AllowSessionMiningModels`  
 一个布尔值属性，指示是否可以创建会话挖掘模型。  
  
 此属性的默认值为 False，指示不能创建会话挖掘模型。  
  
 `AllowAdHocOpenRowsetQueries`  
 布尔值属性，指示是否允许即席打开行集查询。  
  
 此属性的默认值为 False，指示在会话期间不允许打开行集查询。  
  
 `AllowedProvidersInOpenRowset`  
 字符串属性，标识在打开的行集中允许存在的提供程序，由以逗号/分号分隔的提供程序 ProgID 列表组成，或者为 [全部]。  
  
 `MaxConcurrentPredictionQueries`  
 有符号 32 位整数属性，用于定义并发预测查询的最大数目。  
  
## <a name="algorithms-category"></a>算法类别  
 `Microsoft_Association_Rules\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Association_Rules 算法。  
  
 `Microsoft_Clustering\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Clustering 算法。  
  
 `Microsoft_Decision_Trees\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_DecisionTrees 算法。  
  
 `Microsoft_Naive_Bayes\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_ Naive_Bayes 算法。  
  
 `Microsoft_Neural_Network\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Neural_Network 算法。  
  
 `Microsoft_Sequence_Clustering\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Sequence_Clustering 算法。  
  
 `Microsoft_Time_Series\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Time_Series 算法。  
  
 `Microsoft_Linear_Regression\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Linear_Regression 算法。  
  
 `Microsoft_Logistic_Regression\ Enabled`  
 布尔值属性，指示是否启用 Microsoft_Logistic_Regression 算法。  
  
> [!NOTE]  
>  除了可定义服务器上可用的数据挖掘服务的属性外，还有定义特定算法的行为的数据挖掘属性。 您可在创建单个数据挖掘模型时，对这些属性进行配置（不在服务器级别）。 有关详细信息，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](../data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [物理体系结构 &#40;Analysis Services 数据挖掘&#41;](../data-mining/physical-architecture-analysis-services-data-mining.md)   
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
