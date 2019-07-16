---
title: 群集 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071081"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回最可能包含输入事例的分类。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>适用范围  
 只有在基础数据挖掘模型支持聚类分析时，此函数才可用。  
  
## <a name="return-type"></a>返回类型  
 **群集**函数不需要参数。  
  
 **群集**函数返回标量值的群集名称。 但是，如果您使用此函数作为另一个函数的参数，您必须将其作为\<群集列引用 >。  
  
## <a name="remarks"></a>备注  
 **群集**还可用作`<`群集列引用`>`有关**PredictHistogram**函数。  
  
## <a name="examples"></a>示例  
 下面的示例使用包含的单一实例查询[PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)和群集函数从 TM Clustering 挖掘模型的每个群集返回单个事例的距离和每个群集中将存在的各个用例的概率。  
  
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
  
## <a name="see-also"></a>请参阅  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
