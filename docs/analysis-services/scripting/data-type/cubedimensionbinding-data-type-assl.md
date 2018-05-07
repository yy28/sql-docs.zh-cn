---
title: CubeDimensionBinding 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 158f405542ca124bbc0cc06f17f622fded85953e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="cubedimensionbinding-data-type-assl"></a>CubeDimensionBinding 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个派生的数据类型，表示的绑定[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)到多维数据集维度的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeDimensionBinding>  
      <!-- The following elements extend Binding -->  
   <DataSourceID>...</DataSourceID>  
   <CubeID>...</CubeID>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Filter>...</Filter>  
</CubeDimensionBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)， [CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md)， [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)，[筛选器](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)|  
|派生元素|请参阅[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 有关其他信息**绑定**类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象**绑定**类型和继承层次结构的**绑定**类型，请参阅[绑定数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定 & #40;SSAS 多维 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeDimensionBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
