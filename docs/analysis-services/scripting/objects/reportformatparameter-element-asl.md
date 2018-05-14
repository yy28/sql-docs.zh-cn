---
title: ReportFormatParameter 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 48bf728dc79b669393e79de8bbf1d872713493e0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="reportformatparameter-element---asl"></a>ReportFormatParameter 元素-ASL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的名称和值的一个参数，指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]报表格式在运行时。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|  
|子元素|[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ReportFormatParameter**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另请参阅  
 [ReportAction 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Action 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
