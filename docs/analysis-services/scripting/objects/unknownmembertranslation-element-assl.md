---
title: UnknownMemberTranslation 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a10f5a5d571868aaca9e6647792723a28576e785
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029638"
---
# <a name="unknownmembertranslation-element-assl"></a>UnknownMemberTranslation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的转换是为标题[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)元素[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<UnknownMemberTranslations>  
   <UnknownMemberTranslation xsi:type="Translation">...</UnknownMemberTranslation>  
</UnknownMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[转换](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[UnknownMemberTranslations](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**UnknownMemberTranslation**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另请参阅  
 [转换元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
