---
title: AttributeHierarchyVisible 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f66395c1d2f673d2bf1d068bc22bc6ba68384f9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定属性层次结构是否对客户端应用程序可见。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**True**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **AttributeHierarchyVisible**元素确定与特性关联的属性层次结构是否对客户端应用程序可见。 如果此元素设置为**False**，属性层次结构仍然可以用来创建用户定义的层次结构，并且可以引用的多维表达式 (MDX) 语句。  
  
 对应的父级的元素**AttributeHierarchyVisible**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeAttribute>， <xref:Microsoft.AnalysisServices.DimensionAttribute>，和<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [AttributeHierarchyEnabled 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
