---
title: CubeBinding 数据类型 （超的行） (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68bc808952f85efd2056df07b8fb5d8a60561bf7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 数据类型（外部）(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定 & #40;SSAS 多维 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [绑定数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
