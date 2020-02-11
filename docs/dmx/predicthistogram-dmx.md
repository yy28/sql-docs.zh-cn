---
title: PredictHistogram （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893851"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回一个表示给定列预测的直方图的表。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>应用于  
 一个标量列引用或群集列引用。 除 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法外，可以与所有算法类型一起使用。  
  
## <a name="return-type"></a>返回类型  
 表。  
  
## <a name="remarks"></a>备注  
 直方图可以生成统计信息列。 返回的直方图的列结构取决于与**PredictHistogram**函数一起使用的列引用的类型。  
  
## <a name="scalar-columns"></a>标量列  
 对于\<标量列引用>， **PredictHistogram**函数返回的直方图包含以下列：  
  
-   要预测的值。  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]数据挖掘算法不支持 **$ProbabilityVariance**。 对于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 算法，此列始终为 0。  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]数据挖掘算法不支持 **$ProbabilityStdev**。 对于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 算法，此列始终为 0。  
  
-   **$AdjustedProbability**  
  
     **$AdjustedProbability**列是数据挖掘[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]规范的[!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB 的扩展。  
  
## <a name="cluster-columns"></a>群集列  
 **PredictHistogram**函数为\<群集列引用返回的直方图> 包含以下列：  
  
-   **$Cluster** （表示群集名称）  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>示例  
 以下示例返回单独查询中 Bike Buyer 列的预测状态。 查询还根据使用**PredictHistogram**函数获取的调整概率，返回 "自行车购买者" 属性的前两个最可能的状态。  
  
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
 [群集 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
