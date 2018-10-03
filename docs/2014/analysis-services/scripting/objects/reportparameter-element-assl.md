---
title: ReportParameter 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReportParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportParameter
helpviewer_keywords:
- ReportParameter element
ms.assetid: 653a5c64-f1af-4796-bb7b-b44a40e52901
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fdc677b6aabd9d07275b977dd3d3af3145ea00a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093457"
---
# <a name="reportparameter-element-assl"></a>ReportParameter 元素 (ASSL)
  包含名称和值的参数传递给[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]在运行时的报表。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReportParameters](../collections/reportparameters-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 `Value` 元素必须包含一个多维表达式 (MDX) 表达式。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportParameter>。  
  
## <a name="see-also"></a>请参阅  
 [ReportAction 数据类型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [Action 元素&#40;ASSL&#41;](action-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
