---
title: ImpersonationInfoSecurity 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ImpersonationInfoSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ImpersonationInfoSecurity element
ms.assetid: 583fec36-90ef-4d6a-9888-ece6ae865c53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4aaf5aee83f6aa6102aeeb9488ddb7a75c4af540
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224898"
---
# <a name="impersonationinfosecurity-element-assl"></a>ImpersonationInfoSecurity 元素 (ASSL)
  包含一个只读的值，指示是否对中提供的安全凭据进行了任何更改[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|None|  
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
|*PasswordRemoved*|密码信息已从提供的安全凭据中删除。|  
|*保持不变*|未对提供的安全凭据进行更改。|  
  
 与允许的值相对应的枚举`ImpersonationInfoSecurity`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ImpersonationInfoSecurity>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
