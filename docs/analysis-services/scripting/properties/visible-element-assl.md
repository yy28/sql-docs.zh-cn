---
title: "可见元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Visible Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Visible
helpviewer_keywords: Visible element
ms.assetid: 3e9baf1b-351f-4ebf-b57d-13d561f72d6f
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: de9a8d9a56f4842fadc5bcb701463c4f159aaf63
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="visible-element-assl"></a>Visible 元素 (ASSL)
  确定父元素的可见性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|True|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)， [度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **可见**元素确定用户界面组件是否应显示父元素。  
  
 对应的父级的元素**可见**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CalculationProperty>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.CubeHierarchy>， <xref:Microsoft.AnalysisServices.Database>，和<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
