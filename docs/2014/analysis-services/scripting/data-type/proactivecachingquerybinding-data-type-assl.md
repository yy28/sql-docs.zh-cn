---
title: ProactiveCachingQueryBinding 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingQueryBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingQueryBinding data type
ms.assetid: c1b06e50-9e68-40db-bdab-fc2cb3a8ff64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7b9c4aea38bb66277467275d2cf89a04cc3144a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087627"
---
# <a name="proactivecachingquerybinding-data-type-assl"></a>ProactiveCachingQueryBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示信息，用以[ProactiveCaching](../objects/proactivecaching-element-assl.md)有关表和视图，通过指定需要重新生成缓存的查询的执行中的数据源更改的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</RefreshInterval>  
   <QueryNotification>...</QueryNotification>  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[QueryNotification](../objects/querynotification-element-assl.md)， [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 有关详细信息`ProactiveCachingBinding`类型，包括继承层次结构的表`ProactiveCachingBinding`类型，请参阅[ProactiveCachingBinding 数据类型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 有关详细信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 对象的表`Binding`类型和继承层次结构`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 有关 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
