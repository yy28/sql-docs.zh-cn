---
title: AttributeHierarchyEnabled 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 334cb5ef8d9496f66760cec9c1e4d261fff43dde
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attributehierarchyenabled-element-assl"></a>AttributeHierarchyEnabled 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定是否为属性启用属性层次结构。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute><!-- or CubeAttribute -->  
   ...  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
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
|父元素|[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **AttributeHierarchyEnabled**元素确定是否由生成属性层次结构[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]属性。 如果未启用属性层次结构，则不能在用户定义的层次结构中使用属性，也不能在多维表达式 (MDX) 语句中引用属性层次结构。  
  
 对应的父级的元素**AttributeHierarchyEnabled**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeAttribute>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [AttributeHierarchyVisible 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
