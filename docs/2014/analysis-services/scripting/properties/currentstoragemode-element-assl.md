---
title: CurrentStorageMode 元素 (ASSL) |Microsoft 文档
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
- CurrentStorageMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cce7bfd399c0c986a79e919c6227ee604e9ff470
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026213"
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 元素 (ASSL)
  确定父元素的当前存储模式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ROLAP*|  
|基数|0-1：可出现一次或根本不出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../objects/dimension-element-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `CurrentStorageMode` 元素指示当前正在用于主动缓存的存储模式，并且该元素应用于父元素的所有属性。  
  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*MOLAP*|父级使用多维 OLAP (MOLAP) 存储。|  
|*ROLAP*|父级使用关系 OLAP (ROLAP) 存储。|  
|*HOLAP*|父级使用混合 OLAP (HOLAP) 存储。 **注意：** 此值才有效的[分区](../objects/partition-element-assl.md)父元素。|  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `CurrentStorageMode` 的允许值对应的枚举为 <xref:Microsoft.AnalysisServices.StorageMode>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  