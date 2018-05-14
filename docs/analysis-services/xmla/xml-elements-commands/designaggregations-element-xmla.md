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
ms.openlocfilehash: 5338f7650cdd1f533832987f5fe79a532a9a375d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="designaggregations-element-xmla"></a>DesignAggregations 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  在将创建为聚合设计的聚合[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[具体化](../../../analysis-services/xmla/xml-elements-properties/materialize-element-xmla.md)，[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[优化](../../../analysis-services/xmla/xml-elements-properties/optimization-element-xmla.md)，[查询](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)，[步骤](../../../analysis-services/xmla/xml-elements-properties/steps-element-xmla.md)，[存储](../../../analysis-services/xmla/xml-elements-properties/storage-element-xmla.md)[时间](../../../analysis-services/xmla/xml-elements-properties/time-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **DesignAggregations**命令用于生成聚合定义存储的聚合设计。 然后，就可使用聚合设计来具体化分区的聚合，聚合设计可在各个分区之间重复使用。  
  
## <a name="see-also"></a>另请参阅  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
