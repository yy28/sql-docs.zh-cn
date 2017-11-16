---
title: "帐户元素 (ImpersonationInfo) (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Account Element (ImpersonationInfo)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e99a3e4bd81c70fd1043465f59f76b2fab60e863
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="account-element-impersonationinfo-assl"></a>Account 元素 (ImpersonationInfo) (ASSL)
  包含的用户帐户的名称[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
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
 值**帐户**元素，以及值[密码](../../../analysis-services/scripting/properties/password-element-assl.md)元素，用于模拟目的如果的值[ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)元素任何元素派生自**ImpersonationInfo**数据类型设置为*ImpersonateAccount*。  
  
## <a name="see-also"></a>另请参阅  
 [DataSourceImpersonationInfo 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

