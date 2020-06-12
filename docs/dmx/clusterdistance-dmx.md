---
title: ClusterDistance （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 149285ac5888d6b23272b40fbbb1aef9cf55909e
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669808"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **ClusterDistance**函数返回输入事例与指定分类之间的距离; 如果未指定分类，则返回输入事例与最可能分类的距离。  
  
## <a name="syntax"></a>语法  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>应用于  
 只有在基础数据挖掘模型支持聚类分析时，此函数才可用。 函数可用于任何类型的聚类分析模型（EM、K 平均值等），但结果会因算法而异。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>注解  
 **ClusterDistance**函数返回输入事例与该输入事例的概率最高的分类之间的距离。  
  
 在 K-Means 聚类分析中，由于所有事例只能属于一个分类，并且成员身份权值为 1.0，因此分类距离始终是 0。 但是，在 K-Means 中，假定每个分类有一个中点。 您可以通过查询或浏览挖掘模型内容中的 NODE_DISTRIBUTION 嵌套表来获取中点的值。 有关详细信息，请参阅 [聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)。  
  
 在默认的 EM 聚类分析方法中，分类中的所有点都被视为具有均等的可能性；因此，分类就没有中点。 特定情况下的**ClusterDistance**的值和特定的分类*N*的计算方式如下：  
  
 ClusterDistance （N） = 1-（membershipWeight （N））  
  
 或者：  
  
 ClusterDistance （N） = 1-ClusterProbability （N））  
  
## <a name="related-prediction-functions"></a>相关预测函数  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了以下可用于查询聚类分析模型的函数：  
  
-   使用[群集 &#40;DMX&#41;](../dmx/cluster-dmx.md)函数返回最可能的分类。  
  
-   使用[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)函数获取事例属于特定分类的概率。 此值用作分类距离的反数。  
  
-   使用[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)函数返回输入事例在每个模型的分类中存在的可能性的直方图。  
  
-   使用[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)函数返回0到1之间的度量值，该度量值指示输入事例根据算法学习的模型存在的可能性。  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>示例 1：获取到可能性最大的分类的分类距离  
 下面的示例返回从指定事例到该事例最有可能属于的分类的距离。  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 示例结果：  
  
|表达式|  
|----------------|  
|0.0477390930705145|  
  
 若要查看是哪个分类，可以替换上一示例中的 `Cluster` 替换为 `ClusterDistance`。  
  
 示例结果：  
  
|$CLUSTER|  
|--------------|  
|分类 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>示例 2：获取到指定分类的距离  
 下面的语句使用挖掘模型内容架构行集返回挖掘模型中分类的节点 ID 和节点标题的列表。 然后，可以在**ClusterDistance**函数中使用节点标题作为群集标识符参数。  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 示例结果：  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|分类 1|  
|002|Cluster 2|  
  
 下面的语句示例返回指定事例到标记为 Cluster 2 的分类的距离。  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 示例结果：  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>另请参阅  
 [群集 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)  
  
  
