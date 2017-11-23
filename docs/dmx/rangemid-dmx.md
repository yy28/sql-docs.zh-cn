---
title: "RangeMid (DMX) |Microsoft 文档"
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
f1_keywords: RangeMid
dev_langs: DMX
helpviewer_keywords: RangeMid function
ms.assetid: 23493d2d-4afd-43d6-b047-d110fcacee51
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 256a0ebe07b2b5dfc132d0e13e1eefbb7ff20687
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回为离散化列发现的预测存储桶的中点值。  
  
## <a name="syntax"></a>语法  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>适用范围  
 离散化的标量列。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>注释  
 如果用于[SELECT FROM #60; 模型 &#62;预测联接 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)、 **RangeMin**， **RangeMid**，和**RangeMax**函数将返回指定的存储桶的实际边界值。 例如，如果对一个离散化列执行预测，查询将返回该离散化列中存储桶数的预测值。 **RangeMin**， **RangeMid**，和**RangeMax**函数描述预测指定的存储桶。 当**RangeMid**使用 PREDICTION JOIN 语句使用函数、 标量列引用只能包含离散、 可预测列。  
  
## <a name="examples"></a>示例  
 以下示例返回 TM Decision Tree 挖掘模型中“年收入”连续列的最小值、最大值和平均值。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMax &#40; DMX &#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
  
