---
title: Drop 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Drop Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Drop
- microsoft.xml.analysis.drop
- http://schemas.microsoft.com/analysisservices/2003/engine#Drop
helpviewer_keywords:
- Drop element
ms.assetid: a5d21db3-743a-4958-b16d-b6816a5ee787
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b723e6ae10ae045ce43c7138ce481ffdab3955bd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194937"
---
# <a name="drop-element-xmla"></a>Drop 元素 (XMLA)
  删除维度的属性成员。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Drop>  
      <Object>...</Object>  
      <DeleteWithDescendants>...</DeleteWithDescendants>  
      <Where>...</Where>  
   </Drop>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[DeleteWithDescendants](../xml-elements-properties/deletewithdescendants-element-xmla.md)，[对象](../xml-elements-properties/object-element-dimension-xmla.md)，[其中](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Drop` 命令可从启用写操作的维度删除属性成员。  
  
 有关删除成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [插入元素&#40;XMLA&#41;](insert-element-xmla.md)   
 [Update 元素&#40;XMLA&#41;](update-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
