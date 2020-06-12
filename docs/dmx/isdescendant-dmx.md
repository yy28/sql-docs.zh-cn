---
title: IsDescendant （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ef32a9e133c199aae0779c819736d77e0d15c45
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670061"
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
  
## <a name="remarks"></a>注解  
 **IsDescendant**仅用于[&#62; &#60;模型中进行选择。内容 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)并[从 &#60;模型&#62; 中进行选择。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)查询。  
  
## <a name="examples"></a>示例  
 以下示例返回所有属于 IsDescendant 函数中所指定节点后代的事例。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)  
  
  
