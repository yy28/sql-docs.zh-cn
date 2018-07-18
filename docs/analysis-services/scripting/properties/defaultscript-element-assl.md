---
title: DefaultScript 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e21b89833edf744a6e47474e9c438be74530479c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034188"
---
# <a name="defaultscript-element-assl"></a>DefaultScript 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识默认[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)中的元素[mdxscript 被](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**True**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值设置**DefaultScript**到**True**为一个脚本设置的值**DefaultScript**到**False**对于所有其他**MdxScript**中的元素**mdxscript 被**集合。  
  
 对应于的父元素**DefaultScript**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
