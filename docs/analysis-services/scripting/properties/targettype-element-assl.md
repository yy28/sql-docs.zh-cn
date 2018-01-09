---
title: "TargetType 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: TargetType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TargetType
helpviewer_keywords: TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7aa94520c72183f4aaf619d252ce7c99f35f2c96
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="targettype-element-assl"></a>TargetType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]标识中标识的项的项类型[目标](../../../analysis-services/scripting/properties/target-element-assl.md)元素。  
  
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
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
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
  
 对应于的允许值为枚举**TargetType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ActionTargetType>。  
  
 对应于的父元素**TargetType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
