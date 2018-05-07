---
title: ProactiveCachingQueryBinding 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b5ca3bd06b429d87f2fee4dfd4d9ed32b0449960
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="proactivecachingquerybinding-data-type-assl"></a>ProactiveCachingQueryBinding 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个派生的数据类型，表示信息，用以[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关数据源所更改的表和视图，通过指定需要重新生成缓存的查询的执行标识的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCachingQueryBinding>  
   <!-- The following elements extend ProactiveCachingBinding -->  
   <RefreshInterval>...</RefreshInterval>  
   <QueryNotification>...</QueryNotification>  
</ProactiveCachingQueryBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)， [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)|  
|派生元素|無|  
  
## <a name="remarks"></a>注释  
 有关详细信息**ProactiveCachingBinding**类型，包括的继承层次结构的表**ProactiveCachingBinding**类型，请参阅[ProactiveCachingBinding 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)。  
  
 有关详细信息**绑定**类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象**绑定**类型和继承层次结构的**绑定**类型，请参阅[绑定数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定 & #40;SSAS 多维 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
