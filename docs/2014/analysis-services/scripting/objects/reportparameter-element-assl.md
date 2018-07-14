---
title: ReportParameter 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1ceef5a3794aaaaec6ac24d9aca6e66384267ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197817"
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReportParameters](../collections/reportparameters-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `Value` 元素必须包含一个多维表达式 (MDX) 表达式。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ReportParameter>。  
  
## <a name="see-also"></a>请参阅  
 [ReportAction 数据类型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [Action 元素&#40;ASSL&#41;](action-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
