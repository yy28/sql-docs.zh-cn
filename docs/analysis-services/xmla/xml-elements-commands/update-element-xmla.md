---
title: 更新元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bb1fee17642935982b4ea67cafe0c9e6320eb45
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="update-element-xmla"></a>Update 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  更新维度中的属性成员。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)， [MoveWithDescendants](../../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)，[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)，[其中](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **更新**命令移动写入的维度中的成员的属性。  
  
 有关更新成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [删除元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
