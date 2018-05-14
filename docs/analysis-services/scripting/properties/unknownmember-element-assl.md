---
title: UnknownMember 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d0cc0d68cdfcc859a4d79d67c3cf61093ecfac60
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="unknownmember-element-assl"></a>UnknownMember 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指示未知成员是否可见。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*可见*|未知成员存在并显示。|  
|*Hidden*|未知成员存在，但不显示。|  
|*InclusionThresholdSetting*|未知成员未使用。|  
  
 对应于的允许值为枚举**UnknownMember**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.UnknownMemberBehavior>。  
  
## <a name="see-also"></a>另请参阅  
 [UnknownMemberName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)   
 [UnknownMemberTranslation 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
