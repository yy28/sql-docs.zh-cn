---
title: CubeID 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4199a856953c9a5c27bfd36bfac16cbedcc1d74c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cubeid-element-assl"></a>CubeID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素与关联[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeAttributeBinding> <!-- or CubeDimensionBinding, MeasureGroupAttributeBinding, MeasureGroupBinding -->  
   ...  
   <CubeID>...</CubeID>  
      ...  
</CubeAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)， [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**CubeID**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.CubeAttributeBinding>， <xref:Microsoft.AnalysisServices.CubeDimensionBinding>，和<xref:Microsoft.AnalysisServices.MeasureGroupBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
