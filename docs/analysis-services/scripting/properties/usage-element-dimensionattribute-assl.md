---
title: 使用情况元素 (DimensionAttribute) (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b1bdeccce7de60806463071c9595c0e47219c376
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="usage-element-dimensionattribute-assl"></a>Usage 元素 (DimensionAttribute) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  说明如何使用属性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Usage>...</Usage>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Regular*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Regular*|该属性为常规属性。|  
|*Key*|该属性为键属性。|  
|*Parent*|该属性为父属性。|  
  
 对应于的允许值为枚举**用法**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AttributeUsage>。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
