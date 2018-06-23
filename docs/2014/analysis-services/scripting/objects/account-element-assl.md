---
title: 帐户元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0a99dbaee6e1eaec95385295cf1842ffcc336adf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130221"
---
# <a name="account-element-assl"></a>Account 元素 (ASSL)
  包含有关中的帐户类型的详细信息[数据库](database-element-assl.md)元素。  
  
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
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../collections/accounts-element-assl.md)|  
|子元素|[AccountType](../properties/accounttype-element-assl.md)， [AggregationFunction](../properties/aggregationfunction-element-assl.md)，[别名](../collections/aliases-element-assl.md)，[批注](../collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 维度，其[类型](../properties/type-element-dimension-assl.md)元素设置为*帐户，* 可具有属性，指定的帐户类型，例如收入，费用，以及在其他方面，表示由成员在维度中。 然后使用的帐户类型[度量值](measure-element-assl.md)元素，其[AggregationFunction](../properties/aggregatefunction-element-assl.md)元素设置为*ByAccount*，以确定时要使用的聚合函数聚合该维度的成员。 `Account` 元素表示单个帐户类型和这类度量值应使用的聚合函数。  
  
 如果聚合函数不同于使用的默认值，则必须列出帐户类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]为各种帐户类型。  
  
 有效帐户类型集是固定的。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>请参阅  
 [数据库元素&#40;ASSL&#41;](database-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  