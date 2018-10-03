---
title: Visibility 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Visibility Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Visibility
helpviewer_keywords:
- Visibility element
ms.assetid: 59372ebf-af52-4d60-bf9b-bb1644ae9865
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0ec079bcdfefb84f5d7b9e1ea24b5c16b001f16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216627"
---
# <a name="visibility-element-assl"></a>Visibility 元素 (ASSL)
  定义的可见性[批注](../objects/annotation-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Annotation>  
   ...  
   <Visibility>...</Visibility>  
   ...  
</Annotation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[批注](../objects/annotation-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*SchemaRowset*|该批注在架构行集中是可见的。|  
|*无*|该批注不可见。|  
  
 与允许的值相对应的枚举`Visibility`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
