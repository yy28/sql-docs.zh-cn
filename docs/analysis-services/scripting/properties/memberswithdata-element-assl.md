---
title: MembersWithData 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 69a123db59161a15ddf947271b892abaa5658847
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="memberswithdata-element-assl"></a>MembersWithData 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*NonLeafDataVisible*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**MembersWithData**元素仅由父属性 (换而言之，值[用法](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父元素设置为*父*) 以确定是否在父属性中显示非叶成员的数据成员。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|隐藏非叶数据。|  
|*NonLeafDataVisible*|非叶数据可见。|  
  
 对应于的允许值为枚举**MembersWithData**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MembersWithData>。  
  
## <a name="see-also"></a>另请参阅  
 [MembersWithDataCaption 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)   
 [DimensionAttribute 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
