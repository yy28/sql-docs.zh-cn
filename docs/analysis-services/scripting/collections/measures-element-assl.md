---
title: 测量元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 708aba9db7cc5156a0c765af62e529631ac18892
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028668"
---
# <a name="measures-element-assl"></a>Measures 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的集合[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)与父元素关联的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup> <!-- or AggregationInstance, MeasureGroupBinding (out-of-line), PerspectiveMeasureGroup -->  
   ...  
   <Measures>  
      <Measure>...</Measure>  
   </Measures>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupBinding （外部）](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)， [PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|  
|子元素|[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.MeasureCollection> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasureCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
