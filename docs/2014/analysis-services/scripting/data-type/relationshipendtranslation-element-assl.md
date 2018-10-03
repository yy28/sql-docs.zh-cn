---
title: RelationshipEndTranslation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 04e09370-fdfe-4051-9998-4a6859ce8c54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0e36c3f114f70c17022e4fe0c11494f5e9c38748
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131517"
---
# <a name="relationshipendtranslation-element-assl"></a>RelationshipEndTranslation 元素 (ASSL)
  定义一个基元数据类型，表示的本地化的翻译[RelationshipEnd](relationshipend-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndTranslation>  
   <Language>...</Language>  
   <Caption>...</Caption>  
   <CollectionCaption>...</Caption>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Annotations>...</Annotations>  
</RelationshipEndTranslation>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|[AttributeTranslation](translation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[翻译](../collections/translations-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)，[标题](../properties/caption-element-assl.md)， [CollectionCaption](../properties/caption-element-assl.md)，[说明](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [语言](../properties/language-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
