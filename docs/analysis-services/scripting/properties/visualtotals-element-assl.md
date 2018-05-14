---
title: VisualTotals 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0eb8c2d55700323e0fd5c83b308d12175c2c31c0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="visualtotals-element-assl"></a>VisualTotals 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含一个可以确定是否为该属性成员显示直观合计的多维表达式 (MDX)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributePermission>  
      ...  
      <VisualTotals>...</VisualTotals>  
   ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|**0**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**VisualTotals**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
