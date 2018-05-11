---
title: 持久性元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6c83c4c9c8ded6f3798644193036228a464d06fd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="persistence-element-assl"></a>Persistence 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定绑定的源数据的哪些部分是动态的并使用指定的频率更新检查[RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Persistence>...</Persistence>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*NotPersisted*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*NotPersisted*|源元数据、成员和数据都是动态的。|  
|*元数据*|源元数据是静态的，但是成员和数据是动态的。|  
|*全部*|源元数据、成员和数据都是静态的。|  
  
 对应于的允许值为枚举**持久性**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PersistenceType>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
