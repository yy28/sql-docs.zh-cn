---
title: "查询元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Query Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords: Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8de04cb54ec0fe9a28c41bcb9fed2f4362a5b7b7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="query-element-xmla"></a>Query 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含在查询[查询](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)集合使用[DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)命令在基于使用情况的优化过程。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[查询](../../../analysis-services/xmla/xml-elements-properties/queries-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **DesignAggregations** 命令通过在该命令的 **Query** 集合中包含一个或多个 **Queries** 元素来支持基于使用情况的优化。 每个 **Query** 元素表示一个目标查询，设计进程使用这些查询定义以最常用的查询为目标的聚合。 你可以指定您自己的目标查询，也可以使用存储的实例的信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]在要检索信息是最常用的查询日志中使用查询。  
  
 以迭代方式设计聚合，如果你只需在第一个传递目标查询**DesignAggregations**命令因为[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例将存储这些目标查询，并在后续期间使用这些查询**DesignAggregations**命令。 在迭代进程的第一个 **DesignAggregations** 命令中传递目标查询后，任何在 **DesignAggregations** 属性中包含目标查询的后续 **Queries** 命令都会生成错误。  
  
 **Query** 元素包含一个以逗号分隔的值，该值包含以下参数：  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *频率*  
 与该查询此前执行的次数对应的加权系数。 如果 **Query** 元素表示一个新查询，则 *Frequency* 值表示设计进程用于评估该查询的加权系数。 在设计进程中，随着频率值变大，该查询的权重也会增加。  
  
 *数据集*  
 一个数字字符串，该字符串指定维度中的哪些属性要包括在该查询中。 此字符串的字符个数必须与维度中的属性个数相同。 零 (0) 指示指定序号位置的属性不包括在指定维度的查询中，而 1 指示指定序号位置的属性包括在指定维度的查询中。  
  
 例如，字符串“011”所指的查询涉及具有三个属性的维度，其中第二个和第三个属性包括在该查询中。  
  
> [!NOTE]  
>  某些属性与数据集无关。 有关排除特性的详细信息，请参阅[属性 (XMLA)](../../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md)。  
  
 包含聚合设计的度量值组中的每个维度都由 *Query* 元素中的 **Dataset** 值表示。 *Dataset* 值的顺序必须与包括在度量值组中的维度的顺序一致。  
  
## <a name="see-also"></a>另请参阅  
 [设计聚合 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
