---
title: 内容元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Content Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Content
helpviewer_keywords:
- Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98d2de4a0ce93e857a63ebd9fe79dd18d0f9a86e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017616"
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
  描述中的列内容[MiningStructure](../objects/miningstructure-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此枚举描述由挖掘结构列表示的内容类型，可根据需要通过挖掘算法提供程序进行扩展。 有关内容类型的详细信息，请参阅[内容类型（数据挖掘）](../../data-mining/content-types-data-mining.md)。  
  
 下表中列出的值通常所有挖掘算法提供程序都支持。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*离散*|该列包含离散值。|  
|*连续*|该列的值定义一组连续的数值数据。|  
|*离散化*|该列中的值表示数组（或数桶）从连续列派生的值。|  
|*排序*|该列的值定义有序集。|  
|*循环*|该列的值定义循环有序集。|  
|*概率*|列的值指定概率中包含的列的[ClassifiedColumns](../collections/columns-element-assl.md)元素的父`ScalarMiningStructureColumn`。|  
|*Variance*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的方差。|  
|*标准偏差*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的概率标准偏差。|  
|*ProbabilityVariance*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的概率方差。|  
|*ProbabilityStdDev*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的标准偏差。|  
|*支持*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的支持信息。 **注意：** 此列用作第三方挖掘算法提供标准的一部分。 **注意：** Microsoft 提供的算法没有任何使用此列。 <br /><br /> 实例时都提供 SQL Server 登录名。|  
|*Key*|该列为键列。 **注意：** 此内容类型功能仅适用于键列，在其中`IsKey`元素设置为`True`。|  
  
 除了这些标准的值，挖掘算法提供程序附带[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持下表中的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*键序列*|该列为键列，并且该列的值表示一个事件序列。 **注意：** 此内容类型功能仅适用于键列，在其中`IsKey`元素设置为`True`。|  
|*Key Time*|该列为键列，并且该列的值表示时间度量单位。 **注意：** 此内容类型功能仅适用于键列，在其中`IsKey`元素设置为`True`。|  
|*序列*|该列的值表示一个事件序列。|  
|*Time*|该列的值表示时间度量单位。|  
  
 对应的允许值为枚举`Content`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [ClassifiedColumns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  