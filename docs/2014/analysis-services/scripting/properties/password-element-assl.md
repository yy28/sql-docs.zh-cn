---
title: 密码元素 (ASSL) |Microsoft 文档
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e702e7307e11c506652e91ca4cdc8f02ca06318d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014619"
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
 值`Password`元素，以及值[帐户](account-element-impersonationinfo-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](impersonationmode-element-assl.md)任何元素的元素派生自`ImpersonationInfo`数据类型设置为*ImpersonateAccount*。  
  
 只有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的服务器管理员角色的成员可以提供 `Password` 元素的空白值  
  
## <a name="see-also"></a>请参阅  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  