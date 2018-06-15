---
title: TargetType 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe1e79254f4daef21634b4e9c5b2144c857bfee0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039391"
---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识中标识的项的项类型[目标](../../../analysis-services/scripting/properties/target-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Cube*|操作目标是多维数据集。|  
|*单元格*|操作目标是子多维数据集。|  
|*设置*|操作目标是集。|  
|*层次结构*|操作目标是层次结构。|  
|*级别*|操作目标是级别。|  
|*DimensionMembers*|操作目标是维度的成员。|  
|*HierarchyMembers*|操作目标是层次结构的成员。|  
|*LevelMembers*|操作目标是级别的成员。|  
|*AttributeMembers*|操作目标是属性的成员。|  
  
 对应于的允许值为枚举**TargetType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 对应于的父元素**TargetType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
