---
title: "RelationshipType 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RelationshipType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RelationshipType
helpviewer_keywords: RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6d93ac8d20a63e5815d388652e35e6d606502492
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="relationshiptype-element-assl"></a>RelationshipType 元素 (ASSL)
  指示是否成员关系[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)可以更改。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*灵活*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*刚性*|不可更改属性和相关属性之间的成员关系。|  
|*灵活*|可更改属性和相关属性之间的成员关系。|  
  
 例如，如果**ZipCode**从一个无法更改**城市**到另一个，从关系**ZipCode**到**城市**被标记为*刚性*。  
  
 对应于的允许值为枚举**RelationshipType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.RelationshipType>。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
