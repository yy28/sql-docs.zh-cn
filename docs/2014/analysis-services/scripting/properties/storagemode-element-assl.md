---
title: StorageMode 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- StorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11c7c07f0373d3d271c39146509c73b11c9b7f9b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104937"
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*MOLAP*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集元素&#40;ASSL&#41;](../objects/cube-element-assl.md)，[维度元素&#40;ASSL&#41;](../objects/dimension-element-assl.md)， [MeasureGroup 元素&#40;ASSL&#41;](../objects/group-element-assl.md)，[分区元素&#40;ASSL&#41;](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*MOLAP*|父级使用多维 OLAP (MOLAP) 存储。|  
|*ROLAP*|父级使用关系 OLAP (ROLAP) 存储。|  
|*HOLAP*|父级使用混合 OLAP (HOLAP) 存储。 **注意：** 此值不能用于[维度](../objects/dimension-element-assl.md)父元素。|  
|*InMemory*|父级使用 IMBI 存储。|  
  
 与允许的值相对应的枚举`StorageMode`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.StorageMode>。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `StorageMode` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
