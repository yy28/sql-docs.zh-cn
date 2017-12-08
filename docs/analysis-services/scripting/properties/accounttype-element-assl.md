---
title: "AccountType 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AccountType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AccountType
helpviewer_keywords: AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e59eeeebc216840a62266cda57da8bdf2838eeba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
  包含帐户类型中定义的名称[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*收入*|该帐户是一个收入帐户。|  
|*费用*|该帐户是一个支出帐户。|  
|*流*|该帐户是一个现金流帐户。|  
|*平衡*|该帐户是一个余额帐户。|  
|*资产*|该帐户是一个资产帐户。|  
|*责任*|该帐户是一个负债帐户。|  
|*统计*|该帐户是一个统计帐户。|  
  
 对应的允许值为枚举**AccountType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>另请参阅  
 [Accounts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
