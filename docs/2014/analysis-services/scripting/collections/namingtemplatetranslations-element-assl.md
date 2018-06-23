---
title: NamingTemplateTranslations 元素 (ASSL) |Microsoft 文档
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
- NamingTemplateTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslations
helpviewer_keywords:
- NamingTemplateTranslations element
ms.assetid: fde65778-1fa3-490a-9874-8bf2052ef25c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0e22eaea2ab6d19bf1da5620321f0d2002ed382d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017208"
---
# <a name="namingtemplatetranslations-element-assl"></a>NamingTemplateTranslations 元素 (ASSL)
  提供的本地化翻译的集合[NamingTemplate](../properties/namingtemplate-element-assl.md)元素的父代、 [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <NamingTemplateTranslations>  
            <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
...</NamingTemplateTranslations>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../objects/attribute-element-assl.md)类型的[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|[NamingTemplateTranslation](../objects/translation-element-assl.md)类型的[转换](translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 值`NamingTemplateTranslation`元素仅由父属性 (换而言之，值[用法](../properties/usage-element-dimensionattribute-assl.md)元素的父`DimensionAttribute`设置为*父*。)  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  