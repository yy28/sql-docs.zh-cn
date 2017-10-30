---
title: "AttributeHierarchyVisible 元素 (ASSL) |Microsoft 文档"
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
- AttributeHierarchyVisible Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AttributeHierarchyVisible
helpviewer_keywords:
- AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e79ef9a4a3d248f9641bc6aae44c50acb83b56b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 元素 (ASSL)
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
 [AttributeHierarchyEnabled 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

