---
title: EstimatedRows 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5156360620c3790fc7cebb5e958b6001ef014d86
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="estimatedrows-element-assl"></a>EstimatedRows 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含由父元素表示的估计行数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationDesign> <!-- or Cube, MeasureGroup, MeasureGroupBinding, Partition -->  
   ...  
   <EstimatedRows>...</EstimatedRows>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**EstimatedRows**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AggregationDesign>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MeasureGroupBinding>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
