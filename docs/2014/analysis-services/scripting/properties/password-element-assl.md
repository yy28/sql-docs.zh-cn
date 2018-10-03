---
title: Password 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fcaf2b19e885577559d00337349d77cb8f732fcb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224787"
---
# <a name="password-element-assl"></a>Password 元素 (ASSL)
  包含的用户帐户的密码[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`Password`元素，以及的值[帐户](account-element-impersonationinfo-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](impersonationmode-element-assl.md)任何元素派生自`ImpersonationInfo`数据类型设置为*ImpersonateAccount*。  
  
 只有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器管理员角色的成员可以提供 `Password` 元素的空白值  
  
## <a name="see-also"></a>请参阅  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
