---
title: NamingTemplateTranslation 元素 (ASSL) |Microsoft Docs
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
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2832ae5ffe9d5b834fc03f84154fa398b7a19fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167548"
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
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值`NamingTemplateTranslation`元素仅供父属性 (换而言之，值[用法](../properties/usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父级设置为*父*) 来存储的本地化翻译的`NamingTemplate`对于给定语言的值。  
  
 父级对应的元素`NamingTemplateTranslations`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [NamingTemplate 元素&#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
