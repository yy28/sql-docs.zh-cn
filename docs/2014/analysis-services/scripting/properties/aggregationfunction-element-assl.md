---
title: AggregationFunction 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationFunction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 453d51d678a8e721eaa7fa280e23248c66019b5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153207"
---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction 元素 (ASSL)
  包含要用于帐户类型的聚合函数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Sum*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../objects/account-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下列字符串之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Sum*|使用 `Sum` 函数聚合度量值。|  
|*计数*|使用 `Count` 函数聚合度量值。|  
|*Min*|使用 `Min` 函数聚合度量值。|  
|*Max*|使用 `Max` 函数聚合度量值。|  
|*DistinctCount*|使用 `DistinctCount` 函数聚合度量值。|  
|*无*|不聚合度量值。|  
|*AverageOfChildren*|通过返回度量值子成员的平均值聚合度量值。|  
|*FirstChild*|通过返回度量值的第一个子成员聚合度量值。|  
|*LastChild*|通过返回度量值的最后一个子成员聚合度量值。|  
|*FirstNonEmpty*|通过返回度量值的第一个非空成员聚合度量值。|  
|*LastNonEmpty*|通过返回度量值的最后一个非空成员聚合度量值。|  
  
 与允许的值相对应的枚举`AggregationFunction`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>请参阅  
 [帐户元素&#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
