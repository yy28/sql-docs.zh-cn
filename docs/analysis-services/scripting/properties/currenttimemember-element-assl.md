---
title: "CurrentTimeMember 元素 (ASSL) |Microsoft 文档"
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
apiname: CurrentTimeMember Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CurrentTimeMember
helpviewer_keywords: CurrentTimeMember element
ms.assetid: 2e73009c-9f2b-441c-bdf0-ca19b160da4f
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd972a0c5af394cd2e573b5d6111fd5fff2bf3cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="currenttimemember-element-assl"></a>CurrentTimeMember 元素 (ASSL)
  定义与维度关联的时间的当前成员[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Kpi>  
   ...  
   <CurrentTimeMember>...</CurrentTimeMember>  
   ...  
</AggregationDimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值是计算结果为时间维度中单个成员的多维表达式 (MDX) 语句，用于检索计算关键绩效指标 (KPI) 时的当前时间范围。  
  
 对应于的父元素**CurrentTimeMember**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
