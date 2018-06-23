---
title: 目标元素 (ASSL) |Microsoft 文档
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
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Target
helpviewer_keywords:
- Target element
ms.assetid: 08ce0441-94b6-4f1d-acba-f31c8212cb79
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 65150d66769a2ebdb67609989efbc1a7f81e9f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015972"
---
# <a name="target-element-assl"></a>Target 元素 (ASSL)
  标识的目标[操作](../objects/action-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <Target>...</Target>  
   ...  
</Action>  
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
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的预期值取决于值[TargetType](targettype-element-assl.md)的父元素`Action`。 下表介绍基于 `Target` 值的 `TargetType` 预期值。  
  
|TargetType 值|预期值|  
|----------------------|--------------------|  
|*Cube*|多维数据集的名称。|  
|*单元格*|子多维数据集表达式。|  
|*设置*|集表达式或命名集的名称。 **注意：** 不能使用嵌套 select 语句。|  
|*层次结构 HierarchyMembers*|层次结构的名称。|  
|*维度 DimensionMembers*|维度的名称。|  
|*级别 LevelMembers*|级别的名称。|  
|*属性 AttributeMembers*|属性的名称。|  
  
 对应于的父元素`Target`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  