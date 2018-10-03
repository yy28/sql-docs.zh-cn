---
title: 值元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.value
- urn:schemas-microsoft-com:xml-analysis#Value
- http://schemas.microsoft.com/analysisservices/2003/engine#Value
helpviewer_keywords:
- Value element
ms.assetid: f87ca7f8-d9fe-4730-a706-5d50fcfe21df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 054da002271711d4b86a08e694b18e01e796b3ea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205709"
---
# <a name="value-element-xmla"></a>Value 元素 (XMLA)
  包含所需的值[特性](attribute-element-xmla.md)要添加的元素[插入](../xml-elements-commands/insert-element-xmla.md)命令，或[单元格](cell-element-xmla.md)元素更新[UpdateCells](../xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[特性](attribute-element-xmla.md)，[单元格](cell-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 对于 `Attribute` 元素，`Value` 元素包含在提交 `Insert` 命令之后该成员应该包含的所需的值。 有关插入成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
 对于 `Cell` 元素，`Value` 元素包含在提交 `UpdateCells` 命令之后该单元应该包含的所需的值。 存储在该单元的写回表中的实际值为该单元的原始值和所需值之间的差值。  
  
 此元素使用的数据类型应与要更新的单元的数据类型相匹配。  
  
 有关更新单元的详细信息，请参阅[更新单元 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [CellOrdinal 元素&#40;XMLA&#41;](cellordinal-element-xmla.md)   
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 元素&#40;XMLA&#41;](../xml-elements-commands/updatecells-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
