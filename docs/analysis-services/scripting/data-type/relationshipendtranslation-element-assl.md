---
title: "RelationshipEndTranslation 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 04e09370-fdfe-4051-9998-4a6859ce8c54
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4629f3fda5e70d9876adc54d5c8b0d3a00a49196
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="relationshipendtranslation-element-assl"></a>RelationshipEndTranslation 元素 (ASSL)
  定义一个基元数据类型，表示的本地化的翻译[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[标题](../../../analysis-services/scripting/properties/caption-element-assl.md)， [CollectionCaption](../../../analysis-services/scripting/properties/caption-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)，[语言](../../../analysis-services/scripting/properties/language-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

