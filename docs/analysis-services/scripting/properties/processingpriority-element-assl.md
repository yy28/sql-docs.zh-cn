---
title: "ProcessingPriority 元素 (ASSL) |Microsoft 文档"
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
- ProcessingPriority Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProcessingPriority element
ms.assetid: 95d07f1c-ef8d-4e38-9682-ebb7719dbe52
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b7c417953e755171f5baeba30539372f82c0244
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="processingpriority-element-assl"></a>ProcessingPriority 元素 (ASSL)
  确定在后台操作期间（例如迟缓聚合、索引或群集），父对象的处理优先级。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension> <!-- or MeasureGroup, Partition -->  
   ...  
   <ProcessingPriority>...</ProcessingPriority>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|**0**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**ProcessingPriority**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
