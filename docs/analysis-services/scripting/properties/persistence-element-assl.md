---
title: "持久性元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Persistence Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Persistence
helpviewer_keywords: Persistence element
ms.assetid: dafe3df2-4795-48ea-bebe-33c1a3bf18b6
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f49d7a5eabaeaec3ba9d75bcfec92adda6c0e196
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="persistence-element-assl"></a>Persistence 元素 (ASSL)
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
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*NotPersisted*|源元数据、成员和数据都是动态的。|  
|*元数据*|源元数据是静态的，但是成员和数据是动态的。|  
|*全部*|源元数据、成员和数据都是静态的。|  
  
 对应于的允许值为枚举**持久性**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PersistenceType>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
