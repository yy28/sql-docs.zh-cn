---
title: "内容元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Content Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Content
helpviewer_keywords: Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7385e2307a9cafcf761c8ac160e1d46175daaad3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述中的列内容[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此枚举描述由挖掘结构列表示的内容类型，可根据需要通过挖掘算法提供程序进行扩展。 有关内容类型的详细信息，请参阅[内容类型（数据挖掘）](../../../analysis-services/data-mining/content-types-data-mining.md)。  
  
 下表中列出的值通常所有挖掘算法提供程序都支持。  
  
|值|Description|  
|-----------|-----------------|  
|*离散*|该列包含离散值。|  
|*连续*|该列的值定义一组连续的数值数据。|  
|*离散化*|该列中的值表示数组（或数桶）从连续列派生的值。|  
|*排序*|该列的值定义有序集。|  
|*循环*|该列的值定义循环有序集。|  
|*概率*|列的值指定概率中包含的列的[ClassifiedColumns](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)元素的父**ScalarMiningStructureColumn**。|  
|*Variance*|列的值指定的中包含的列的方差**ClassifiedColumns**元素的父**ScalarMiningStructureColumn**。|  
|*标准偏差*|列的值指定中包含的列标准偏差**ClassifiedColumns**元素的父**ScalarMiningStructureColumn**。|  
|*ProbabilityVariance*|列的值指定的中包含的列的概率方差**ClassifiedColumns**元素的父**ScalarMiningStructureColumn**。|  
|*ProbabilityStdDev*|列的值指定中包含的列概率标准偏差**ClassifiedColumns**元素的父**ScalarMiningStructureColumn**。|  
|*支持*|列的值指定列中包含的支持信息**ClassifiedColumns**元素的父**ScalarMiningStructureColumn**。<br /><br /> 注意： 此列作为标准的一部分的第三方挖掘算法提供程序。 Microsoft 提供的算法不能使用此列。|  
|*Key*|该列为键列。<br /><br /> 注意： 此内容类型功能仅适用于键列，在其中**IsKey**元素设置为**True**。|  
  
 除了这些标准的值，挖掘算法提供程序附带[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持下表中的值。  
  
|值|Description|  
|-----------|-----------------|  
|*键序列*|该列为键列，并且该列的值表示一个事件序列。<br /><br /> 注意： 此内容类型功能仅适用于键列，在其中**IsKey**元素设置为**True**。|  
|*Key Time*|该列为键列，并且该列的值表示时间度量单位。<br /><br /> 注意： 此内容类型功能仅适用于键列，在其中**IsKey**元素设置为**True**。|  
|*序列*|该列的值表示一个事件序列。|  
|*Time*|该列的值表示时间度量单位。|  
  
 对应的允许值为枚举**内容**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [ClassifiedColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
