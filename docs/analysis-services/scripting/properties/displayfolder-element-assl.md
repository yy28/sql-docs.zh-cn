---
title: "DisplayFolder 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DisplayFolder Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc9e0f1479821a0559c9ac105cdbc2fb4f9f666c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="displayfolder-element-assl"></a>DisplayFolder 元素 (ASSL)
  指定要在其中列出父元素的文件夹。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]面向开发人员和管理员的应用程序可能支持的显示文件夹以对多个元素进行分类以可视方式使用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
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
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)，[转换](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 在较大的多维数据集中，可能有几百个度量值和层次结构。 **DisplayFolder**属性定义客户端上的用户外观。 值**DisplayFolder**属性可以包含以下选项之一：  
  
-   为空，表示该度量值不属于文件夹。  
  
-   包含单个文件夹名称，表示该度量值应呈现为属于具有相同名称的文件夹。  
  
-   包含由反斜杠分隔的多个文件夹名称 (\\)，表示嵌入的文件夹层次结构。  
  
 **DisplayFolder**属性适用于**CalculationProperty**元素才的值[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)设置为*成员*.  
  
 对应的父级的元素**DisplayFolder**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CalculationProperty>， <xref:Microsoft.AnalysisServices.Hierarchy>， <xref:Microsoft.AnalysisServices.Kpi>， <xref:Microsoft.AnalysisServices.Measure>，和<xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另请参阅  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Mdxscript 被元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
