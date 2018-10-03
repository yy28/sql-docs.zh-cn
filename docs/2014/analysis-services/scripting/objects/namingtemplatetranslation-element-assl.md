---
title: NamingTemplateTranslation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplateTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslation
helpviewer_keywords:
- NamingTemplateTranslation element
ms.assetid: 4a97a31d-23bc-4afd-a4dc-bc0ad7121f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7689c1b2d83abb7673253550e133cd0fa0ea5e20
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086249"
---
# <a name="namingtemplatetranslation-element-assl"></a>NamingTemplateTranslation 元素 (ASSL)
  提供的本地化的翻译[NamingTemplate](../properties/namingtemplate-element-assl.md)父元素[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<NamingTemplateTranslations>  
   <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
</NamingTemplateTranslations>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[翻译](translation-element-assl.md)|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`NamingTemplateTranslation`元素仅供父属性 (换而言之，值[用法](../properties/usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父级设置为*父*) 来存储的本地化翻译的`NamingTemplate`对于给定语言的值。  
  
 父级对应的元素`NamingTemplateTranslations`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [NamingTemplate 元素&#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
