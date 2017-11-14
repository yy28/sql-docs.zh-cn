---
title: "CurrentStorageMode 元素 (ASSL) |Microsoft 文档"
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
apiname:
- CurrentStorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CurrentStorageMode
helpviewer_keywords:
- CurrentStorageMode element
ms.assetid: 050c21e4-368b-4ff0-b0c5-349f93fe9747
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 24b284deffbf0d7c6902c132a8a87fd0e40abfb8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ROLAP*|  
|基数|0-1：可出现一次或根本不出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **CurrentStorageMode**元素指示当前正在出于主动缓存，使用的存储模式和适用于父元素的所有属性。  
  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*MOLAP*|父级使用多维 OLAP (MOLAP) 存储。|  
|*ROLAP*|父级使用关系 OLAP (ROLAP) 存储。|  
|*HOLAP*|父级使用混合 OLAP (HOLAP) 存储。<br /><br /> 注意： 此值才有效的[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)父元素。|  
  
 对应于允许的值在枚举**CurrentStorageMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.StorageMode>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

