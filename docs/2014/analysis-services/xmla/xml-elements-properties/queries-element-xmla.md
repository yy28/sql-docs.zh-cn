---
title: 查询元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Queries Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.queries
- urn:schemas-microsoft-com:xml-analysis#Queries
- http://schemas.microsoft.com/analysisservices/2003/engine#Queries
helpviewer_keywords:
- Queries element
ms.assetid: e199412a-23f1-4d11-9e72-11f184ad9602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7fbec1d4ef3c5da759c60039196dc16735da803e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225797"
---
# <a name="queries-element-xmla"></a>Queries 元素 (XMLA)
  包含在基于使用情况的优化期间 [DesignAggregations](query-element-xmla.md) 命令使用的 [Query](../xml-elements-commands/designaggregations-element-xmla.md) 元素的集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Queries>  
      <Query>...</Query>  
   </Queries>  
   ...  
</DesignAggregations>  
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
|父元素|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|子元素|[“数据集属性”](query-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
