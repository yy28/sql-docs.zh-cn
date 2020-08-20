---
description: Cluster (DMX)
title: 群集 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0722e53752cfa01ffee086cb8cf1f6a84f82fd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457837"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回最可能包含输入事例的分类。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>适用于  
 只有在基础数据挖掘模型支持聚类分析时，此函数才可用。  
  
## <a name="return-type"></a>返回类型  
 **群集**函数不需要参数。  
  
 **Cluster**函数返回群集名称的标量值。 但是，如果使用此函数作为另一个函数的参数，则必须将其视为 \<cluster column reference> 。  
  
## <a name="remarks"></a>备注  
 **群集**还可以用作 `<` PredictHistogram 函数的群集列引用 `>` 。 **PredictHistogram**  
  
## <a name="examples"></a>示例  
 下面的示例使用带有 [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) 和群集函数的单独查询，以返回 TM 群集挖掘模型的每个分类中单个事例的距离，以及单个事例在每个分类中的概率。  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另请参阅  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
