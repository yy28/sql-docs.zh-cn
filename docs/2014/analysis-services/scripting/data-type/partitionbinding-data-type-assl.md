---
title: PartitionBinding 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc5053c872b804740f121a9b8712eb3569a95444
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227927"
---
# <a name="partitionbinding-data-type-assl"></a>PartitionBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示绑定到[分区](../objects/partition-element-assl.md)元素。  
  
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
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[CubeID](../../xmla/xml-elements-properties/id-element-xmla.md)， [DatabaseID](../../xmla/xml-elements-properties/databaseid-element-xmla.md)， [PartitionID](../../xmla/xml-elements-properties/partitionid-element-xmla.md)，[源](../properties/source-element-binding-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>备注  
 有关其他信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 对象的表`Binding`类型和继承层次结构`Binding`类型，请参阅[&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 有关 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
