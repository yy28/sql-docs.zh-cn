---
title: Alias 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54fe6d13ed207ac15a740e9c5c60d766289964b3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="alias-element-assl"></a>Alias 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的别名[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[别名](../../../analysis-services/scripting/collections/aliases-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**别名**元素用作定义的帐户的备用名称**帐户**父元素，并可帮助确定在用户的帐户类型和聚合函数的组合接口。  
  
 对应于的父元素**别名**分析管理对象 (AMO) 对象模型中的集合是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
