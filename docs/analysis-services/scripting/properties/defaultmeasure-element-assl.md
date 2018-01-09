---
title: "DefaultMeasure 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DefaultMeasure Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DefaultMeasure
helpviewer_keywords: DefaultMeasure element
ms.assetid: ceac8b3d-ebae-463f-9e8c-506281d42792
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f6086bffeed2224588990c48c043c9126bc64ba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="defaultmeasure-element-assl"></a>DefaultMeasure 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含定义的默认度量值的多维表达式 (MDX) 表达式[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <DefaultMeasure>...</DefaultMeasure>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应的父级的元素**DefaultMeasure**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>和<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
