---
title: RestrictionList 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RestrictionList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cad57213c69c63dbc45e476d0163a46c111bc8a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067947"
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 元素 (XMLA)
  包含 [Discover](../xml-elements-methods-discover.md) 方法使用的限制列和值的集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[限制](restrictions-element-xmla.md)|  
|子元素|限制列和值（请参阅“备注”）。|  
  
## <a name="remarks"></a>备注  
 `RestrictionList` 元素包含限制列的集合，可在这些列上筛选 `Discover` 方法返回的数据。 `RestrictionList` 元素中的每个限制列由一个单独的 XML 元素定义。 限制列的值是 XML 元素中包含的数据，限制列的名称与 XML 元素的名称相对应。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
