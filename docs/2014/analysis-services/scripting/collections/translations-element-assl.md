---
title: Translations 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Translations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Translations
helpviewer_keywords:
- Translations element
ms.assetid: 7f6b8ff2-e834-44d3-a176-216203158a8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7ea3c98e2263b78f947d75c5b225d2a3a63ef40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061227"
---
# <a name="translations-element-assl"></a>Translations 元素 (ASSL)
  包含的集合[翻译](../objects/translation-element-assl.md)与父元素关联的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action><!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Translations>  
      <Translation>...</Translation>  
      <!-- or -->  
      <Translation xsi:type="AttributeTranslation">...</Translation><!-- parent: DimensionAttribute or ScalarMiningStructureColumn -->  
      <!-- or -->  
      <Translation xsi:type="RelationshipEndTranslation">...</Translation><!-- parent: RelationshipEnd -->  
   </Translations>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)， [AttributeRelationship](../objects/attributerelationship-element-assl.md)， [CalculationProperty](../objects/calculationproperty-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)， [数据库](../objects/database-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[层次结构](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)， [级别](../objects/level-element-assl.md)，[度量值](../objects/measure-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [角度来看](../objects/perspective-element-assl.md)， [RelationshipEnd](../data-type/relationshipend-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)， [TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
  
 **子元素**  
  
|祖先或父级|子元素|  
|------------------------|-------------------|  
|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)或[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[翻译](../objects/translation-element-assl.md)类型的[AttributeTranslation](../data-type/translation-data-type-assl.md)|  
|[RelationshipEnd](../data-type/relationshipendtranslation-element-assl.md)类型的[RelationshipEndTranslation](../data-type/relationshipendtranslation-element-assl.md)|  
|其他|[翻译](../objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.TranslationCollection> 和 <xref:Microsoft.AnalysisServices.AttributeTranslationCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
