---
title: EventColumn 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e45f9d2d45cef97186e61fa793eb5644367d5e1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030818"
---
# <a name="eventcolumn-data-type-assl"></a>EventColumn 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个基元数据类型，表示要为捕获的信息的列[事件](../../../analysis-services/scripting/objects/event-element-assl.md)作为的一部分的元素[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|  
|派生元素|[列](../../../analysis-services/scripting/objects/column-element-assl.md)([列](../../../analysis-services/scripting/collections/columns-element-assl.md)集合[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>另请参阅  
 [Events 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
