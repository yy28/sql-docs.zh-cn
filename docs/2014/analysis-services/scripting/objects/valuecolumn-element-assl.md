---
title: ValueColumn 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ValueColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ValueColumn element
ms.assetid: 6c2d6822-8ecc-46df-9fa9-bb92ac716c36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 876d5efb4d4b84e8f42cfd3c360258c8cb67d865
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048138"
---
# <a name="valuecolumn-element-assl"></a>ValueColumn 元素 (ASSL)
  标识提供父元素值的列。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <ValueColumn xsi:type="DataItem">...</ValueColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|默认值|不定（请参阅“备注”）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 如果[NameColumn](namecolumn-element-assl.md)的元素`DimensionAttribute`指定，则相同`DataItem`值用作默认值为`ValueColumn`元素。 如果`NameColumn`的元素`DimensionAttribute`未指定， [KeyColumns](../collections/keycolumns-element-assl.md)的集合`DimensionAttribute`将包含一个[KeyColumn](keycolumn-element-assl.md)表示键列的字符串元素数据类型，相同`DataItem`值用作默认值为`ValueColumn`元素。  
  
 有关详细信息`DataItem`类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表`DataItem`类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 父级对应的元素`NameColumn`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.DimensionAttribute>和<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
