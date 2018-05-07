---
title: AttributeRelationship 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 157349b670a939a89d8c1aba5232ecbc19949c2e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="attributerelationship-element-assl"></a>AttributeRelationship 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供有关两个属性之间的关系的详细信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeRelationships>  
      <AttributeRelationship>  
      <AttributeID>...</AttributeID>  
            <RelationshipType>...</RelationshipType>  
      <Cardinality>...</Cardinality>  
      <Optionality >...</Optionality>  
      <OverrideBehavior >...</OverrideBehavior>  
            <Annotations>...</Annotations>  
      <Name>...</Name>  
      <Visible>...</Visible>  
      <Translations>...</Translations>  
   </AttributeRelationship>  
</AttributeRelationships>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)，[基数](../../../analysis-services/scripting/properties/cardinality-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [Optionality](../../../analysis-services/scripting/properties/optionality-element-assl.md)， [OverrideBehavior](../../../analysis-services/scripting/properties/overridebehavior-element-assl.md)， [RelationshipType](../../../analysis-services/scripting/properties/relationshiptype-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AttributeRelationship>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
