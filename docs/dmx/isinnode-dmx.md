---
description: IsInNode (DMX)
title: IsInNode (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68f88915209a3a15cb7e8f1fd64e9d877655f3ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352343"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示指定的节点是否包含当前事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>返回类型  
 Boolean 类型。  
  
## <a name="remarks"></a>备注  
 **IsInNode** 仅用于 [&#62; &#60;模型中进行选择。&#40;DMX&#41;的事例 ](../dmx/select-from-model-cases-dmx.md) ，并 [从 &#60;模型&#62; 中进行选择。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md) 查询。  
  
## <a name="examples"></a>示例  
 以下示例返回所有用于创建与 IsInNode 函数中所指定节点关联的模型的事例。  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
