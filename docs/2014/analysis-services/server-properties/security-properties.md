---
title: 安全属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28553d897d6e3c8b9672e2b16695c9a8924c0d05
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200217"
---
# <a name="security-properties"></a>安全属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的安全服务器属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
 **适用于：** 多维和表格服务器模式  
  
## <a name="properties"></a>属性  
 `RequireClientAuthentication`  
 一个布尔值属性，指示是否需要客户端身份验证。  
  
 该属性的默认值为 True，指示需要客户端身份验证。  
  
 `SecurityPackageList`  
 字符串属性，它包含服务器用于进行客户端身份验证的 SSPI 包的列表，该列表以逗号分隔。  
  
 `DisableClientImpersonation`  
 指示是否禁用客户端模拟（例如，通过存储过程）的布尔值属性。  
  
 该属性的默认值为 False，指示启用客户端模拟。  
  
 `BuiltinAdminsAreServerAdmins`  
 指示本地计算机管理员组的成员是否为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员的布尔值属性。  
  
 `ServiceAccountIsServerAdmin`  
 指示服务帐户是否为服务器管理员的布尔值属性。  
  
 该属性的默认值为 True，指示服务帐户为服务器管理员。  
  
 `ErrorMessageMode`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `DataProtection\ RequiredProtectionLevel`  
 有符号 32 位整数属性，用于定义所有客户端请求所需的保护级别。 该属性具有下表所列的值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*0*|无，允许使用明文。|  
|*1*|（默认值）需要加密，没有明文日志记录。|  
|*2*|允许进行明文请求，但只带有签名（保护效果弱于加密）。|  
  
 `AdministrativeDataProtection\ RequiredProtectionLevel`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
