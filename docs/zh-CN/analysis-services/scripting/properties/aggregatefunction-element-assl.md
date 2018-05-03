---
title: AggregateFunction 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregateFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregateFunction
helpviewer_keywords:
- AggregateFunction element
ms.assetid: 880b6bd0-d62a-4221-831c-39f748ee84f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c7e713cb8ac1a6bc27bca0cc23f7f4e191850f40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="aggregatefunction-element-assl"></a>AggregateFunction 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义使用的聚合函数的类型[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Sum*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*Sum*|度量值的聚合使用**总和**函数。|  
|*Count*|度量值的聚合使用**计数**函数。|  
|*Min*|度量值的聚合使用**Min**函数。|  
|*Max*|度量值的聚合使用**最大**函数。|  
|*DistinctCount*|度量值的聚合使用**DistinctCount**函数。|  
|*InclusionThresholdSetting*|不聚合度量值。|  
|*ByAccount*|按帐户聚合度量值。|  
|*AverageOfChildren*|通过返回度量值子成员的平均值聚合度量值。|  
|*FirstChild*|通过返回度量值的第一个子成员聚合度量值。|  
|*LastChild*|通过返回度量值的最后一个子成员聚合度量值。|  
|*FirstNonEmpty*|通过返回度量值的第一个非空成员聚合度量值。|  
|*LastNonEmpty*|通过返回度量值的最后一个非空成员聚合度量值。|  
  
 对应于的允许值为枚举**AggregateFunction**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
