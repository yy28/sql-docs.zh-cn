---
title: 透视元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Perspective Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bf23f3a033a4600d3c3022c5e074c693e531d890
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="perspective-element-assl"></a>Perspective 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的透视的详细信息[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[透视](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|  
|子元素|[操作](../../../analysis-services/scripting/collections/actions-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[计算](../../../analysis-services/scripting/collections/calculations-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)， [说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 透视提供多维数据集的子集，用于选择要包括的维度、层次结构、属性和其他详细信息，以及定义要包括的数据切片。 一个透视属于一个多维数据集。 不能在透视中覆盖或添加对象；所有维度、层次结构和其他详细信息必须存在于基础多维数据集中。 也不能包括对象，以及将其标记为不可见。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
