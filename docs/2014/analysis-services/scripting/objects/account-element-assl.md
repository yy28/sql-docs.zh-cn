---
title: 帐户元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Account Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 262ba3be01879770a734ab7334782e26aa04b364
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109047"
---
# <a name="account-element-assl"></a>Account 元素 (ASSL)
  包含有关内的某个帐户类型的详细信息[数据库](database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Accounts>  
   <Account>  
      <AccountType>...</AccountType>  
      <AggregationFunction>...</AggregationFunction>  
            <Aliases>...</Aliases>  
            <Annotations>...</Annotations>  
   </Account>  
</Accounts>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../collections/accounts-element-assl.md)|  
|子元素|[AccountType](../properties/accounttype-element-assl.md)， [AggregationFunction](../properties/aggregationfunction-element-assl.md)，[别名](../collections/aliases-element-assl.md)，[批注](../collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 维度，其[类型](../properties/type-element-dimension-assl.md)元素设置为*帐户，* 可以在维度中具有成员的属性的指定帐户类型，如收入、 支出，并在其他方面，表示。 然后使用的帐户类型[度量值](measure-element-assl.md)元素，其[AggregationFunction](../properties/aggregatefunction-element-assl.md)元素设置为*ByAccount*，以确定时要使用的聚合函数聚合该维度的成员。 `Account` 元素表示单个帐户类型和这类度量值应使用的聚合函数。  
  
 如果聚合函数不同于使用的默认值，则必须列出的帐户类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]为每个帐户类型。  
  
 有效帐户类型集是固定的。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>请参阅  
 [数据库元素&#40;ASSL&#41;](database-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
