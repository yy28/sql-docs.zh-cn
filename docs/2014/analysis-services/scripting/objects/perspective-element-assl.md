---
title: Perspective 元素 (ASSL) |Microsoft Docs
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
- Perspective Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b006d7d48c072cb98a68e42c04cf75c4aaa9e04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297397"
---
# <a name="perspective-element-assl"></a>Perspective 元素 (ASSL)
  定义的透视的详细信息[多维数据集](cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
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
|父元素|[透视](../collections/perspectives-element-assl.md)|  
|子元素|[操作](../collections/actions-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[计算](../collections/calculations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DefaultMeasure](measure-element-assl.md)， [描述](../properties/description-element-assl.md)，[维度](../collections/dimensions-element-assl.md)， [ID](../properties/id-element-assl.md)， [Kpi](../collections/kpis-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MeasureGroups](../collections/groups-element-assl.md)，[名称](../properties/name-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 透视提供多维数据集的子集，用于选择要包括的维度、层次结构、属性和其他详细信息，以及定义要包括的数据切片。 一个透视属于一个多维数据集。 不能在透视中覆盖或添加对象；所有维度、层次结构和其他详细信息必须存在于基础多维数据集中。 也不能包括对象，以及将其标记为不可见。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
