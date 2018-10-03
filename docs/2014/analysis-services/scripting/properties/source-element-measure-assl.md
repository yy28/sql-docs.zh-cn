---
title: Source 元素 (Measure) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element (Measure)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 933851f354f14e325608c954ce77ba5f3d034a10
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117314"
---
# <a name="source-element-measure-assl"></a>Source 元素 (Measure) (ASSL)
  包含的值的源的详细信息[度量值](../objects/measure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值](../objects/measure-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Source`的`DataItem`，它可作为`Source`的`Measure`，又可以为类型[RowBinding](../data-type/binding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [MeasureBinding](../data-type/measurebinding-data-type-assl.md)，或[CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md)。  
  
 有关其他信息`DataItem`类型，包括 ASSL 对象和属性表`DataItem`类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 父级对应的元素`Source`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
