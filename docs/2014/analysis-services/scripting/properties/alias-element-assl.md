---
title: Alias 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Alias Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Alias
helpviewer_keywords:
- Alias element
ms.assetid: 674fdb06-e33c-4f35-bd6a-d9bbb13ececa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b894b9883fc2146ba234bccf543a0d08d436bf86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104257"
---
# <a name="alias-element-assl"></a>Alias 元素 (ASSL)
  定义的别名[帐户](../objects/account-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[别名](../collections/aliases-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Alias` 元素的值用作 `Account` 父元素定义的帐户的备用名称，帮助标识用户界面中帐户类型和聚合函数的组合。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `Aliases` 集合的父级对应的元素为 <xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
