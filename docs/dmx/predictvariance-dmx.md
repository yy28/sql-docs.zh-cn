---
title: "PredictVariance (DMX) |Microsoft 文档"
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
ms.topic: language-reference
f1_keywords: PredictVariance
dev_langs: DMX
helpviewer_keywords: PredictVariance function
ms.assetid: 3c535237-083a-4102-bdfe-9f3c929e7b2c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: db699ed158838f0d259d5aaf6fdf163542b94d65
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="predictvariance-dmx"></a>PredictVariance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定列的方差。  
  
## <a name="syntax"></a>语法  
  
```  
  
PredictVariance(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>适用范围  
 标量列。  
  
## <a name="return-type"></a>返回类型  
 由指定类型的标量值*\<标量列引用 >*。  
  
## <a name="remarks"></a>注释  
 如果列引用为离散， **PredictVariance**返回 0，因为无法从离散值计算方差。  
  
## <a name="examples"></a>示例  
 以下示例根据 TM Decision Tree 挖掘模型，使用自然预测联接确定某个人是否可能购买自行车，并且还确定该预测的方差。  
  
```  
SELECT  
  [Bike Buyer],  
  PredictVariance([Bike Buyer]) AS [Variance]  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
