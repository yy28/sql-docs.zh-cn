---
title: CaptionIsMdx 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0989516071c157d6e5ad6a29ee852a27022850e9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="captionismdx-element-assl"></a>CaptionIsMdx 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义是否为标题[操作](../../../analysis-services/scripting/objects/action-element-assl.md)元素是一个多维表达式 (MDX) 表达式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action>  
   ...  
   <CaptionIsMdx>...</CaptionIsMdx>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**False**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**CaptionIsMdx**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
