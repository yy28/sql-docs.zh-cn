---
title: "CubeBinding 数据类型 （超的行） (ASSL) |Microsoft 文档"
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
- CubeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0624bd051d8534e82b608bc925236abc0153798
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 数据类型（外部）(ASSL)
  定义一个基元数据类型，表示之间的关系[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素和[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[度量值组](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|派生元素|[绑定](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)([绑定](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)集合[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)或[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令)|  
  
## <a name="remarks"></a>注释  
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
