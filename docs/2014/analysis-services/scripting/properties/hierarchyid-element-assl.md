---
title: HierarchyID 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- HierarchyID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID element
ms.assetid: 6effe47d-e598-41f8-993a-b2bce49fd7dd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 96fd95f6853f5edd7f7eaa5d6aa9627cc322a1bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024898"
---
# <a name="hierarchyid-element-assl"></a>HierarchyID 元素 (ASSL)
  包含标识符 (ID) [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeHierarchy> <!-- or MeasureGroupHierarchy, PerspectiveHierarchy -->  
      ...  
   <HierarchyID>...</HierarchyID>  
      ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)， [PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应的父级的元素`HierarchyID`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeHierarchy>和<xref:Microsoft.AnalysisServices.PerspectiveHierarchy>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  