---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ColumnID Element (EventColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 71e51ec736b10a6d72621efb2a9b094882ed8057
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129978"
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
  包含要作为的一部分捕获事件的信息的列的标识符 (ID)[跟踪](../objects/trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[EventColumn](../data-type/eventcolumn-data-type-assl.md)|  
|子元素|无。|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`ColumnID`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>请参阅  
 [Columns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Event 元素&#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Events 元素&#40;ASSL&#41;](../collections/events-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  