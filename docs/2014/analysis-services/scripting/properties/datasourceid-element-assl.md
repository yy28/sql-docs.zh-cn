---
title: DataSourceID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 2d71ba53-1684-4da0-8da4-fb75033c971b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d7b2bbf4a3acf952e665d9d5c1acde85905e647
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201557"
---
# <a name="datasourceid-element-assl"></a>DataSourceID 元素 (ASSL)
  标识[数据源](../objects/datasource-element-assl.md)元素与父元素相关联。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeBinding> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</CubeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|取决于上下文|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimensionBinding](../data-type/binding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)， [QueryBinding](../data-type/querybinding-data-type-assl.md)，[DataSourceView](../objects/datasourceview-element-assl.md)， [TableBinding](../data-type/tablebinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中，与 `DataSourceID` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.CubeDimensionBinding>、<xref:Microsoft.AnalysisServices.DimensionBinding>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding>、<xref:Microsoft.AnalysisServices.QueryBinding>、<xref:Microsoft.AnalysisServices.DataSourceView> 和 <xref:Microsoft.AnalysisServices.TableBinding>。  
  
## <a name="see-also"></a>请参阅  
 [ID 元素&#40;ASSL&#41;](id-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
