---
title: Password 元素 (ASSL) |Microsoft Docs
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
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99d7eabdd66e6c7f036389b4825c5926873367b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197737"
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
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值`Password`元素，以及的值[帐户](account-element-impersonationinfo-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](impersonationmode-element-assl.md)任何元素派生自`ImpersonationInfo`数据类型设置为*ImpersonateAccount*。  
  
 只有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器管理员角色的成员可以提供 `Password` 元素的空白值  
  
## <a name="see-also"></a>请参阅  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
