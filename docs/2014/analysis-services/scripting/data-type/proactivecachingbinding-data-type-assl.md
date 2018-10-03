---
title: ProactiveCachingBinding 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCachingBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingBinding data type
ms.assetid: 02e6ff2f-2f18-4607-9198-bb46f113f9ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a8d34019463453b52df520d1c0153420903a0f9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209757"
---
# <a name="proactivecachingbinding-data-type-assl"></a>ProactiveCachingBinding 数据类型 (ASSL)
  定义表示信息的抽象的派生的数据类型[ProactiveCaching](../objects/proactivecaching-element-assl.md)元素有关需要重新生成缓存的数据源更改或重新生成过程的状态。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingBinding>  
   <!-- ProactiveCachingBinding is an abstract base class with no child elements -->  
</ProactiveCachingBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[绑定](binding-data-type-assl.md)|  
|派生数据类型|[ProactiveCachingIncrementalProcessingBinding](proactivecachingincrementalprocessingbinding-data-type-assl.md)， [ProactiveCachingObjectNotificationBinding](proactivecachingobjectnotificationbinding-data-type-assl.md)， [ProactiveCachingQueryBinding](querybinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 有关详细信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 对象的表`Binding`类型和继承层次结构`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 有关 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ProactiveCachingBinding>。  
  
## <a name="inheritance-hierarchy-of-proactivecachingbinding-types"></a>ProactiveCachingBinding 类型的继承层次结构  
 下面的层次结构演示了 `ProactiveCachingBinding` 类型的继承。  
  
 [绑定](binding-data-type-assl.md)元素  
  
 `ProactiveCachingBinding` 元素  
  
 [ProactiveCachingObjectNotificationBinding](proactivecachingobjectnotificationbinding-data-type-assl.md)元素  
  
 [ProactiveCachingInheritedBinding](inheritedbinding-data-type-assl.md)元素  
  
 [ProactiveCachingTablesBinding](proactivecachingtablesbinding-data-type-assl.md)元素  
  
 [ProactiveCachingQueryBinding](querybinding-data-type-assl.md)元素  
  
 [ProactiveCachingIncrementalProcessingBinding](proactivecachingincrementalprocessingbinding-data-type-assl.md)元素  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
