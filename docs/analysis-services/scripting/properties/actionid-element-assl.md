---
title: 操作 Id 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c118c7218892684acf357408f6cd3c80bf014ec0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032518"
---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
