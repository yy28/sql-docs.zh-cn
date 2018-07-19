---
title: Text 元素 (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 77e7fad88ddba7d6eaed048f1c2b1ef95bd9c5bb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062705"
---
# <a name="text-element-assl"></a>Text 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的文本[命令](../../../analysis-services/scripting/objects/command-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
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
|父元素|[Command](../../../analysis-services/scripting/objects/command-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 父级对应的元素**文本**在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Command>。  
  
## <a name="see-also"></a>请参阅  
 [命令元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)   
 [属性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
