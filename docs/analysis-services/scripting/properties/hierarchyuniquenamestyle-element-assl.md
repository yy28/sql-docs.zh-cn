---
title: "HierarchyUniqueNameStyle 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- HierarchyUniqueNameStyle Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- HierarchyUniqueNameStyle element
ms.assetid: 2ac57825-e9e5-4ec4-9856-fa2326d2c43f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e19b3e412b7330d6ef735bf269b72080e031b024
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyuniquenamestyle-element-assl"></a>HierarchyUniqueNameStyle 元素 (ASSL)
  确定如何唯一的名称中包含的层次结构生成[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimension>  
   ...  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*IncludeDimensionName*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*IncludeDimensionName*|包括维度的名称，将其作为层次结构名称的一部分。|  
|*ExcludeDimensionName*|维度的名称不作为层次结构名称的一部分。|  
  
 对应于的父元素**HierarchyUniqueNameStyle**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

