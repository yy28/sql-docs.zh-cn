---
title: DisplayFolder 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DisplayFolder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73de197b50ebd3636cb97e6a011fee1e8c3a71af
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220097"
---
# <a name="displayfolder-element-assl"></a>DisplayFolder 元素 (ASSL)
  指定要在其中列出父元素的文件夹。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 开发人员和管理员的应用程序可能支持使用显示文件夹来直观地对多个元素进行分类。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)，[层次结构](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[度量值](../objects/measure-element-assl.md)，[翻译](../objects/translation-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在较大的多维数据集中，可能有几百个度量值和层次结构。 `DisplayFolder` 属性可定义客户端的用户外观。 `DisplayFolder` 属性的值可包含任何下列选项之一：  
  
-   为空，表示该度量值不属于文件夹。  
  
-   包含单个文件夹名称，表示该度量值应呈现为属于具有相同名称的文件夹。  
  
-   包含由反斜杠分隔的多个文件夹名称 (\\)，表示嵌入的文件夹层次结构。  
  
 `DisplayFolder`属性适用于`CalculationProperty`仅当元素的值[CalculationType](calculationtype-element-assl.md)设置为*成员*。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `DisplayFolder` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.CalculationProperty>、<xref:Microsoft.AnalysisServices.Hierarchy>、<xref:Microsoft.AnalysisServices.Kpi>、<xref:Microsoft.AnalysisServices.Measure> 和 <xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>请参阅  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
