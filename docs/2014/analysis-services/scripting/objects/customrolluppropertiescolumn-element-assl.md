---
title: CustomRollupPropertiesColumn 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CustomRollupPropertiesColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CustomRollupPropertiesColumn
helpviewer_keywords:
- CustomRollupPropertiesColumn element
ms.assetid: 7f4a9825-c768-4523-acb3-511a5160fd44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e848817a08c2f90a5a4c7466568a6543dbe8c8b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104837"
---
# <a name="customrolluppropertiescolumn-element-assl"></a>CustomRollupPropertiesColumn 元素 (ASSL)
  定义用于提供自定义汇总公式属性的列的详细信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <CustomRollupPropertiesColumn xsi:type="DataItem">...</CustomRollupPropertiesColumn>  
   ...  
</DimensionAttribute>  
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
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 有关其他信息`DataItem`类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表`DataItem`类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 父级对应的元素`CustomRollupPropertiesColumn`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [CustomRollupColumn 元素&#40;ASSL&#41;](column-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
