---
title: PermissionSet 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PermissionSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 590dbc9ae62340fd3d4cf08d06f8a593bcf520f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049299"
---
# <a name="permissionset-element-assl"></a>PermissionSet 元素 (ASSL)
  标识与关联的权限集[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 程序集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*安全*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*安全*|只允许内部计算和本地数据访问。 *安全*是限制性最强的权限集。 所执行的程序集代码*安全*权限无法访问外部系统资源，例如文件、 网络、 环境变量或注册表。|  
|*ExternalAccess*|*安全*，以及访问外部系统资源，如文件、 网络、 环境变量和注册表的附加功能。|  
|*不受限制*|不受限制允许程序集不受限制地访问资源，内部和外部[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在执行的代码*Unrestricted*程序集可以调用非托管的代码。|  
  
 与允许的值相对应的枚举`PermissionSet`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.PermissionSet>。  
  
## <a name="see-also"></a>请参阅  
 [ComAssembly 数据类型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [程序集元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
