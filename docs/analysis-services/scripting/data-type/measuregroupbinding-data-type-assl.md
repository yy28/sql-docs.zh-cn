---
title: "MeasureGroupBinding 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupBinding
helpviewer_keywords:
- MeasureGroupBinding data type
ms.assetid: 47e83eec-e0bc-4118-9a0f-5bfdd6218297
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0045e3f58bbbf50699ad25b823969771c23efdd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroupbinding-data-type-assl"></a>MeasureGroupBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示一种绑定到[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupBinding>  
   <!-- The following elements extend Binding -->  
   <DataSourceID>...</DataSourceID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Persistence>...</Persistence>  
   <RefreshPolicy>...</RefreshPolicy>  
   <RefreshInterval>...</RefreshInterval>  
   <Filter>...</Filter>  
</MeasureGroupBinding>  
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
|子元素|[CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md)， [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)，[筛选器](../../../analysis-services/scripting/properties/filter-element-binding-assl.md)， [MeasureGroupID](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md)，[持久性](../../../analysis-services/scripting/properties/persistence-element-assl.md)， [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)， [RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)|  
|派生元素|请参阅[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 有关其他信息**绑定**类型，包括 Analysis Services 脚本语言 (ASSL) 对象的绑定类型和继承层次结构的表**绑定**类型，请参阅[绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MeasureGroupBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

