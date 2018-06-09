---
title: ClusterProbability (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4d8ce16bb07af07bd2bfd651cf5fc1ae15b7e08
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841680"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回输入事例属于指定分类的概率。  
  
## <a name="syntax"></a>语法  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>适用范围  
 只有在基础数据挖掘模型支持聚类分析时，此函数才可用。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>Remarks  
 以下语法使用挖掘模型内容架构行集来返回挖掘模型中存在的节点标题。  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 有关使用此语法的详细信息，请参阅[SELECT FROM&#60;模型&#62;。内容&#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)。 有关挖掘模型内容架构行集的详细信息，请参阅[DMSCHEMA_MINING_MODEL_CONTENT 行集](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)。  
  
 如果\<节点标题 > 未指定，则该函数返回输入的事例属于最可能分类的概率。 使用**群集**函数以返回最可能的分类。  
  
## <a name="examples"></a>示例  
 以下示例返回指定实例存在于标记为 Cluster 2 的群集中的概率。  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>请参阅  
 [群集&#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
