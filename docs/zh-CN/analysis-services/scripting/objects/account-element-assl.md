---
title: 帐户元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Account Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Account
helpviewer_keywords:
- Account element
ms.assetid: 0bb7d06c-0158-4ab2-b2b1-cb50ba24f7c0
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 54da4e03516002762f0312e50bcf1256279be58f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="account-element-assl"></a>Account 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含有关中的帐户类型的详细信息[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../../../analysis-services/scripting/collections/accounts-element-assl.md)|  
|子元素|[AccountType](../../../analysis-services/scripting/properties/accounttype-element-assl.md)， [AggregationFunction](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md)，[别名](../../../analysis-services/scripting/collections/aliases-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 维度，其[类型](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)元素设置为*帐户，*可具有属性，指定的帐户类型，例如收入，费用，以及在其他方面，表示由成员在维度中。 然后使用的帐户类型[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)元素，其[AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)元素设置为*ByAccount*，以确定时要使用的聚合函数聚合该维度的成员。 **帐户**元素表示单个帐户类型和应该使用的此类度量值的聚合函数。  
  
 如果聚合函数不同于使用的默认值，则必须列出帐户类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]为各种帐户类型。  
  
 有效帐户类型集是固定的。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Account>。  
  
## <a name="see-also"></a>另请参阅  
 [数据库元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
