---
title: Kpi 元素 (ASSL) |Microsoft Docs
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
- Kpi Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Kpi
helpviewer_keywords:
- Kpi element
ms.assetid: 1979a58f-97a8-4c1a-aa65-dcfb6d2404cf
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27b0bcbe2ddaabcc7b3f9ef16f3fa620a8c2db38
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235637"
---
# <a name="kpi-element-assl"></a>Kpi 元素 (ASSL)
  在定义关键绩效指标 (KPI)[多维数据集](cube-element-assl.md)元素或[角度来看](perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Kpis>  
   <Kpi> <!-- ancestor: Cube -->  
            <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DisplayFolder>...</DisplayFolder>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <Value>...</Value>  
            <Goal>...</Goal>  
      <Status>...</Status>  
      <Trend>...</Trend>  
      <TrendGraphic>...</TrendGraphic>  
      <StatusGraphic>...</StatusGraphic>  
      <CurrentTimeMember>...</CurrentTimeMember>  
      <Annotations>...</Annotations>  
   </Kpi>  
   <!-- or -->  
   <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- ancestor: Perspective -->  
   </Kpi>  
</Kpis>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[Cube](cube-element-assl.md)|InclusionThresholdSetting|  
|[透视](../data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Kpi](../collections/kpis-element-assl.md)|  
  
## <a name="child-elements"></a>子元素  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[多维数据集](../collections/annotations-element-assl.md)， [AssociatedMeasureGroupID](../properties/id-element-assl.md)， [CurrentTimeMember](member-element-assl.md)，[说明](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [目标](../properties/goal-element-assl.md)， [ID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)，[状态](../properties/status-element-assl.md)， [StatusGraphic](../properties/statusgraphic-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[趋势](../properties/trend-element-assl.md)， [TrendGraphic](../properties/trendgraphic-element-assl.md)，[值](../properties/value-element-assl.md)|  
|[透视](perspective-element-assl.md)|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.Kpi> 和 <xref:Microsoft.AnalysisServices.PerspectiveKpi>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
