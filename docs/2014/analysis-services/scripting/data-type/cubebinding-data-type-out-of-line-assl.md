---
title: CubeBinding 数据类型 （超的行） (ASSL) |Microsoft 文档
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
- CubeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b919e8f28d5cb102268ed3338aa0309e45a738c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125457"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 数据类型（外部）(ASSL)
  定义一个基元数据类型，表示之间的关系[多维数据集](../objects/cube-element-assl.md)元素和[数据源](../objects/datasource-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[数据源](../objects/datasource-element-assl.md)， [DataSourceID](../properties/id-element-assl.md)， [ID](../properties/id-element-assl.md)，[度量值组](../objects/group-element-assl.md)|  
|派生元素|[绑定](../../xmla/xml-elements-properties/binding-element-xmla.md)([绑定](../../xmla/xml-elements-properties/bindings-element-xmla.md)集合[过程](../../xmla/xml-elements-commands/process-element-xmla.md)或[批处理](../../xmla/xml-elements-commands/batch-element-xmla.md)命令)|  
  
## <a name="remarks"></a>Remarks  
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  