---
title: AttributeHierarchyDisplayFolder 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AttributeHierarchyDisplayFolder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeHierarchyDisplayFolder
helpviewer_keywords:
- AttributeHierarchyDisplayFolder element
ms.assetid: d4a3aff7-553e-416c-9c42-819a96ae264d
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8edc310c53df3f81651ec7de66e938ac41c4bb31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028029"
---
# <a name="attributehierarchydisplayfolder-element-assl"></a>AttributeHierarchyDisplayFolder 元素 (ASSL)
  指定在其中显示关联的属性层次结构的文件夹。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
      ...  
      <AttributeHierarchyDisplayFolder>...  
   </AttributeHierarchyDisplayFolder>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`AttributeHierarchyDisplayFolder`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  