---
title: MembersWithData 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c0311a774b225234aeb63d4d67680e12b693b0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128402"
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
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值`MembersWithData`元素仅由父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父元素设置为*父*) 以确定是否父属性中显示非叶成员的数据成员。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](../../multidimensional-models/parent-child-dimension-attributes.md)。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|隐藏非叶数据。|  
|*NonLeafDataVisible*|非叶数据可见。|  
  
 对应于的允许值为枚举`MembersWithData`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MembersWithData>。  
  
## <a name="see-also"></a>请参阅  
 [MembersWithDataCaption 元素&#40;ASSL&#41;](caption-element-assl.md)   
 [DimensionAttribute 数据类型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  