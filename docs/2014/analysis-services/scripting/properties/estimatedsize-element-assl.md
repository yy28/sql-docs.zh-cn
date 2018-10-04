---
title: EstimatedSize 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EstimatedSize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EstimatedSize
helpviewer_keywords:
- EstimatedSize element
ms.assetid: a9c63a22-d424-4f27-a186-5372f7b0224d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ce5a46547488bb81e0ad50890e3588259bad4c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048507"
---
# <a name="estimatedsize-element-assl"></a>EstimatedSize 元素 (ASSL)
  包含父元素的只读估计大小（以字节为单位）。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database> <!-- or MeasureGroup, Partition -->  
   ...  
   <EstimatedSize>...</EstimatedSize>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Long|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../objects/database-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中，与父级对应的元素为 <xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.MeasureGroup> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
