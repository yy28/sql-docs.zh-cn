---
title: AggregateFunction 元素 (ASSL) |Microsoft 文档
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
- AggregateFunction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregateFunction
helpviewer_keywords:
- AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e292a0c509a746130493c7df601a9d373096c406
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017420"
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction 元素 (ASSL)
  定义使用的聚合函数的类型[度量值](../objects/measure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
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
|父元素|[度量值](../objects/measure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Sum*|使用 `Sum` 函数聚合度量值。|  
|*计数*|使用 `Count` 函数聚合度量值。|  
|*Min*|使用 `Min` 函数聚合度量值。|  
|*Max*|使用 `Max` 函数聚合度量值。|  
|*DistinctCount*|使用 `DistinctCount` 函数聚合度量值。|  
|*无*|不聚合度量值。|  
|*ByAccount*|按帐户聚合度量值。|  
|*AverageOfChildren*|通过返回度量值子成员的平均值聚合度量值。|  
|*FirstChild*|通过返回度量值的第一个子成员聚合度量值。|  
|*LastChild*|通过返回度量值的最后一个子成员聚合度量值。|  
|*FirstNonEmpty*|通过返回度量值的第一个非空成员聚合度量值。|  
|*LastNonEmpty*|通过返回度量值的最后一个非空成员聚合度量值。|  
  
 对应于的允许值为枚举`AggregateFunction`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  