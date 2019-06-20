---
title: RangeMax (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 417f92a00e396952218c6ef04d105245f1e3708e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658966"
---
# <a name="rangemax-dmx"></a>RangeMax (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回为离散化列发现的预测存储桶的高端值。  
  
## <a name="syntax"></a>语法  
  
```  
  
RangeMax(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>适用范围  
 标量列。  
  
## <a name="return-type"></a>返回类型  
 一个标量值。  
  
## <a name="remarks"></a>备注  
 **RangeMax**函数可在[SELECT DISTINCT FROM&#60;模型&#62; &#40;DMX&#41; ](../dmx/select-distinct-from-model-dmx.md)查询。 与这种类型的查询一起使用时，标量列引用可以包含连续或离散的可预测列或输入列。  
  
 与一起使用时[SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)，则**RangeMin**， **RangeMid**，并**RangeMax**函数返回指定存储桶的实际边界值。 例如，如果对一个离散化列执行预测，查询将返回该离散化列中存储桶数的预测值。 **RangeMin**， **RangeMid**，并**RangeMax**函数用于说明预测所指定的存储桶。 当**RangeMax**函数用于 PREDICTION JOIN 语句，标量列引用只能包含离散、 可预测列。  
  
## <a name="examples"></a>示例  
 以下示例返回 Decision Tree 挖掘模型中“年收入”连续列的最小值、最大值和平均值。  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
