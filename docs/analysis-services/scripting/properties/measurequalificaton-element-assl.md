---
title: MeasureQualificaton 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 198c11e2e1b3f93f75f1f5be249350a1bd342d93
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="measurequalificaton-element-assl"></a>MeasureQualification 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定是否对中的度量值应用前缀[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <MeasureQualification>...</MeasureQualification>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*无*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*InclusionThresholdSetting*|不对此度量值组内的度量值应用前缀。|  
|*PrefixMeasureGroup*|此度量值组中每个度量值的唯一名称和标题都以度量值组的名称加上一个空格为前缀。|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**MeasureQualification**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [维度元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [MeasureGroup 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
