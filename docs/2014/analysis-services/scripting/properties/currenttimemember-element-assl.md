---
title: CurrentTimeMember 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CurrentTimeMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CurrentTimeMember
helpviewer_keywords:
- CurrentTimeMember element
ms.assetid: 2e73009c-9f2b-441c-bdf0-ca19b160da4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c8016a1fc492225701c4fe47b60796f475a3c401
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119657"
---
# <a name="currenttimemember-element-assl"></a>CurrentTimeMember 元素 (ASSL)
  定义与维度关联的时间的当前成员[Kpi](../objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Kpi>  
   ...  
   <CurrentTimeMember>...</CurrentTimeMember>  
   ...  
</AggregationDimension>  
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
|父元素|[Kpi](../objects/kpi-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值是计算结果为时间维度中单个成员的多维表达式 (MDX) 语句，用于检索计算关键绩效指标 (KPI) 时的当前时间范围。  
  
 父级对应的元素`CurrentTimeMember`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
