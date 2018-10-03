---
title: 格式元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Format Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ed7cf229d4ef65e324a59d2d9292948ae530147
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228007"
---
# <a name="format-element-assl"></a>Format 元素 (ASSL)
  包含的所需的格式[DataItem](../data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
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
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 允许值`Format`元素是 Microsoft Office Excel 格式，以及字符串*TrimRight*， *TrimLeft*， *TrimAll*，和*TrimNone*。 修整*TrimRight*是默认值。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|任何 Excel 格式的字符串|根据指定的命名格式字符串或自定义格式字符串设置数据的格式。 可指定 Excel 支持的任何格式的字符串。|  
|*TrimAll*|对数据的左侧和右侧进行修整。|  
|*TrimLeft*|对数据的左侧进行修整。|  
|*TrimNone*|不修整数据。|  
|*TrimRight*|对数据的右侧进行修整。|  
  
 父级对应的元素`Format`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
