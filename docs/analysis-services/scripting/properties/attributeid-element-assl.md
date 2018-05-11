---
title: AttributeID 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bf1ed6637865fa00723700bfe7c390c32e92dd43
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attributeid-element-assl"></a>AttributeID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含与父元素关联的属性的 ID。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationAttribute> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <AttributeID>...</AttributeID>  
   ...  
</AggregationAttribute>  
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
|父元素|[AggregationAttribute](../../../analysis-services/scripting/data-type/aggregationattribute-data-type-assl.md)， [AggregationDesignAttribute](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)， [AggregationInstanceAttribute](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)， [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)， [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)， [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**AttributeID**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AggregationAttribute>， <xref:Microsoft.AnalysisServices.AggregationDesignAttribute>， <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>， <xref:Microsoft.AnalysisServices.AttributeBinding>， <xref:Microsoft.AnalysisServices.AttributePermission>， <xref:Microsoft.AnalysisServices.AttributeRelationship><xref:Microsoft.AnalysisServices.CubeAttribute>， <xref:Microsoft.AnalysisServices.CubeAttributeBinding>， <xref:Microsoft.AnalysisServices.PerspectiveAttribute>，和<xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
