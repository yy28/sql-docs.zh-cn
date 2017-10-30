---
title: "DimensionAttributeBinding 数据类型 （超的行） (ASSL) |Microsoft 文档"
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
- DimensionAttributeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DimensionAttributeBinding data type
ms.assetid: d8ec77a9-749f-4b08-8d56-8b6514a70248
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b60ccc402874d2261bd16756a0427e90cac7c22c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionattributebinding-data-type-out-of-line-assl"></a>DimensionAttributeBinding 数据类型（外部）(ASSL)
  定义一个派生数据类型，该类型表示维度中的属性的外部绑定。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <DimensionID>...</DimensionID>  
   <AttributeID>...</AttributeID>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</DimensionAttributeBinding>  
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
|子元素|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)， [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)， [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)， [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)， [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)， [翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|派生元素|[绑定](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)([绑定](../../../analysis-services/scripting/collections/attributes-element-assl.md)Analysis (XMLA) XML 集合[批处理](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)和[过程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令)|  
  
## <a name="remarks"></a>注释  
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定 &#40;SSAS 多维 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

