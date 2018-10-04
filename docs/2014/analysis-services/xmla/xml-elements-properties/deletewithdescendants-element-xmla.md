---
title: DeleteWithDescendants 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DeleteWithDescendants Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DeleteWithDescendants
- microsoft.xml.analysis.deletewithdescendants
- urn:schemas-microsoft-com:xml-analysis#DeleteWithDescendants
helpviewer_keywords:
- DeleteWithDescendants element
ms.assetid: adfc9437-aaa7-4364-bcdb-128fcc9a410d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93a6d92e675e0ae016327e064fabb6ec2c012aac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48199937"
---
# <a name="deletewithdescendants-element-xmla"></a>DeleteWithDescendants 元素 (XMLA)
  指示是否属性成员的后代也会删除由父[Drop](../xml-elements-commands/drop-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Drop>  
   ...  
   <DeleteWithDescendants>...</DeleteWithDescendants>  
   ...  
</Drop>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[删除](../xml-elements-commands/drop-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DeleteWithDescendants`元素可确定是否`Drop`命令应删除的标识的属性成员[其中](where-element-xmla.md)元素，但同时要应该删除这些属性成员的后代。  
  
> [!NOTE]  
>  此属性仅适用于父子层次结构中的属性成员。  
  
 有关删除和更新属性成员的详细信息，请参阅[插入、更新和删除成员 (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
