---
title: PredictHistogram (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictHistogram
dev_langs:
- DMX
helpviewer_keywords:
- PredictHistogram function
ms.assetid: 85ffc542-96e7-4f58-aaa3-34d76befcedf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a7b6c9df43d66d69b9dea1e06bea646a6a31d4dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回一个表示给定列预测的直方图的表。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>适用范围  
 一个标量列引用或群集列引用。 除 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法外，可以与所有算法类型一起使用。  
  
## <a name="return-type"></a>返回类型  
 表。  
  
## <a name="remarks"></a>注释  
 直方图可以生成统计信息列。 返回的直方图的列结构取决于与一起使用的列引用的类型**PredictHistogram**函数。  
  
## <a name="scalar-columns"></a>标量列  
 有关\<标量列引用 >，直方图， **PredictHistogram**函数将返回包含以下各列：  
  
-   要预测的值。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 不支持数据挖掘算法 **$ProbabilityVariance**。 对于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 算法，此列始终为 0。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] 不支持数据挖掘算法 **$ProbabilityStdev**。 对于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 算法，此列始终为 0。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**列为[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]扩展[!INCLUDE[msCoName](../includes/msconame-md.md)]OLE DB 数据挖掘的规范。  
  
## <a name="cluster-columns"></a>群集列  
 直方图， **PredictHistogram**函数返回\<群集列引用 > 包含以下各列：  
  
-   **$Cluster** （表示群集名称）  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>示例  
 以下示例返回单独查询中 Bike Buyer 列的预测状态。 该查询还返回 Bike Buyer 属性，根据使用获取的调整后的概率的顶部的两个最有可能状态**PredictHistogram**函数。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另请参阅  
 [群集&#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [数据挖掘算法 & #40;Analysis Services-数据挖掘 & #41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
