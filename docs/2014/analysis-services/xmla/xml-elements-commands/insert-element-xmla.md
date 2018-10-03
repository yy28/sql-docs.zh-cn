---
title: Insert 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Insert Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Insert
- http://schemas.microsoft.com/analysisservices/2003/engine#Insert
- microsoft.xml.analysis.insert
helpviewer_keywords:
- Insert command
ms.assetid: d1137033-cc19-4bcb-b93d-8575f17bea6b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a077a263a66c4684279be6e2f353348f451d5435
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120927"
---
# <a name="insert-element-xmla"></a>Insert 元素 (XMLA)
  在维度中插入属性成员。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Insert>  
      <Object>...</Object>  
      <Attributes>...</Attributes>  
   </Insert>  
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
|子元素|[特性](../xml-elements-properties/attributes-element-xmla.md)，[对象](../xml-elements-properties/object-element-dimension-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Insert` 命令可向已启用写操作的维度中插入新的属性成员。  
  
 有关删除成员的详细信息，请参阅[插入、 更新和删除成员&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [Drop 元素&#40;XMLA&#41;](drop-element-xmla.md)   
 [Update 元素&#40;XMLA&#41;](update-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  
