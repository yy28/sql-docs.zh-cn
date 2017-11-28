---
title: "停止时间元素 (ASSL) |Microsoft 文档"
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
apiname: StopTime Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: StopTime
helpviewer_keywords: StopTime element
ms.assetid: 6f863d53-033b-46e0-9837-e891e739b4b0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 62690b30361e5f52cdc56226e31c209d60e75f1d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="stoptime-element-assl"></a>StopTime 元素 (ASSL)
  指定的日期和时间[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素应停止。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
   ...  
   <StopTime>...</StopTime>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|DateTime|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|无|  
  
 对应于的父元素**停止时间**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另请参阅  
 [跟踪元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
