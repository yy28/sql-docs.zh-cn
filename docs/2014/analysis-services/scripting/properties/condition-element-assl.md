---
title: 条件元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Condition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- condition
helpviewer_keywords:
- Condition element
ms.assetid: 9c3cb31c-4aa1-49e4-aeb2-6cab54db0be3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fa61c470eaf39edc883aac73707e86c21a9e24c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227917"
---
# <a name="condition-element-assl"></a>Condition 元素 (ASSL)
  包含多维表达式 (MDX) 表达式，用于确定是否[操作](../objects/action-element-assl.md)父元素应用于目标。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Condition>...</Condition  
      ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Condition` 包含计算结果为布尔值的 MDX 表达式。 如果该表达式返回`True`，则`Action`适用于中指定的目标[目标](target-element-assl.md)元素。 否则，不应用 `Action`。  
  
 父级对应的元素`Condition`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
