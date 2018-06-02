---
title: DesignAggregations 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b32a7ecaf7c8268b88d3fc417cc1e41e024bfd2f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574129"
---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 实例上创建的聚合设计的聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <DesignAggregations>  
      <Object>...</Object>  
      <Time>...</Time>  
      <Steps>...</Steps>  
      <Optimization>...</Optimization>  
      <Storage>...</Storage>  
      <Materialize>...</Materialize>  
      <Queries>...</Queries>  
   </DesignAggregations>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[具体化](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md)，[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[优化](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md)，[查询](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)，[步骤](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md)，[存储](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md)[时间](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **DesignAggregations**命令用于生成聚合定义存储的聚合设计。 然后，就可使用聚合设计来具体化分区的聚合，聚合设计可在各个分区之间重复使用。  
  
## <a name="see-also"></a>另请参阅
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
