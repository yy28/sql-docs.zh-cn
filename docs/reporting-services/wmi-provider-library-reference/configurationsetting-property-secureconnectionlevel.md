---
description: SecureConnectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)
title: SecureConnectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dcf7fdc038f5284d78835e64e568bb348756a3d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373153"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting 属性 - SecureConnectionLevel
  返回 RSReportServer.config 文件中指定的安全连接级别。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>属性值  
 表示安全连接级别的 **Integer** 值。 返回值指明是否配置了 TLS。 值大于或等于 1 表示启用了 TLS。 值为 0 表示禁用了 TLS。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>备注

在 SQL Server 2008 R2 中，SecureConnectionLevel 是一个开关。 有关详细信息，请参阅 [ConfigurationSetting 方法 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)。

## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
