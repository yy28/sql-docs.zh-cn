---
title: 值元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: deb60f79544e3386b2e79de7b857ee6d36fa2df7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-xmla"></a>Value 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所需的值的[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)要添加的元素[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)命令，或[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)元素更新[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)，[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**属性**元素，**值**元素包含成员应包含后所需的值**插入**命令已提交。 有关插入成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
 有关**单元格**元素，**值**元素包含的单元格应包含后所需的值**UpdateCells**命令已提交。 存储在该单元的写回表中的实际值为该单元的原始值和所需值之间的差值。  
  
 此元素使用的数据类型应与要更新的单元的数据类型相匹配。  
  
 有关更新单元的详细信息，请参阅[更新单元 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CellOrdinal 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [插入元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [UpdateCells 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
