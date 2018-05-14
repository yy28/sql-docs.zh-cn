---
title: 帐户元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bf3d3b56e9cc2b299ddcdec1c0a506e0168f8741
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="accounts-element-assl"></a>Accounts 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含在中定义的帐户类型的集合[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子元素|[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 维度，其[类型](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)元素设置为*帐户*、 可以具有一个属性，指定的帐户类型，例如收入，支出，等等，表示由维度中的成员。 然后使用的帐户类型[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)元素，其[AggregationFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)元素设置为*ByAccount*，以确定时要使用的聚合函数聚合该维度的成员。 **Accounts** 元素包含表示帐户类型和应应用于每个帐户类型的聚合函数的 **Account** 元素的集合。  
  
 如果聚合函数不同于使用的默认值，则必须列出帐户类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]为各种帐户类型。  
  
 有效帐户类型集是固定的。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.AccountCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [AccountType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
