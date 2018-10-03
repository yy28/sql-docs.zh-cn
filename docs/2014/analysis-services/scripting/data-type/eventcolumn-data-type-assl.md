---
title: EventColumn 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EventColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EventColumn
helpviewer_keywords:
- EventColumn data type
ms.assetid: c0009f1d-d136-4155-9a1b-7baacda4b552
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 175504777bdba88ef434d275f136becc8241ada0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118037"
---
# <a name="eventcolumn-data-type-assl"></a>EventColumn 数据类型 (ASSL)
  定义一个基元数据类型，表示要为捕获的信息的列[事件](../objects/event-element-assl.md)元素的一部分[跟踪](../objects/trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[ColumnID](../properties/columnid-element-eventcolumn-assl.md)|  
|派生元素|[列](../objects/column-element-assl.md)([列](../collections/columns-element-assl.md)的集合[跟踪](../objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>请参阅  
 [Events 元素&#40;ASSL&#41;](../collections/events-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
