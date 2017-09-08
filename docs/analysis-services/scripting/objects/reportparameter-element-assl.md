---
title: "ReportParameter 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ReportParameter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportParameter
helpviewer_keywords:
- ReportParameter element
ms.assetid: 653a5c64-f1af-4796-bb7b-b44a40e52901
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fd3c4b4bd2224c928bcd7864bd797bea36a3d420
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="reportparameter-element---assl"></a>ReportParameter 元素-ASSL
  包含的名称和值的参数传递给[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]在运行时的报表。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ReportParameters>  
      <ReportParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportParameter>  
</ReportParameters>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|  
|子元素|[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 **值**元素必须包含的多维表达式 (MDX) 表达式。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportParameter>。  
  
## <a name="see-also"></a>另请参阅  
 [ReportAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Action 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/action-element-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
