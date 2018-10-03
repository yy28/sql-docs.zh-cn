---
title: 值元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d338b8607d8515bf89183eeadd24252c55af8fc5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218187"
---
# <a name="value-element-assl"></a>Value 元素 (ASSL)
  包含父元素的值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|任何 simpleType|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|任何 simpleType|  
|其他|String|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)，[批注](../objects/annotation-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)， [ReportFormatParameter](../objects/reportformatparameter-element-asl.md)， [ReportParameter](../objects/reportparameter-element-assl.md)， [ServerProperty](../objects/serverproperty-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Value` 元素包含与父对象关联的值。 `Value` 元素的预期值因父元素而异，如下表中所述。  
  
|父元素|预期值|  
|--------------------|--------------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|算法参数的值。|  
|[批注](../objects/annotation-element-assl.md)|批注的值。|  
|[Kpi](../objects/kpi-element-assl.md)|用于计算关键绩效指标 (KPI) 的值的多维表达式 (MDX) 表达式。|  
|[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)|报表格式参数的值。|  
|[ReportParameter](../objects/reportparameter-element-assl.md)|用于计算报表参数值的 MDX 表达式。|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|当前运行的实例的服务器属性值。|  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Value` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.AlgorithmParameter>、<xref:Microsoft.AnalysisServices.Annotation>、<xref:Microsoft.AnalysisServices.Kpi>、<xref:Microsoft.AnalysisServices.ReportParameter> 和 <xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
