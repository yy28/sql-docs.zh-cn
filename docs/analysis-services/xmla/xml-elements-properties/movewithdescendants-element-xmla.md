---
title: MoveWithDescendants 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 518c95efa36c6a234036a1c7f293c3df8283749a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969187"
---
# <a name="movewithdescendants-element-xmla"></a>MoveWithDescendants 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指示是否由父也会更新属性成员的后代[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Update>  
   ...  
   <MoveWithDescendants>...</MoveWithDescendants>  
   ...  
</Update>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **MoveWithDescendants**元素可确定是否**更新**命令不应只更新通过标识的属性成员[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)元素，但此外，这些属性成员的后代也更新。  
  
> [!NOTE]  
>  此属性仅适用于父子层次结构中的属性成员。  
  
 有关更新成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
