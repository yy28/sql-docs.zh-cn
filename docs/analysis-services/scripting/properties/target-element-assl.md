---
title: Target 元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 98ec5c729f5735343f5eaa87e5232fcfb138cf38
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045775"
---
# <a name="target-element-assl"></a>Target 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识的目标[操作](../../../analysis-services/scripting/objects/action-element-assl.md)元素。  
  
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
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的预期值取决于的值[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)父元素**操作**。 下表描述了预期值**目标**值的基础**TargetType**。  
  
|TargetType 值|预期值|  
|----------------------|--------------------|  
|*Cube*|多维数据集的名称。|  
|*单元格*|子多维数据集表达式。|  
|*设置*|集表达式或命名集的名称。<br /><br /> 注意： 不能使用嵌套 select 语句。|  
|*层次结构 HierarchyMembers*|层次结构的名称。|  
|*维度 DimensionMembers*|维度的名称。|  
|*级别 LevelMembers*|级别的名称。|  
|*属性 AttributeMembers*|属性的名称。|  
  
 父级对应的元素**目标**在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
