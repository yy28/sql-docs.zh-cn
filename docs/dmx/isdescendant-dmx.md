---
title: IsDescendant (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c33a607587ee19de0f47942cd2c1e5b350229a88
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061035"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示当前节点是否源自指定节点。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>返回类型  
 一种布尔值类型。  
  
## <a name="remarks"></a>Remarks  
 **IsDescendant**只用于[SELECT FROM&#60;模型&#62;。内容&#40;DMX&#41; ](../dmx/select-from-model-content-dmx.md)并[FROM&#60;模型&#62;。DIMENSION_CONTENT &#40;DMX&#41; ](../dmx/select-from-model-dimension-content-dmx.md)查询。  
  
## <a name="examples"></a>示例  
 以下示例返回所有属于 IsDescendant 函数中所指定节点后代的事例。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
