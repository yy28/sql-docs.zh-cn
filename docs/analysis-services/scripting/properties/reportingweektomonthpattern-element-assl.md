---
title: ReportingWeekToMonthPattern 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 627a662686d5f05c86b64638f0307c54415fbc5a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="reportingweektomonthpattern-element-assl"></a>ReportingWeekToMonthPattern 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的报表周月模式[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*445*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*445*|季度，4 周中第二个月，和 5 周中第三个月的第一个月中的 4 周。|  
|*454*|季度 5 周，第二个月中和第三个月中的 4 周的第一个月中的 4 周。|  
|*544*|中的季度，4 周中的第二个月份和第三个月中的 4 周的第一个月的 5 周。|  
  
 对应于的允许值为枚举**ReportingWeekToMonthPattern**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ReportingWeekToMonthPattern>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
