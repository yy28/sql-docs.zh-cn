---
title: 条件元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2edc8a241e92987c4cde54c58576c60abb257c3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015526"
---
# <a name="condition-element-assl"></a>Condition 元素 (ASSL)
  包含的多维表达式 (MDX) 表达式，它确定是否[操作](../objects/action-element-assl.md)父元素将应用到目标。  
  
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
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Condition` 包含计算结果为布尔值的 MDX 表达式。 如果表达式返回`True`，则`Action`适用于中指定的目标[目标](target-element-assl.md)元素。 否则，不应用 `Action`。  
  
 对应于的父元素`Condition`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  