---
title: ProactiveCachingIncrementalProcessingBinding 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProactiveCachingIncrementalProcessingBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProactiveCachingIncrementalProcessingBinding data type
ms.assetid: f49c0c96-4277-417b-9660-d77a4faebd00
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 128d118c5f1a6dd05a8bab5434b1dba1f9f22ce1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027757"
---
# <a name="proactivecachingincrementalprocessingbinding-data-type-assl"></a>ProactiveCachingIncrementalProcessingBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示一种绑定到[ProactiveCaching](../objects/proactivecaching-element-assl.md)过程的重新生成缓存的状态有关的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingIncrementalProcessingBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</ RefreshInterval >  
   <IncrementalProcessingNotification>...</ IncrementalProcessingNotification >  
</ProactiveCachingIncrementalProcessingBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[ProactiveCachingBinding](binding-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)， [RefreshInterval](../properties/refreshinterval-element-assl.md)|  
|派生元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关详细信息`ProactiveCachingBinding`类型，包括的继承层次结构的表`ProactiveCachingBinding`类型，请参阅[ProactiveCachingBinding 数据类型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 有关详细信息`Binding`类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象`Binding`类型和继承层次结构的`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  