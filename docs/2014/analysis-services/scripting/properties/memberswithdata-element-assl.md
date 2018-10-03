---
title: MembersWithData 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17a3fced7327c1fb2211b1c80f774ae859757952
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089638"
---
# <a name="memberswithdata-element-assl"></a>MembersWithData 元素 (ASSL)
  确定是否显示父属性中非叶成员的数据成员。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*NonLeafDataVisible*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`MembersWithData`元素仅供父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父元素设置为*父*) 以确定是否若要显示父属性中非叶成员的数据成员。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|隐藏非叶数据。|  
|*NonLeafDataVisible*|非叶数据可见。|  
  
 与允许的值相对应的枚举`MembersWithData`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MembersWithData>。  
  
## <a name="see-also"></a>请参阅  
 [MembersWithDataCaption 元素&#40;ASSL&#41;](caption-element-assl.md)   
 [DimensionAttribute 数据类型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
