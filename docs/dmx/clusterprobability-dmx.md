---
title: ClusterProbability （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60c95521ba42dc5877c0e10a3f34453a497ad438
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969929"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  返回输入事例属于指定分类的概率。  
  
## <a name="syntax"></a>语法  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>应用到  
 只有在基础数据挖掘模型支持聚类分析时，此函数才可用。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>备注  
 以下语法使用挖掘模型内容架构行集来返回挖掘模型中存在的节点标题。  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 有关使用此语法的详细信息，请参阅[SELECT FROM &#60;model&#62;。内容 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)。 有关挖掘模型内容架构行集的详细信息，请参阅[DMSCHEMA_MINING_MODEL_CONTENT 行集](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126267(v=sql.110))。  
  
 如果 \<node caption> 未指定，则函数将返回输入事例属于最可能分类的概率。 使用**群集**函数返回最可能的分类。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [群集 &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
