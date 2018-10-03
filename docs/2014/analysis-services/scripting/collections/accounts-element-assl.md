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
- Accounts Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Accounts
helpviewer_keywords:
- Accounts element
ms.assetid: 3ec62f58-c19b-4b15-b040-8941521a389b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d0dd0fabf7ebfc6ee020a533149b73e72f7a8a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126137"
---
# <a name="accounts-element-assl"></a>Accounts 元素 (ASSL)
  包含集合中定义的帐户类型[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
   ...  
   <Accounts>  
      <Account>...</Account>  
   </Accounts>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](../objects/database-element-assl.md)|  
|子元素|[帐户](../objects/account-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 维度，其[类型](../properties/type-element-dimension-assl.md)元素设置为*帐户*，可以具有的属性的指定帐户类型，例如收入，支出等，由维度中的成员表示。 然后使用的帐户类型[度量值](../objects/measure-element-assl.md)元素，其[AggregationFunction](../properties/aggregatefunction-element-assl.md)元素设置为*ByAccount*，以确定时要使用的聚合函数聚合该维度的成员。 `Accounts` 元素包含表示帐户类型和应应用于每个帐户类型的聚合函数的 `Account` 元素的集合。  
  
 如果聚合函数不同于使用的默认值，则必须列出的帐户类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]为每个帐户类型。  
  
 有效帐户类型集是固定的。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AccountCollection>。  
  
## <a name="see-also"></a>请参阅  
 [AccountType 元素&#40;ASSL&#41;](../properties/accounttype-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
