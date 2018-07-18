---
title: ColumnID 元素 (EventColumn) (ASSL) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82cc6d67aa0c1533b9779b93468fdf8845272cde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245597"
---
# <a name="columnid-element-eventcolumn-assl"></a>ColumnID 元素 (EventColumn) (ASSL)
  包含要作为的一部分捕获的事件的信息的列的标识符 (ID)[跟踪](../objects/trace-element-assl.md)元素。  
  
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
 父级对应的元素`ColumnID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.TraceColumn>。  
  
## <a name="see-also"></a>请参阅  
 [Columns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Event 元素&#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Events 元素&#40;ASSL&#41;](../collections/events-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
