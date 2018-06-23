---
title: 更新元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Update Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords:
- Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 68eb54e24daccb08a77cc88b2396d31114a29b25
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124416"
---
# <a name="update-element-xmla"></a>Update 元素 (XMLA)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[属性](../xml-elements-properties/attributes-element-xmla.md)， [MoveWithDescendants](../xml-elements-properties/movewithdescendants-element-xmla.md)，[对象](../xml-elements-properties/object-element-dimension-xmla.md)，[其中](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Update` 命令可在启用写操作的维度内移动属性成员。  
  
 有关更新成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [删除元素&#40;XMLA&#41;](drop-element-xmla.md)   
 [插入元素&#40;XMLA&#41;](insert-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  