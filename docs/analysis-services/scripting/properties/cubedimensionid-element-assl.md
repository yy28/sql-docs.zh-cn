---
title: CubeDimensionID 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4702fab97ade8bf9520d9e4f54cf8df392074a6b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cubedimensionid-element-assl"></a>CubeDimensionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)与父元素相关联的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesignDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeDimensionID>...</CubeDimensionID>  
   ...  
</AggregationDesignDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)， [AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)， [AggregationInstanceCubeDimension](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)， [MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)， [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)， [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**CubeDimensionID**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.CubeAttributeBinding>， <xref:Microsoft.AnalysisServices.CubeDimensionBinding>， <xref:Microsoft.AnalysisServices.CubeDimensionPermission>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimensionBinding>，和<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
