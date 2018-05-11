---
title: MembersWithDataCaption 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0d9683e8440dcbc2d6d4f8793fe9027a14c92ef4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="memberswithdatacaption-element-assl"></a>MembersWithDataCaption 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**MembersWithDataCaption**元素仅由父属性 (换而言之，值[用法](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父元素设置为*父*) 来确定父属性中的数据成员的标题。 有关数据成员的详细信息，请参阅[父子层次结构中的属性](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
 对应的父级的元素**MembersWithDataCaption**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AttributeTranslation>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [MembersWithData 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [AttributeTranslation 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
