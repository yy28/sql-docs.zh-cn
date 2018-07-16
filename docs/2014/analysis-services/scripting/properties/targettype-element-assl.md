---
title: TargetType 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TargetType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b21033bb9a7e20923adccfa135475cf93dafb7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237557"
---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
  标识的标识中的项的项类型[目标](target-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Cube*|操作目标是多维数据集。|  
|*单元格*|操作目标是子多维数据集。|  
|*设置*|操作目标是集。|  
|*Hierarchy*|操作目标是层次结构。|  
|*Level*|操作目标是级别。|  
|*DimensionMembers*|操作目标是维度的成员。|  
|*HierarchyMembers*|操作目标是层次结构的成员。|  
|*LevelMembers*|操作目标是级别的成员。|  
|*AttributeMembers*|操作目标是属性的成员。|  
  
 与允许的值相对应的枚举`TargetType`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 父级对应的元素`TargetType`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
