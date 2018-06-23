---
title: RelationshipType 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- RelationshipType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a2e5b5ec9e9591a45a80f099397ed6568a986313
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129975"
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 元素 (ASSL)
  指示是否成员关系[AttributeRelationship](../objects/attributerelationship-element-assl.md)可以更改。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*灵活*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*刚性*|不可更改属性和相关属性之间的成员关系。|  
|*灵活*|可更改属性和相关属性之间的成员关系。|  
  
 例如，如果`ZipCode`从一个无法更改`City`到另一个，从关系`ZipCode`到`City`被标记为*刚性*。  
  
 对应于的允许值为枚举`RelationshipType`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.RelationshipType>。  
  
## <a name="see-also"></a>请参阅  
 [属性和属性层次结构](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  