---
title: AccountType 元素 (ASSL) |Microsoft 文档
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
- AccountType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AccountType
helpviewer_keywords:
- AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ff7203d2882689b21a6ab3171880c26a8d385f7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126172"
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
  包含帐户类型中定义的名称[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../objects/account-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*收入*|该帐户是一个收入帐户。|  
|*费用*|该帐户是一个支出帐户。|  
|*流*|该帐户是一个现金流帐户。|  
|*平衡*|该帐户是一个余额帐户。|  
|*资产*|该帐户是一个资产帐户。|  
|*责任*|该帐户是一个负债帐户。|  
|*统计*|该帐户是一个统计帐户。|  
  
 对应的允许值为枚举`AccountType`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>请参阅  
 [帐户元素&#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  