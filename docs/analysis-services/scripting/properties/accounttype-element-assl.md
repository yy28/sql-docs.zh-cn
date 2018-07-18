---
title: AccountType 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5258ff60c8dfafefbf81f87d3538c396c085ccac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035178"
---
# <a name="accounttype-element-assl"></a>AccountType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|“值”|Description|  
|-----------|-----------------|  
|*收入*|该帐户是一个收入帐户。|  
|*费用*|该帐户是一个支出帐户。|  
|*流*|该帐户是一个现金流帐户。|  
|*平衡*|该帐户是一个余额帐户。|  
|*资产*|该帐户是一个资产帐户。|  
|*负债*|该帐户是一个负债帐户。|  
|*统计*|该帐户是一个统计帐户。|  
  
 对应的允许值为枚举**AccountType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AccountTypes>。  
  
## <a name="see-also"></a>另请参阅  
 [帐户元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
