---
title: IsDescendant (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsDescendant
dev_langs:
- DMX
helpviewer_keywords:
- IsDescendant function
ms.assetid: d9fe7446-edb5-487b-8ea6-c9efaccf6d90
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f28895488169aa0644728f380d66a4dad3ceae94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
 **IsDescendant**仅用在[SELECT FROM&#60;模型&#62;。内容&#40;DMX&#41; ](../dmx/select-from-model-content-dmx.md)和[SELECT FROM&#60;模型&#62;。DIMENSION_CONTENT &#40;DMX&#41; ](../dmx/select-from-model-dimension-content-dmx.md)查询。  
  
## <a name="examples"></a>示例  
 以下示例返回所有属于 IsDescendant 函数中所指定节点后代的事例。  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
