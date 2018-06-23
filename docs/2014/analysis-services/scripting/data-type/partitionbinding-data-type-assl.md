---
title: PartitionBinding 数据类型 (ASSL) |Microsoft 文档
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
- PartitionBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PartitionBinding
helpviewer_keywords:
- PartitionBinding data type
ms.assetid: 859d4b47-31c7-4678-9388-254fec484299
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c4e265cd83401d480de74adf89949dd8edf73616
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029126"
---
# <a name="partitionbinding-data-type-assl"></a>PartitionBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示一种绑定到[分区](../objects/partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PartitionBinding>  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <PartitionID>...</PartitionID>  
   <Source>...</Source>  
</PartitionBinding>  
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
|子元素|[CubeID](../../xmla/xml-elements-properties/id-element-xmla.md)， [DatabaseID](../../xmla/xml-elements-properties/databaseid-element-xmla.md)， [PartitionID](../../xmla/xml-elements-properties/partitionid-element-xmla.md)，[源](../properties/source-element-binding-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 有关其他信息`Binding`类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象`Binding`类型和继承层次结构的`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  