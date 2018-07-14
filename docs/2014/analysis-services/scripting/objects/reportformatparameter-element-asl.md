---
title: ReportFormatParameter 元素 (ASSL) |Microsoft Docs
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
- ReportFormatParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportFormatParameter
helpviewer_keywords:
- ReportFormatParameter element
ms.assetid: 064a8683-c44b-4261-be4d-32226d3d3119
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfcc98e3abe60296e7ee28b57bc54fe89f5c2abe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245577"
---
# <a name="reportformatparameter-element-assl"></a>ReportFormatParameter 元素 (ASSL)
  包含名称和指定参数的值如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]报表在运行时的格式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ReportFormatParameters>  
   <ReportFormatParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportFormatParameter>  
</ReportFormatParameters>  
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
|父元素|[ReportFormatParameters](../collections/reportformatparameters-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 父级对应的元素`ReportFormatParameter`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>请参阅  
 [ReportAction 数据类型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [Action 元素&#40;ASSL&#41;](action-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
