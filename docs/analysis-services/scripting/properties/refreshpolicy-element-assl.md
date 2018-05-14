---
title: RefreshPolicy 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d553fc069242c8c9c3ba3348820c81474fd3a668
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  频率确定维度或度量值组的动态部分 (所指定的[持久性](../../../analysis-services/scripting/properties/persistence-element-assl.md)元素) 检查的更改。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|请参阅下表。|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
|祖先或父级|“默认值”|  
|------------------------|-------------------|  
|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|*依据查询*|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|无|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|说明|  
|-----------|-----------------|  
|*依据查询*|每个查询都进行检查，以查看数据源是否已更改。|  
|*ByInterval*|源数据计算机在指定的间隔内的更改仅检查[RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)。|  
  
 对应于的允许值为枚举**RefreshPolicy**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.RefreshPolicy>。  
  
## <a name="see-also"></a>另请参阅  
 [持久性元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
