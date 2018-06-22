---
title: AttributeAllMemberTranslations 元素 (ASSL) |Microsoft 文档
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
- AttributeAllMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeAllMemberTranslations
helpviewer_keywords:
- AttributeAllMemberTranslations element
ms.assetid: 1a0d86ea-d95d-4d93-b321-acd35ed4ac26
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fa787c7c3731962690c1b8d25e736f061caf74e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016483"
---
# <a name="attributeallmembertranslations-element-assl"></a>AttributeAllMemberTranslations 元素 (ASSL)
  包含维度“全部”成员标题对应的翻译的集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
   ...  
   <AttributeAllMemberTranslations>  
      <AttributeAllMemberTranslation xsi:type="Translation">...</AttributeAllMemberTranslation>  
   </AttributeAllMemberTranslations>  
      ...  
</Dimension>  
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
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|[AttributeAllMemberTranslation](../objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`AttributeAllMemberTranslations`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>请参阅  
 [转换元素&#40;ASSL&#41;](translations-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  