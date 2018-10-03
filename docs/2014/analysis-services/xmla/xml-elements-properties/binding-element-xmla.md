---
title: 绑定元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Binding Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.binding
- http://schemas.microsoft.com/analysisservices/2003/engine#Binding
- urn:schemas-microsoft-com:xml-analysis#Binding
helpviewer_keywords:
- Binding element
ms.assetid: d5acd8d4-8551-449a-ae30-d0ba828cc02d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 397e02a8aae8978d36be088b792df5edc163c63d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168243"
---
# <a name="binding-element-xmla"></a>Binding 元素 (XMLA)
  定义的外部绑定[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象，例如在维度中，属性为[绑定](bindings-element-xmla.md)系列[批处理](../xml-elements-commands/batch-element-xmla.md)或[进程](../xml-elements-commands/process-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Bindings>  
   <Binding xsi:type="DimensionAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="MeasureGroupAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="PartitionBinding">...</Binding>  
</Bindings>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DimensionAttributeBinding](../../scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupAttributeBinding](../../scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [PartitionBinding](../../scripting/data-type/binding-data-type-assl.md)|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[绑定](bindings-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Binding` 元素可定义要由 `Batch` 或 `Process` 命令处理的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 对象的外部绑定，而不是数据源和数据源视图。 有关处理对象的详细信息，请参阅[处理对象&#40;XMLA&#41;](../xml-elements-objects.md)。  
  
 有关的外部绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
