---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dcbc88925b788c90f965e0b3b526979047f96b38
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含要作为的一部分捕获事件的信息的列的标识符 (ID)[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|子元素|无。|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ColumnID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [Columns 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Event 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Events 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
