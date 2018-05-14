---
title: IgnoreUnrelatedDimensions 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fb55ec97bc6ca2e619e04b43b1e56869c57db5b2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="ignoreunrelateddimensions-element-assl"></a>IgnoreUnrelatedDimensions 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|True|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 当**IgnoreUnrelatedDimensions**是**true**，将无关的维度强制到其顶层; 值时**false**，维度不强制到其顶层。 此属性是为多维表达式 (MDX) 类似[ValidMeasure](../../../mdx/validmeasure-mdx.md)函数。  
  
 对应于的父元素**IgnoreUnrelatedDimensions**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
