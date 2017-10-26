---
title: "操作 Id 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ActionID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ActionID
helpviewer_keywords:
- ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7a37bba497503e9d3c01031e3256baa86d1e3e0a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
  包含名称的[操作](../../../analysis-services/scripting/objects/action-element-assl.md)元素上定义[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)在中可用的元素[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素作为[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ActionID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.PerspectiveAction>。  
  
## <a name="see-also"></a>另请参阅  
 [操作元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/actions-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

