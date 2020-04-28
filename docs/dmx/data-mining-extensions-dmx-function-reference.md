---
title: 数据挖掘扩展插件（DMX）函数引用 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d57ac2db4149178a61424affef5e8948de0063
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070954"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>数据挖掘扩展插件 (DMX) 函数参考
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持一些使用数据挖掘扩展插件 (DMX) 语言的函数。 这些函数扩展了预测查询的结果，在结果中包括了可进一步说明预测的信息。 通过使用这些函数，还可对预测结果的返回方式进行更好的控制。 下表提供了指向资源的链接，有助于您了解如何在 DMX 中使用函数。  
  
|函数|说明|  
|--------------|-----------------|  
|[&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)|列出可用于所有模型类型的函数，并提供指向如何查询特定挖掘模型类型的相关详细信息的链接。|  
|[DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|提供有关如何使用 DMX 构建预测查询的概述。|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|返回一个表，该表包含指定数量的最底层的行，并根据排名表达式按排名的升序排列。|  
  
 下表列出了 DMX 支持的函数。  
  
|函数|说明|  
|--------------|-----------------|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|返回一个表，该表包含表表达式的最后 n 个项目行，依据排名表达式按升序排列。|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|返回一个表，该表包含满足指定百分比表达式，但数量最小的最底层的行，并根据排名表达式按排名的升序排列。|  
|[BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)|返回一个表，该表包含满足指定求和表达式，但数量最小的最底层的行，并根据排名表达式按排名的升序排列。|  
|[分类 (DMX)](../dmx/cluster-dmx.md)|返回最可能包含输入事例的分类。|  
|[ClusterProbability (DMX)](../dmx/clusterprobability-dmx.md)|返回输入事例属于该分类的概率。|  
|[存在 &#40;DMX&#41;](../dmx/exists-dmx.md)|只要指定的 SELECT 语句返回的结果集包含行，就返回 True。|  
|[IsDescendant (DMX)](../dmx/isdescendant-dmx.md)|指示当前节点是否源自指定节点。|  
|[IsInNode (DMX)](../dmx/isinnode-dmx.md)|指示指定节点是否包含事例。|  
|[则 istestcase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|指示事例是否属于测试事例集。|  
|[则 istrainingcase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)|指示事例是否属于定型事例集。|  
|[Lag (DMX)](../dmx/lag-dmx.md)|返回当前事例的日期与数据中最后日期之间的时间段。|  
|[Predict (DMX)](../dmx/predict-dmx.md)|对指定列执行预测。|  
|[PredictAdjustedProbability (DMX)](../dmx/predictadjustedprobability-dmx.md)|返回调整后的指定可预测列的概率。|  
|[PredictAssociation (DMX)](../dmx/predictassociation-dmx.md)|预测列中的关联成员身份。|  
|[PredictCaseLikelihood (DMX)](../dmx/predictcaselikelihood-dmx.md)|返回输入事例适合现有模型的可能性。 此函数只能与聚类分析模型一起使用。|  
|[PredictHistogram (DMX)](../dmx/predicthistogram-dmx.md)|返回一个表，该表包含指定列的直方图。|  
|[PredictNodeId (DMX)](../dmx/predictnodeid-dmx.md)|返回选定事例的 NodeID。|  
|[PredictProbability (DMX)](../dmx/predictprobability-dmx.md)|返回指定列的概率。|  
|[PredictSequence (DMX)](../dmx/predictsequence-dmx.md)|预测序列中接下来的值。|  
|[PredictStdev (DMX)](../dmx/predictstdev-dmx.md)|检索指定列的标准偏差值。|  
|[PredictSupport (DMX)](../dmx/predictsupport-dmx.md)|返回列的支持值。|  
|[PredictTimeSeries (DMX)](../dmx/predicttimeseries-dmx.md)|预测一个时序的未来值。|  
|[PredictVariance (DMX)](../dmx/predictvariance-dmx.md)|返回指定列的方差值。|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|返回为指定离散化列发现的预测存储桶的上限值。|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)|返回为指定离散化列发现的预测存储桶的中点值。|  
|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|返回为离散化列发现的预测存储桶的下限值。|  
|[StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)|返回指定的表挖掘结构列的值。|  
|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|返回一个表，该表包含指定数量的最顶层的行，并根据排名表达式按排名降序排列。|  
|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|返回一个表，该表包含满足指定百分比表达式，但数量最小的最顶层的行，并根据排名表达式按排名降序排列。|  
|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|返回一个表，该表包含满足指定求和表达式，但数量最小的最顶层的行，并根据排名表达式按排名降序排列。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 运算符引用](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 语法元素的数据挖掘扩展插件](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)   
 [DMX 预测查询的结构和用法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
