---
title: 应用程序元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Application Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Application
helpviewer_keywords:
- Application element
ms.assetid: dfd780ad-f643-4a1c-b58b-34271ae91240
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b4a9b82bef51b02d65c934a6b8adbbbdb30e2e4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200387"
---
# <a name="application-element-assl"></a>Application 元素 (ASSL)
  标识关联的应用程序[操作](../objects/action-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Application>...</Application>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)或其派生的元素之一： [DrillThroughAction](../data-type/action-data-type-assl.md)， [ReportAction](../data-type/reportaction-data-type-assl.md)， [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 客户端应用程序可以使用 `Application` 元素确定哪些操作适用于给定的应用程序。 客户端应用程序负责计算此元素的值。  
  
 父级对应的元素`Application`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [Actions 元素&#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
