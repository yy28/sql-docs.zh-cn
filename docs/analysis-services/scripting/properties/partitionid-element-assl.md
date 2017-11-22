---
title: "PartitionID 元素 (ASSL) |Microsoft 文档"
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
apiname: PartitionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: PartitionID element
ms.assetid: 95e59c73-5ca4-478e-898d-50ffa4bbe794
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ced5e03a10c37e4b28c467efd03a72c42dadea4d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="partitionid-element-assl"></a>PartitionID 元素 (ASSL)
  将相关联[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)具有父元素、 绑定或外部的绑定元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PartitionBinding>  
   ...  
   <PartitionID>...</PartitionID>  
   ...  
</PartitionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关绑定和扩展的外部绑定的详细信息，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
