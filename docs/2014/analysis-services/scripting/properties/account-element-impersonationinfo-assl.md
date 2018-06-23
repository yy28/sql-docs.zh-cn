---
title: 帐户元素 (ImpersonationInfo) (ASSL) |Microsoft 文档
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
- Account Element (ImpersonationInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 454e46b3515ebd6b5ad8e8193edbc2a9aea14562
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024662"
---
# <a name="account-element-impersonationinfo-assl"></a>Account 元素 (ImpersonationInfo) (ASSL)
  包含的用户帐户的名称[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
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
 值`Account`元素，以及值[密码](password-element-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](impersonationmode-element-assl.md)任何元素的元素派生自`ImpersonationInfo`数据类型设置为*ImpersonateAccount*。  
  
## <a name="see-also"></a>请参阅  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  