---
title: HideMemberIf 元素 (ASSL) |Microsoft Docs
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
- HideMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HideMemberIf
helpviewer_keywords:
- HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0829804ae0225c848da3583c429e39d9bc176821
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187024"
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 元素 (ASSL)
  指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*永远不会*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Level](../objects/level-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*永远不会*|从不隐藏成员。|  
|*OnlyChildWithNoName*|如果成员是其父级的唯一子级并且成员名称为空，则隐藏该成员。|  
|*OnlyChildWithParentName*|如果成员是其父级的唯一子级并且其名称与其父级名称相同，则隐藏该成员。|  
|*NoName*|如果成员名称为空，则隐藏该成员。|  
|*ParentName*|如果成员名称与其父级名称相同，则隐藏该成员。|  
  
## <a name="remarks"></a>Remarks  
 与允许的值相对应的枚举`HideMemberIf`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.HideIfValue>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
