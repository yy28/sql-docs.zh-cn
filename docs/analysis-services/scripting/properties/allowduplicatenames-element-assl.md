---
title: "AllowDuplicateNames 元素 (ASSL) |Microsoft 文档"
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
apiname: AllowDuplicateNames Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllowDuplicateNames
helpviewer_keywords: AllowDuplicateNames element
ms.assetid: d0a80040-115f-4490-926f-4d64d8977e67
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45beca28a1a17afdf7645d8a42cbab519e51373e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="allowduplicatenames-element-assl"></a>AllowDuplicateNames 元素 (ASSL)
  确定是否允许重复的名称在[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Hierarchy>  
      ...  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**True**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**AllowDuplicateNames**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
