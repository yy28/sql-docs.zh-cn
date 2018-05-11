---
title: 密码元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1ae6eed7fd8f98aa026fceaf79efe8b5643660fa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="password-element-assl"></a>Password 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的用户帐户的密码[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**密码**元素，以及值[帐户](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)元素任何元素派生自**ImpersonationInfo**数据类型设置为*ImpersonateAccount*。  
  
 只有服务器管理员角色的成员[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例可以提供空白值**密码**元素  
  
## <a name="see-also"></a>另请参阅  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
