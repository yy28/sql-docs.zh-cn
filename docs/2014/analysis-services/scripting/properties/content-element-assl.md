---
title: 内容元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b27152b0c181061e25727270fd89bd423728a5a2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097857"
---
# <a name="content-element-assl"></a>Content 元素 (ASSL)
  描述中的列的内容[MiningStructure](../objects/miningstructure-element-assl.md)元素。  
  
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
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此枚举描述由挖掘结构列表示的内容类型，可根据需要通过挖掘算法提供程序进行扩展。 有关内容类型的详细信息，请参阅[内容类型（数据挖掘）](../../data-mining/content-types-data-mining.md)。  
  
 下表中列出的值通常所有挖掘算法提供程序都支持。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*离散*|该列包含离散值。|  
|*连续*|该列的值定义一组连续的数值数据。|  
|*离散化*|该列中的值表示数组（或数桶）从连续列派生的值。|  
|*排序*|该列的值定义有序集。|  
|*循环*|该列的值定义循环有序集。|  
|*概率*|列的值指定中包含的列的概率[ClassifiedColumns](../collections/columns-element-assl.md)父元素`ScalarMiningStructureColumn`。|  
|*Variance*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的方差。|  
|*标准偏差*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的概率标准偏差。|  
|*ProbabilityVariance*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的概率方差。|  
|*ProbabilityStdDev*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的标准偏差。|  
|*支持*|该列的值指定父 `ClassifiedColumns` 的 `ScalarMiningStructureColumn` 元素中包含的列的支持信息。 **注意：** 此列作为标准的一部分提供的第三方挖掘算法提供程序。 **注意：** Microsoft 提供的算法没有任何使用此列。 <br /><br /> .|  
|*Key*|该列为键列。 **注意：** 此内容类型是仅适用于在其中的键列`IsKey`元素设置为`True`。|  
  
 除了这些标准值挖掘算法提供程序附带[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持下表中的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*键序列*|该列为键列，并且该列的值表示一个事件序列。 **注意：** 此内容类型是仅适用于在其中的键列`IsKey`元素设置为`True`。|  
|*关键时间*|该列为键列，并且该列的值表示时间度量单位。 **注意：** 此内容类型是仅适用于在其中的键列`IsKey`元素设置为`True`。|  
|*序列*|该列的值表示一个事件序列。|  
|*Time*|该列的值表示时间度量单位。|  
  
 对应的允许值的枚举`Content`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [ClassifiedColumns 元素&#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
