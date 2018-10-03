---
title: ImpersonationMode 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ImpersonationMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87a68d6ef1035d7caf1d787d9ab44578d17c5489
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105139"
---
# <a name="impersonationmode-element-assl"></a>ImpersonationMode 元素 (ASSL)
  包含一个值，指示派生自的元素的模拟方法[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*默认*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*默认*|父级使用最适合使用了模拟的上下文的模拟方法。|  
|*ImpersonateAccount*|父级使用父元素中指定的用户帐户的凭据。|  
|*ImpersonateAnonymous*|父级使用匿名用户的凭据。|  
|*ImpersonateCurrentUser*|父级使用当前用户的凭据。|  
|*ImpersonateServiceAccount*|父级使用与实例相关联的服务帐户的凭据[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
  
 与允许的值相对应的枚举`ImpersonationMode`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ImpersonationLevel>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
