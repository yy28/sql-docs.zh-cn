---
title: ManufacturingFirstWeekOfMonth 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ManufacturingFirstWeekOfMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ManufacturingFirstWeekOfMonth
helpviewer_keywords:
- ManufacturingFirstWeekOfMonth element
ms.assetid: adb76a2f-c6c3-459e-a441-e80adad76ff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb71e35842b43901d8289dbfe64f7d90a19957fb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066529"
---
# <a name="manufacturingfirstweekofmonth-element-assl"></a>ManufacturingFirstWeekOfMonth 元素 (ASSL)
  定义生产月的第一周[TimeBinding](../data-type/binding-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
< TimeBinding>  
   ...  
   <ManufacturingFirstWeekOfMonth>...</ManufacturingFirstWeekOfMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer（1 到 4）|  
|默认值|`1`|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`ManufacturingFirstWeekOfMonth`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.TimeBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
