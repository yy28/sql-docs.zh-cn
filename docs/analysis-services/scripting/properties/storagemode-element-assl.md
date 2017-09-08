---
title: "StorageMode 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- StorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd6ed7838025255015c3a4103689b772dd035771
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="storagemode-element-assl"></a>StorageMode 元素 (ASSL)
  确定父元素的存储模式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*MOLAP*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)，[维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[分区元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*MOLAP*|父级使用多维 OLAP (MOLAP) 存储。|  
|*ROLAP*|父级使用关系 OLAP (ROLAP) 存储。|  
|*HOLAP*|父级使用混合 OLAP (HOLAP) 存储。<br /><br /> 注意： 此值不是有效的[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)父元素。|  
|*InMemory*|父级使用 IMBI 存储。|  
  
 对应于的允许值为枚举**StorageMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.StorageMode>。  
  
 对应的父级的元素**StorageMode**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
