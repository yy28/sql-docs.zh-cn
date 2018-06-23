---
title: ImpersonationInfo 数据类型 (ASSL) |Microsoft 文档
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
- ImpersonationInfo Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ImpersonationInfo data type
ms.assetid: 8a6b55fe-1f02-4519-bdc2-4553b576b2f3
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0525811218028039e8244c93a87090bd7909f685
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130219"
---
# <a name="impersonationinfo-data-type-assl"></a>ImpersonationInfo 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示用于模拟用户的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo>  
   <ImpersonationMode>...</ImpersonationMode>  
   <Account>...</Account>  
   <Password>   </Password>  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
</ImpersonationInfo>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[帐户](../properties/account-element-impersonationinfo-assl.md)， [ImpersonationInfoSecurity](../properties/impersonationinfosecurity-element-assl.md)， [ImpersonationMode](../properties/impersonationmode-element-assl.md)，[密码](../properties/password-element-assl.md)|  
|派生元素|[DataSourceImpersonationInfo](../properties/impersonationinfo-element-assl.md)， [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  