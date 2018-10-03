---
title: FiscalYearName 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- FiscalYearName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FiscalYearName
helpviewer_keywords:
- FiscalYearName element
ms.assetid: ce613a21-6890-4796-aac5-b029eca46255
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9acbbcdcf1695228cf197c1a29f653d01ccbd320
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083427"
---
# <a name="fiscalyearname-element-assl"></a>FiscalYearName 元素 (ASSL)
  定义的会计年度名称的命名约定[TimeBinding](../data-type/binding-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TimeBinding>  
   ...  
   <FiscalYearName>...</FiscalYearName>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*NextCalendarYearName*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*CalendarYearName*|向会计年度分配当前日历年的名称。|  
|*NextCalendarYearName*|向会计年度分配下一日历年的名称。|  
  
 与允许的值相对应的枚举`FiscalYearName`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.FiscalYearName>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
