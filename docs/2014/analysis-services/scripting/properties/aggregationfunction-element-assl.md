---
title: AggregationFunction 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90908001138f59d4270811376ac44025148889cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308437"
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
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
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
  
  
