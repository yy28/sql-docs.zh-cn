---
title: Optionality 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0fc2d3f4d741e25596963ee555d1d164fb9a8b1c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="optionality-element-assl"></a>Optionality 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指示成员的 optionality [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <Optionality>...</OPtionality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*必需*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*必需*|相关属性中的每个成员必须是与拥有的属性中的至少一个成员关联**AttributeRelationship**元素。|  
|*可选*|相关属性中的每个成员不一定要与拥有的属性中的至少一个成员关联**AttributeRelationship**元素。|  
  
 对应于的允许值为枚举**基数**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Optionality>。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
