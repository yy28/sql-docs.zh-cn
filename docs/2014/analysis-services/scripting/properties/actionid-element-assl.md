---
title: 操作 Id 元素 (ASSL) |Microsoft 文档
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
- ActionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ActionID
helpviewer_keywords:
- ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13e83d3a022416de56cba7bbf6693ea408b51562
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026014"
---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
  包含名称的[操作](../objects/action-element-assl.md)元素上定义[多维数据集](../objects/cube-element-assl.md)在中可用的元素[透视](../objects/perspective-element-assl.md)元素作为[PerspectiveAction](../data-type/action-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PerspectiveAction](../data-type/action-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`ActionID`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PerspectiveAction>。  
  
## <a name="see-also"></a>请参阅  
 [操作元素&#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  