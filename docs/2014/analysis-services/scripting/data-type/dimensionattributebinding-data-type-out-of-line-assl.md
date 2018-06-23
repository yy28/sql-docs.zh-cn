---
title: DimensionAttributeBinding 数据类型 （超的行） (ASSL) |Microsoft 文档
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
- DimensionAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DimensionAttributeBinding data type
ms.assetid: d8ec77a9-749f-4b08-8d56-8b6514a70248
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6f72755c02c6b8b07cdf67c4d5464d1f3b2d9e55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125235"
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
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[绑定](binding-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[AttributeID](../properties/id-element-assl.md)， [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md)， [DimensionID](../properties/dimensionid-element-assl.md)， [KeyColumns](../collections/columns-element-assl.md)， [NameColumn](../objects/column-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
|派生元素|[绑定](../../xmla/xml-elements-properties/binding-element-xmla.md)([绑定](../collections/attributes-element-assl.md)Analysis (XMLA) XML 集合[批处理](../../xmla/xml-elements-commands/batch-element-xmla.md)和[过程](../../xmla/xml-elements-commands/process-element-xmla.md)命令)|  
  
## <a name="remarks"></a>Remarks  
 有关扩展的行绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  