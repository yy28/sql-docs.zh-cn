---
title: MeasureGroupAttributeBinding 数据类型 （的外部） (ASSL) |Microsoft Docs
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
- MeasureGroupAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 244656b0ae951ec5f8274f11e58153faef80957d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218207"
---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>MeasureGroupAttributeBinding 数据类型（外部）(ASSL)
  定义一个派生数据类型，该类型表示包含在度量值组中的维度的属性外部绑定。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <GranularityAttributeID>...</GranularityAttributeID>  
   <Source>...</Source>  
</MeasureGroupAttributeBinding>  
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
|子元素|[CubeID](../properties/id-element-assl.md)， [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md)， [MeasureGroupID](../properties/measuregroupid-element-assl.md)， [GranularityAttributeID](../properties/attributeid-element-assl.md)，[源](../properties/source-element-binding-assl.md)|  
|派生元素|[绑定](../../xmla/xml-elements-properties/binding-element-xmla.md)([绑定](../collections/attributes-element-assl.md)集合的 XML for Analysis (XMLA)[批处理](../../xmla/xml-elements-commands/batch-element-xmla.md)并[过程](../../xmla/xml-elements-commands/process-element-xmla.md)命令)|  
  
## <a name="remarks"></a>Remarks  
 有关的外部绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
