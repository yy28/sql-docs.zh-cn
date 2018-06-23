---
title: 查询元素 (XMLA) |Microsoft 文档
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
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: e01c14cb889a7d2953c98d8dfeee3bb89eee344e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027066"
---
# <a name="query-element-xmla"></a>Query 元素 (XMLA)
  包含在查询[查询](queries-element-xmla.md)集合使用[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)命令在基于使用情况的优化过程。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[查询](queries-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DesignAggregations` 命令通过在该命令的 `Query` 集合中包含一个或多个 `Queries` 元素来支持基于使用情况的优化。 每个`Query`元素表示一个目标查询，用于定义目标的最常用的查询的聚合设计过程。 你可以指定您自己的目标查询，也可以使用存储的实例的信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]在要检索信息是最常用的查询日志中使用查询。  
  
 以迭代方式设计聚合，如果你只需在第一个传递目标查询`DesignAggregations`命令因为[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例存储这些目标查询，并在后续过程中使用这些查询`DesignAggregations`命令。 在迭代进程的第一个`DesignAggregations` 命令中传递目标查询后，任何在 `DesignAggregations` 属性中包含目标查询的后续 `Queries` 命令都会生成错误。  
  
 `Query` 元素包含一个以逗号分隔的值，该值包含以下参数：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *频率*  
 与该查询此前执行的次数对应的加权系数。 如果`Query`元素表示一个新的查询，*频率*值表示设计进程用于评估该查询加权系数。 在设计进程中，随着频率值变大，该查询的权重也会增加。  
  
 *数据集*  
 一个数字字符串，该字符串指定维度中的哪些属性要包括在该查询中。 此字符串的字符个数必须与维度中的属性个数相同。 零 (0) 指示指定序号位置的属性不包括在指定维度的查询中，而 1 指示指定序号位置的属性包括在指定维度的查询中。  
  
 例如，字符串“011”所指的查询涉及具有三个属性的维度，其中第二个和第三个属性包括在该查询中。  
  
> [!NOTE]  
>  某些属性与数据集无关。 有关排除特性的详细信息，请参阅[属性 (XMLA)](query-element-xmla.md)。  
  
 包含聚合设计的度量值组中每个维度都由*数据集*中的值`Query`元素。 *Dataset* 值的顺序必须与包括在度量值组中的维度的顺序一致。  
  
## <a name="see-also"></a>请参阅  
 [设计聚合&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  