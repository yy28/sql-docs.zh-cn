---
title: MembersWithDataCaption 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithDataCaption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 847a355f2517a5a630096e2617a27bdae396e565
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103897"
---
# <a name="memberswithdatacaption-element-assl"></a>MembersWithDataCaption 元素 (ASSL)
  提供用于为系统生成的数据成员创建标题的模板字符串。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeTranslation> <!-- or DimensionAttribute -->  
   ...  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeTranslation](../data-type/translation-data-type-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`MembersWithDataCaption`元素仅供父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父元素设置为*父*) 来确定父属性中的数据成员的标题。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 父级对应的元素`MembersWithDataCaption`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.AttributeTranslation>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [MembersWithData 元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [AttributeTranslation 数据类型&#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
